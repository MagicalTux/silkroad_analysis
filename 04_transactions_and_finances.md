# Transactions & Financial Analysis

## Transaction Overview

| Metric | Value |
|--------|-------|
| Total transactions | 136 |
| Total BTC transacted | 5,464.99 BTC |
| USD equivalent (at $0.76/BTC) | ~$4,153 |
| Finalized (completed) | 77 (57%) |
| Canceled | 20 (15%) |
| Confirmed delivered | 46 (34%) |
| Reported non-delivery | 4 (3%) |
| Still pending at snapshot | 39 (29%) |

At the time, 5,465 BTC was worth approximately $4,153. At Bitcoin's all-time high (~$69,000 in Nov 2021), those same coins would have been worth ~$377 million.

## Revenue by Seller

| Seller | Orders | BTC Revenue | ~USD |
|--------|--------|-------------|------|
| Silk Road (admin) | 41 | 1,253.67 | $954 |
| maxvendor | 15 | 880.00 | $670 |
| psynom | 15 | 626.66 | $477 |
| Goldismoney | 18 | 575.00 | $438 |
| 1UP of Canada | 7 | 552.00 | $420 |
| gasy2you | 2 | 410.00 | $312 |
| P4r4b0l4 | 12 | 350.00 | $266 |
| ecstatic | 2 | 200.00 | $152 |
| afuzzyfelling | 2 | 150.00 | $114 |
| BockZu | 1 | 100.00 | $76 |
| muaddib | 2 | 99.96 | $76 |
| nvram | 11 | 55.50 | $42 |
| altoid | 1 | 50.00 | $38 |
| UK420 | 2 | 45.00 | $34 |
| hookups | 1 | 40.00 | $30 |
| Fractal | 1 | 25.00 | $19 |
| MONkey | 1 | 24.20 | $18 |
| AlterEgo | 1 | 20.00 | $15 |
| purechem | 1 | 8.00 | $6 |

The admin account (Silk Road) was responsible for **30% of all orders** and **23% of total revenue**, making the site operator also its biggest vendor.

## Transaction Timeline

- **First transaction:** February 6, 2011 (user `stayinalive` buying 5g shrooms from Silk Road for 57.67 BTC)
- **Last transaction in snapshot:** March 21, 2011

The first actual sale on the entire platform was a mushroom purchase from the admin. This buyer shipped to: "[redacted name and address], Providence, RI."

## The Free Shroom Campaign

A significant portion of Silk Road's 41 orders (at least 15) were the **free 1-gram mushroom samples**. This was a deliberate strategy to onboard new buyers and build trust. The admin listed item #20: "For a limited time only, we are offering 1 gram FOR FREE so you can try out a purchase on Silk Road before committing to a larger order."

These free samples went to addresses across the US, Canada, and Finland.

## Escrow System

The transaction table reveals the escrow workflow:
1. **Order placed** (`date` field)
2. **Payment verified** (`verified = 1`)
3. **Seller ships** (`shipped = 1`, `ship_date`)
4. **Buyer confirms delivery** (`delivered = 1`) or reports non-delivery (`no_delivery = 1`)
5. **Transaction finalized** (`finalized = 1`) -- funds released to seller
6. **Or canceled** (`canceled = 1`) -- refund to buyer

The `bc_addr` field was almost always empty, suggesting the escrow used internal account balances rather than per-transaction Bitcoin addresses (with one exception: transaction 156 shows address `1GcBwBFTstshhmcwdMdBLT5PMUtrsZK5ED` -- a test by the admin to "123 fake st").

## Shipping Addresses: A Major OPSEC Disaster

**The most striking finding in this database is that shipping addresses were stored in plaintext.** Despite forum discussions about encryption and the admin's claim that addresses were "re-encrypted and stored in the database," the transaction records contain fully readable names and addresses.

This means this database copy contains the **real names and home addresses** of early Silk Road buyers. Examples:

- Buyers in the US: Providence RI, Houston TX, Seattle WA, Atlanta GA, Austin TX, Boston MA, etc.
- International buyers: Helsinki/Lahti Finland, Moscow Russia, Reykjavik Iceland, Mannheim Germany, Visby Sweden, Glasgow Scotland, Benevento Italy, Melbourne Australia, Lille France, etc.

A few security-conscious users encrypted their addresses with PGP before submission (visible as `-----BEGIN PGP MESSAGE-----` blocks in the address field), but they were a small minority (~5 out of 136 transactions).

## Notable Transaction Details

### The altoid Transaction (#62)
Ross Ulbricht's presumed account `altoid` had exactly one sale: 1/4 oz homegrown marijuana to `superduper` for 50 BTC. Shipped to "[redacted name and address], Atlanta, GA." This transaction was marked verified but NOT shipped, then finalized and canceled -- suggesting it may never have been completed.

### Repeat Buyers
Several users ordered multiple times:
- `nvram`: 3 orders (shrooms from Silk Road, LSD from P4r4b0l4)
- `S1NGURAMI55`: 4 orders (shrooms + mescaline), all to addresses in Lahti, Finland
- `420guy`: 3 orders to "[redacted name and address], North Canton, OH"
- `superduper`: 2 orders to the same Atlanta apartment
- `nexus`: 3 orders using [redacted name] at two Florida addresses
- `Polarys`: 3 orders to "[redacted name and address], Visby, Sweden"

### International Reach
Despite the site's tiny size, transactions involved addresses in:
USA, Canada, Finland, Russia, Germany, Sweden, UK (Scotland, England), Iceland, Italy, France, Austria, Ireland, Australia

### Non-Delivery Cases
Only 4 transactions were flagged as non-delivery:
- Two of maxvendor's MDMA shipments to Finland (bomber, sillysally)
- One Silk Road shroom shipment (ogre86 in Spokane, WA)
- One gasy2you LSD shipment (interested_party in Helsinki)

The Finland addresses were heavily represented in non-delivery -- customs may have been intercepting international drug shipments.
