# Security & OPSEC Analysis

## The Admin's OPSEC

### What He Got Right
- Operated as a Tor hidden service (`.onion`)
- Used Bitcoin for payments
- Implemented an escrow system
- Claimed addresses were "encrypted in the database"
- Did not use HTTPS (correctly noting it was redundant over Tor)

### What He Got Wrong

1. **The "altoid" connection**: User `altoid` (UID 2) was used to promote Silk Road on clearnet forums (Bitcoin Talk, Shroomery). The FBI later linked these forum posts to Ulbricht's real identity. The fact that altoid is the second account ever created on Silk Road -- immediately after the admin -- made this connection even more damning.

2. **The `silkroadmarket.org` domain**: The admin announced this clearnet gateway in the forum on March 1, 2011. The domain was purchased from KalyHost.com (a hosting service run by Mark Karpeles, later known for Mt. Gox) using a fake name and paid with Bitcoin. A user (#293) warned about the WHOIS records: "whats up with having info in whois record? ur talk in the forums + whois record seems like plausible id." While the registration used a fake identity, the mere existence of a clearnet domain associated with Silk Road created an additional attack surface.

3. **Uploading the database to a third-party host**: This very database snapshot exists because Ulbricht uploaded a copy of the Silk Road MySQL database to KalyHost's server -- the same hosting provider where `silkroadmarket.org` was registered. The purpose of this upload is unknown, but it represents a catastrophic OPSEC failure: the entire database including plaintext shipping addresses, transaction records, and private messages was placed on infrastructure he did not fully control.

4. **Geographic self-identification**: In private messages, the admin revealed he shipped from the US and was from Texas. nvram noted: "Fuckin' A. I'm from Texas too." The admin's shroom listings specified "ship_from: US."

5. **Coding the site himself**: The admin confirmed to nvram that he built the entire PHP system. The amateur quality of the code (all varchar fields, per-user message tables, SQL injection vulnerabilities) is consistent with a self-taught programmer working alone.

6. **Being both admin and top seller**: The Silk Road admin account was both the marketplace operator AND the #1 seller by transaction volume. If any transaction were traced, it would lead directly to the person running the entire operation.

7. **Plaintext addresses in the database**: Despite claims of encryption, the database contains readable shipping addresses. Either encryption was not implemented, was reversible by the server, or the snapshot predates the encryption feature.

8. **The SQL injection/XSS period**: The admin posted in the forum (Mar 3): "After adding some measures to prevent SQL injection attacks and XXS attacks, we produced an error in the checkout page." This suggests the site ran without basic input sanitization for its first ~7 weeks.

## User OPSEC

### Failures

1. **Real names and addresses**: The vast majority of buyers provided real names and home addresses. Only ~5 out of 136 transactions used PGP-encrypted addresses.

2. **Email addresses in profiles**: Users `NorthernSoul` and `Phoenix26` put clearnet email addresses in their Bitcoin address field. PGP keys posted in profiles sometimes contained real email addresses.

3. **Password in plaintext PM**: Goldismoney revealed their account password in a message to the admin.

4. **Reuse of addresses**: Multiple repeat buyers used the same name and address across transactions, making correlation trivial.

5. **Real names with minimal obfuscation**: Most users didn't even use fake names. Names like "[redacted]" (nvram), "[redacted]" (420guy), and "[redacted]" (Polarys) appear to be real.

6. **Using clearnet services**: A user mentioned accessing bitcoin.org forums from clearnet, and another warned about the implications.

### Successes

1. **PGP adoption by some users**: 1UP of Canada, sillysally, xcentrix, ttd, d72sh, and jibberish encrypted their shipping addresses with PGP.

2. **Use of Poste Restante**: Finnish user S1NGURAMI55 had items shipped to "Poste Restante" (general delivery) rather than a home address.

3. **Fake names**: Some users clearly used aliases (e.g., "Mr. Palida," "Smaz Galord," "Fu Inc.").

4. **PO Boxes**: A few users (420guy, mrf1911) used PO boxes rather than residential addresses.

5. **1UP of Canada's advocacy**: His detailed forum post on GPG encryption was the most articulate security guide on the site.

## The d72sh Warning

User `d72sh` sent the most security-conscious message in the entire database (Mar 8):
> "i hope you have not accessed the bitcoin.org forums on clearnet; as it is possible to tie your identity there (and everything posted in your silk road thread) to this site. a subpoena will reveal the IP's from which your account has logged into bitcoin.org/smf."

This was exactly the investigative technique that ultimately led to Ulbricht's arrest. The user who wrote this warning understood the threat model better than the site's creator.

## Technical Vulnerabilities (Reported)

1. **Authentication bypass** (Feb 22): Visiting `/messages.php` while logged out showed another user's inbox
2. **HTML injection/XSS** (Feb 28): All input fields vulnerable; nvram reported this
3. **SQL injection** (pre-Mar 3): The admin acknowledged fixing these
4. **PHP errors exposed** (Mar 2): MySQL connection strings and file paths leaked in error messages (`/var/www/include/functions.php`, line 3)
5. **Special character handling** (Mar 8): Scandinavian characters caused messages to arrive blank
6. **No HTTPS for .onion**: While the admin correctly noted Tor provides transport encryption, the lack of HTTPS meant there was no server authentication -- a malicious exit node or Tor circuit compromise could have intercepted traffic (though this is less of an issue for hidden services)

## Bitcoin Traceability

The `variables` table shows a single BTC exchange rate, suggesting the system did not use per-transaction Bitcoin addresses or any form of coin mixing. User `cidtastic` raised this concern in the forum (Mar 2):
> "blockexplorer.com: You can view people's transaction history"

Users discussed early Bitcoin tumbling services, and the admin later implemented a built-in tumbler -- but this snapshot predates that feature. User `muaddib` even listed a manual Bitcoin mixing service as a product (Item 149, "Clean Coin Exchange").

## Summary

This snapshot captures a marketplace with fundamental security weaknesses at every level:
- The admin leaked his own identity through promotional activities
- The codebase had textbook web vulnerabilities
- Addresses were stored in a recoverable format
- Most users made zero effort to protect their identity
- Bitcoin transactions were fully traceable
- The admin was simultaneously the biggest vendor, creating maximum legal exposure

The few users who understood operational security (d72sh, 1UP of Canada, sillysally) were outliers in a community that largely trusted the platform's anonymity without verification.
