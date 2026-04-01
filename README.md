# Silk Road Early Database Analysis

Analysis of an early copy of the Silk Road 1.0 MySQL database, covering the marketplace's first **10 weeks of operation** (January 10 -- March 21, 2011).

## Background

Silk Road was the first major darknet marketplace, operated by Ross Ulbricht as a Tor hidden service from 2011 until its seizure by the FBI in October 2013. At its peak it had over 100,000 buyers and generated $1.2 billion in revenue.

This database predates all of that. It captures the site when it had **521 users**, **132 listings**, and **$4,153 in total sales** -- a one-man PHP operation selling mushrooms to a few hundred early adopters, two months before the Gawker article that made it famous.

## Provenance

This database was found on a MySQL server at KalyHost.com, a hosting provider run by Mark Karpeles (later known as the operator of the Mt. Gox Bitcoin exchange). Ulbricht had purchased the `silkroadmarket.org` clearnet domain from KalyHost using a fake name and Bitcoin payment, and uploaded this copy of the Silk Road database to the same server for unknown reasons -- possibly as a backup or for the clearnet gateway.

## Reports

1. **[Overview & Database Structure](01_overview_and_database_structure.md)** -- Schema design, table sizes, date ranges, and technical observations about the amateur PHP/MySQL codebase.

2. **[Users & Sellers](02_users_and_sellers.md)** -- 521 users, 99 sellers, registration growth, notable accounts including the `altoid` promotional account (UID 2) and power users like `nvram` and `1UP of Canada`.

3. **[Marketplace & Listings](03_marketplace_and_listings.md)** -- 132 listings across 7 drug categories, pricing in both BTC and USD (at $0.76/BTC), the admin's mushroom store, and notable non-drug items (stolen credit cards, a parking placard, a Bitcoin mixing service).

4. **[Transactions & Finances](04_transactions_and_finances.md)** -- 136 transactions totaling 5,465 BTC (~$4,153), revenue breakdown by seller, the escrow workflow, and the critical finding that shipping addresses were stored in plaintext.

5. **[Messaging & Private Communications](05_messaging_and_private_communications.md)** -- Per-user message table architecture, the admin's inbox revealing bug reports and operational conversations, security warnings from users, and system message templates.

6. **[Forum & Community](06_forum_and_community.md)** -- 96 threads and 449 posts covering trust systems, growth-vs-security debates, Bitcoin anonymity concerns, GPG advocacy, weapons discussions, and product requests.

7. **[Site Analytics & Traffic](07_site_analytics_and_traffic.md)** -- 92,449 page views showing 10x traffic growth over 3 weeks, most visited pages, and the top 20 most active users.

8. **[Security & OPSEC Analysis](08_security_and_opsec_analysis.md)** -- The admin's OPSEC failures (altoid trail, clearnet domain, database upload, geographic clues), user OPSEC failures (real names, plaintext addresses), and technical vulnerabilities reported during this period.

9. **[Historical Significance](09_historical_significance.md)** -- Context within the broader Silk Road timeline, connections to the criminal investigation, the altoid/Ulbricht link, and what this genesis-period snapshot reveals about the seeds of the site's eventual downfall.

10. **[Private Messages Deep Dive](10_private_messages_deep_dive.md)** -- Analysis of seller and buyer inboxes beyond the admin's. Includes altoid's failed drug deal, the admin's dispute with 1UP of Canada over GPG encryption, the maxvendor reliability crisis, email/IP address leaks in messages, and pink's documented search for heroin.

## Key Findings

- **The `altoid` account (UID 2)** is the second user ever registered, 5 days after the admin -- the same username Ulbricht used to promote Silk Road on clearnet forums, which the FBI later traced back to him.
- **The admin was the #1 seller**, responsible for 30% of all orders (mushrooms), making him maximally exposed to drug trafficking charges.
- **Shipping addresses were stored in plaintext** despite the admin's claims of encryption, exposing buyer identities across 12+ countries.
- **The site had basic web vulnerabilities** (SQL injection, XSS, authentication bypass) during its first weeks.
- **One user (d72sh) prophetically warned** that clearnet forum activity could be traced via subpoena -- exactly the technique the FBI used years later.
- **Traffic grew from ~700 to 6,000+ page views/day** in just three weeks, foreshadowing the explosive growth to come.
- **altoid (Ulbricht) tried and failed to fulfill a drug order**, canceling with the excuse that he "ran into a sketchy situation" -- suggesting he was sourcing locally, not growing as claimed.
- **The admin dismissed GPG encryption as "redundant"** when a vendor required it for shipping addresses, calling Tor's transport encryption sufficient. The plaintext addresses in this database prove him wrong.

## Notes

Personal names and street addresses of private individuals have been redacted throughout. Public figures (Ross Ulbricht, Mark Karpeles, etc.) are named where relevant. Silk Road usernames are preserved as they are pseudonymous handles, not real identities.
