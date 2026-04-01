# Silk Road Database: Overview & Structure

## What This Database Is

This is an early copy of the Silk Road 1.0 MySQL database, covering the site's first ~10 weeks of operation: **January 10, 2011 through March 21, 2011**. Silk Road was founded by Ross Ulbricht (known online as "Dread Pirate Roberts") and operated as a Tor hidden service at `ianxz6zefk72ulzz.onion`.

This snapshot captures the marketplace in its infancy -- before the June 2011 Gawker article that brought it mainstream attention, and over two years before the FBI seized the site in October 2013.

## Provenance

This database copy was uploaded by Ulbricht (presumably) to a MySQL server at KalyHost.com -- a hosting provider run by Mark Karpeles (later known as the operator of the Mt. Gox Bitcoin exchange). KalyHost is also where Ulbricht purchased the `silkroadmarket.org` clearnet domain, using a fake name and paying with Bitcoin. The purpose of uploading the database to this third-party server is unknown -- it may have been a backup, a migration attempt, or related to the hosting of the clearnet gateway. Regardless of intent, placing a complete copy of the operational database on infrastructure outside his control represents a significant OPSEC failure.

## Database Summary

| Table | Rows | Description |
|-------|------|-------------|
| `users` | 521 | All registered accounts |
| `items` | 132 | Product listings |
| `transactions` | 136 | Completed/pending orders |
| `categories` | 7 | Product categories |
| `stats` | 92,449 | Page view analytics |
| `variables` | 1 | Site configuration (BTC exchange rate) |
| `forum_topics` | 6 | Forum sections |
| `forum_threads` | 96 | Forum discussion threads |
| `forum_posts` | 449 | Individual forum posts |
| `messages` (base) | 20 | System-level messages |
| `messages1`-`messages523` | ~522 tables | Per-user private message inboxes |

## Date Range

- **First user registration:** January 10, 2011 (user "Silk Road" -- the admin account)
- **Last activity in snapshot:** March 21, 2011
- **Stats tracking begins:** February 15, 2011
- **Stats tracking ends:** March 21, 2011

## Technical Observations

### Schema Design

The database is hand-built PHP/MySQL with no framework. Key observations:

- **Nearly everything is `varchar(99)` or `varchar(9999)`** -- prices, dates, booleans, quantities are all stored as strings rather than proper numeric/datetime types. Dates are Unix timestamps stored in varchar fields.
- **Per-user message tables**: Rather than a single messages table with a `recipient_id` column, each user gets their own `messagesN` table (where N = user uid). There are 522 message tables for 521 users, suggesting the base `messages` table is shared/system-level.
- **No foreign keys**: Relationships between tables are implicit (e.g., `items.userid` references `users.uid` but there's no constraint).
- **No indexes** beyond primary keys -- consistent with a beginner-level MySQL setup.
- **Passwords stored in the `pass` field** -- likely hashed but no salt column visible.

### The `variables` Table

Contains a single row:
- `xrate = 0.7615` -- This is the BTC/USD exchange rate. At the time, 1 BTC was worth approximately $0.76. This means the prices listed in BTC translate to very modest USD amounts by today's standards, but were standard for early 2011.

### The `stats` Table

A rudimentary analytics system logging every page view with:
- Unix timestamp
- Current page URL
- Referring page URL
- User ID (if logged in)

92,449 page views were recorded between February 15 and March 21, 2011.

### Code Clues From Bug Reports

Messages from users to the admin reveal the site was written in plain PHP:
- File paths like `/var/www/include/functions.php`, `/var/www/payment_sent.php`
- MySQL connection errors showing the `www-data` user
- SQL injection and XSS vulnerabilities were reported and patched during this period
- A user reported a critical bug: viewing `/messages.php` while not logged in showed another user's inbox

The admin confirmed in a forum conversation that he coded the entire PHP system himself.
