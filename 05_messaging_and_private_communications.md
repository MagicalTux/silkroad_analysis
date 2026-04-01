# Messaging & Private Communications

## Architecture

The messaging system uses a **per-user table design**: each user gets their own `messagesN` table (where N = their user uid). There are 522 message tables total. The base `messages` table contains 20 system-level messages.

Each message has: `type` (message/feedback/feedback_request), `from` (sender uid), `subject`, `message` body, `date`, and `read` status.

## Message Types

Messages fell into several categories:
- **User-to-user communication**: Private messages between buyers and sellers
- **System notifications**: "Your item has been sold!", "Your order has been shipped!", "Your item has been delivered!"
- **Feedback**: Buyer ratings and reviews
- **Admin support**: Bug reports, complaints, feature requests sent to the Silk Road account

## The Admin's Inbox (messages1): A Window Into Operations

The Silk Road admin's message inbox is the richest data source, containing ~120+ messages. Key themes:

### Early Inquiries (Jan-Feb 2011)
- "is the web site still functioning?" (Jan 23)
- "Is this an actual operation? How is business?" (Feb 8)
- "Can you get me a gun?" (Feb 10)
- "Im curious as if you all are legit. only 126 registered users? and 13 transactions?" (Feb 22)

These messages show the site struggled with credibility in its first weeks.

### Bug Reports & Technical Issues
Users reported significant bugs directly to the admin:

1. **Critical auth bug**: "If I'm not logged in and go to messages.php I get the message folder from someone else" (user #114, Feb 22)
2. **SQL/XSS vulnerabilities**: "Profile descriptions are vulnerable to HTML injection" (nvram, Feb 28)
3. **Payment processing errors**: PHP parse errors, MySQL connection failures for `www-data` user
4. **Broken checkout**: After adding SQL injection protections, the checkout page broke for ~4 hours (acknowledged in forum post Mar 3)
5. **Blank messages**: Special characters (Scandinavian letters) caused messages to arrive empty

### Security Warnings

One particularly prescient message from user `d72sh` (message #12, Mar 8):
> "i hope you have not accessed the bitcoin.org forums on clearnet; as it is possible to tie your identity there (and everything posted in your silk road thread) to this site. a subpoena will reveal the IP's from which your account has logged into bitcoin.org/smf."

This was prophetic -- the FBI did exactly this to identify Ulbricht years later.

Another user (#293) warned about the WHOIS records for `silkroadmarket.org`:
> "whats up with having info in whois record? ur talk in the forums + whois record seems like plausible id... its not going to be hard to put 2+2 together if that phone falls into the wrong hands."

### Goldismoney's Password Leak

User `Goldismoney` (a major mescaline seller) got locked out of their account and messaged the admin from a different account (#221), revealing their password in plaintext: `[redacted]`. This demonstrates the casual attitude toward security even among active vendors.

### Development Offers

User #223 offered to help with development: "would like to offer development help. experienced with html, css, php, mysql, and others."

### The nvram Relationship

nvram (user 145) had an extensive message exchange with the admin, revealing:
- He was reselling Silk Road products locally in Austin, TX
- He inquired about selling cocaine
- He asked the admin "Did you code this entire PHP system yourself?" (the admin confirmed)
- He reported the admin was from Texas: "Fuckin' A. I'm from Texas too"
- He asked to rename his account to "iceland"

## System Message Templates

The automated messages reveal the escrow workflow:

**Sale notification to seller:**
> "Congratulations, [qty] of your items, "[title]," has sold for [amount] BTC! Your buyers funds have been secured and are being held in escrow until their order arrives. Please ship within the next 72 hours..."

**Shipment notification to buyer:**
> "Your order, [title], has been shipped. Please allow up to 10 days for your order to arrive. Once it arrives, please confirm delivery..."

**Delivery confirmation to seller:**
> "Your buyer confirmed delivery of [qty] '[title]'! The amount of [X] BTC will be deposited into your Bitcoin account ([address]) within 48 hours."

Early versions of these templates had HTML `<br />` tags mixed with `\n` newlines, and several had missing variable interpolation (showing empty fields where usernames/item names should be) -- more evidence of the amateur PHP codebase.
