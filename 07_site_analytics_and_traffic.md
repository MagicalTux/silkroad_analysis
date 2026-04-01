# Site Analytics & Traffic Patterns

## Data Source

The `stats` table logged every page view from February 15 to March 21, 2011, recording:
- Unix timestamp
- Current page URL
- Previous page (referrer within site)
- User ID (if logged in)

Total recorded page views: **92,449**

## Daily Traffic

| Date | Page Views | Notable Events |
|------|-----------|----------------|
| Feb 15 | 182 | Stats tracking begins |
| Feb 16 | 932 | |
| Feb 17 | 976 | |
| Feb 18 | 295 | Dip |
| Feb 19 | 738 | |
| Feb 20 | 858 | |
| Feb 21 | 951 | |
| Feb 22-28 | 566-891/day | Steady ~700 avg |
| **Mar 1** | **2,404** | Inflection point -- traffic triples |
| Mar 2 | 3,643 | |
| Mar 3 | 3,746 | |
| Mar 9 | 4,002 | |
| Mar 10 | 4,698 | |
| Mar 14 | 4,995 | |
| Mar 18 | 5,992 | |
| **Mar 20** | **6,213** | Peak traffic day |
| Mar 21 | 4,519 | Snapshot ends |

Traffic grew from ~700 views/day in late February to **6,000+ views/day** by March 20 -- nearly a 10x increase in three weeks.

The jump around March 1 correlates with the admin's creation of `silkroadmarket.org` as a clearnet portal, and likely with mentions on Bitcoin forums.

## Most Visited Pages

| Page | Views | % of Total |
|------|-------|-----------|
| `/index.php` (homepage) | 19,037 | 20.6% |
| `/category.php?uid=10` (Other) | 4,333 | 4.7% |
| `/category.php?uid=1` (Marijuana) | 3,838 | 4.2% |
| `/category.php?uid=7` (LSD) | 3,584 | 3.9% |
| `/forums.php` | 3,582 | 3.9% |
| `/messages.php` | 3,507 | 3.8% |
| `/category.php?uid=9` (Prescription) | 2,634 | 2.9% |
| `/category.php?uid=6` (Ecstasy) | 2,414 | 2.6% |
| `/forum_topic.php?topic=4` (Silk Road forum) | 2,330 | 2.5% |
| `/category.php?uid=5` (Shrooms) | 1,966 | 2.1% |
| `/my_account.php` | 1,772 | 1.9% |
| `/message.php` | 1,635 | 1.8% |
| `/about.php` | 1,389 | 1.5% |
| `/instructions.php` | 1,331 | 1.4% |
| `/forum_topic.php?topic=6` (Product requests) | 1,323 | 1.4% |
| `/category.php?uid=12` (DMT) | 1,235 | 1.3% |
| `/forum_topic.php?topic=2` (Shipping) | 997 | 1.1% |
| `/buy.php` | 955 | 1.0% |
| `/register.php` | 792 | 0.9% |
| `/guidelines.php` | 774 | 0.8% |

Key observations:
- The homepage dominated with 20% of all traffic
- Category browsing was the primary activity
- Forums were almost as popular as product categories
- `/register.php` had 792 views but only ~350 registrations in this period, suggesting a ~44% conversion rate
- `/buy.php` had 955 views but only ~100 orders, suggesting most browsing was speculative

## Most Active Users by Page Views

| User | Page Views | Role |
|------|-----------|------|
| nvram | 2,745 | Seller/buyer, power user |
| psynom | 2,726 | EU-based LSD seller |
| ttd | 1,572 | Active community member |
| 1UP of Canada | 1,162 | Canadian cannabis seller |
| pink | 965 | Buyer, forum regular |
| Makai | 927 | Security researcher, buyer |
| MONkey | 758 | Prescription seller |
| 420guy | 723 | Buyer |
| cidtastic | 665 | Early adopter, skeptic |
| Roxxo | 631 | DMT seller |
| nexus | 616 | Buyer |
| CREAM | 589 | Prescription seller |
| eshen | 574 | Buyer |
| silky420 | 565 | Buyer |
| P4r4b0l4 | 565 | LSD/seeds seller |
| muaddib | 540 | Cannabis seller |
| renwoxing | 487 | MXE seller from Hong Kong |
| Goldismoney | 474 | Mescaline seller |
| k1ngk0ng | 439 | Buyer |
| benerhous | 430 | Buyer |

The top two users (nvram and psynom) each generated nearly 3% of all site traffic on their own. The top 20 users accounted for ~18,000 page views (19.5% of total traffic).

## User Behavior Patterns

Based on the stats data:
- The site was clearly browsing-heavy: ratio of page views to transactions was roughly 680:1
- The forum launch (Feb 26) correlated with increased engagement
- Many users visited the site repeatedly without purchasing -- "window shopping" on a darknet market
- The `/about.php` and `/instructions.php` pages getting significant traffic suggests many newcomers needed help understanding how the site worked
