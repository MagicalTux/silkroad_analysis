# Private Messages: Deep Dive

## Overview

Beyond the admin's inbox (covered in report 05), the database contains per-user message tables for all 521 users. The most active inboxes belong to the admin (168 messages), nvram (103), maxvendor (56), 1UP of Canada (46), Goldismoney (35), and Kind Bud/420guy (25). This report covers findings from reading through the largest inboxes.

## The altoid Cancellation

The most historically significant message outside the admin's inbox is in `superduper`'s messages (uid 131). When altoid (Ulbricht's promotional account) canceled superduper's marijuana order, the system sent a cancellation notice, but altoid also sent a personal message:

> "Hey, I'm really sorry but I ran into a sketchy situation trying to get your weed and I can't get it to you. I'm going to cancel your order, and I think you'll just get refunded through Bitcoin. I think there are some people selling hash on here, so maybe you can just get some of that. Sorry again, and good luck"

This is notable because it shows Ulbricht personally attempted to fulfill a drug order through his altoid account and failed. The "sketchy situation" suggests he was trying to source marijuana locally to ship, not growing it himself as the listing claimed ("I grow this stuff myself and I love it").

## The Admin's Security Philosophy vs. 1UP of Canada

A revealing disagreement played out in 1UP of Canada's inbox. 1UP required all customers to GPG-encrypt their shipping addresses. When the admin noticed this, he pushed back:

> "I can understand your concern for keeping addresses private. I share that concern, but there is encryption already built into the system, so I think what you are asking your customers to do is redundant and probably creates unnecessary concern for those that don't understand how to do what you are asking. Because Silk Road is a hidden service, the address never leaves the encrypted tor network..."

The admin asked 1UP to change his messaging from "I recommend you use GPG encryption on the Silk Road" to something seller-specific like "please use GPG encryption when sending me messages or placing orders."

1UP complied but continued to accept only GPG-encrypted addresses. In hindsight, 1UP was right -- the database we're reading now contains plaintext addresses for every buyer who didn't encrypt. The admin's assurances about built-in encryption were either premature or misleading.

## The Admin's MDMA Testing Admission

In a message to user `nexus` (Jan 30, 2011), the admin described the MDMA being sold:

> "The MDMA we offer is a high purity powder. It has not been lab tested, but testing on human subjects has revealed it to be highly potent."

This is one of the earliest messages in the database and reveals that the initial Silk Road inventory included MDMA sold by the admin (or sourced by the admin) that was tested only on humans, not in a lab.

## The maxvendor Reliability Crisis

maxvendor's inbox tells the story of the site's first vendor reliability crisis. Multiple buyers complained about non-delivery:

- `nexus`: "Paid on Monday, would at least expect some confirmation message" (Feb 17)
- A buyer asked if maxvendor was "still around" after reading on the Hidden Wiki that he'd been "MIA" (Mar 6)
- The admin sent a "delivery never arrived" notice and split the refund 50/50

maxvendor eventually returned with this message to the admin:

> "hey, reshipped everybody missing a shipment with 2x the amount plus samples galore, like $100 worth of MDMA :)"

The admin responded warmly: "Well done max! I get your commitment to customer service and am pleased to have you back. I will put in a 'vacation mode' soon for vendors, so you can pause things while you are gone next time."

## Goldismoney's Operational Details

From Goldismoney's inbox:
- Confirmed shipping from the USA (despite selling "synthetic" mescaline, suggesting US-based synthesis)
- When asked by the admin if the mescaline was extracted or synthetic, replied: "My mescaline is synthesis. The purity is guaranteed to be 95% or higher."
- Had a prolonged issue with a Finnish buyer (`S1NGURAMI55`) whose address contained Scandinavian characters that the site's character encoding couldn't handle, causing addresses to arrive blank

## The Finland Connection

User `S1NGURAMI55`'s inbox reveals they were one of the earliest and most active international buyers. The admin personally handled their shipments and revealed:

> "Sorry for the delay. They are being shipped from the US and the post office isn't open Sunday or yesterday because of 'president's day.' This is also the first time I have shipped to Finland so I had to research the best way to do it. They will arrive ground up and vacuum sealed in a flat envelope. I included some extra to make up for the delay."

This confirms the admin was physically going to a US post office and mailing drugs internationally himself.

## pink's Heroin Search

User `pink`'s inbox documents an increasingly desperate search for opiates across the platform:

- Bought prescription stimulants and benzodiazepines from nvram and CREAM
- Posted forum threads begging for heroin vendors
- Received unsolicited offers from strangers:
  - One user (#307) wrote sympathetically: "I am truly sorry to hear about your predicament, friend... I hope to have a material available that I guarantee you will be interested in."
  - Another (#494) offered: "I can sort you out if you want, no worries at all, H is plentiful and cheap round here" and provided an email: `random58949340@cmail.nu`
  - The ALPHABET spam account even targeted them: "do you want H? C? X? GHB? I can do all the letters you want"
- Mentioned being previously prescribed Adderall but cut off by their doctor for "asking for more" and having a past benzo addiction
- Was actively having "H come in from a couple different places" by late March, suggesting they found sources outside Silk Road

## 1UP of Canada's Departure

1UP of Canada's final messages tell a poignant story. After building the most professional cannabis operation on the site, he messaged the admin on March 17:

The admin responded: "Sorry to hear that. I hope everything is ok. If you do come back as a seller, please only confirm shipment AFTER you ship so this doesn't happen again. I will refund those orders... Good luck, and thank you for your contribution here. You helped Silk Road get off the ground :)"

1UP had also been working with `superduper` on becoming a US distributor. superduper had written: "let me be your american distributor so that I can re-sell on this site." 1UP was in the process of setting up vacuum-sealed international shipping when personal circumstances forced his departure.

## Vendor-to-Vendor Communication

The inboxes reveal vendors were communicating with each other:
- maxvendor messaged nexus with a link to buy Indonesian cigarettes online (`indonesia-cigarettes.com`) when nexus asked about sourcing clove cigarettes
- `Obscure` shared their email (`obscure@safe-mail.net`) and PGP key with nexus, along with their pricing for MDMA/2C-B/speed
- Goldismoney and psynom (both major sellers) had exchanged messages about sourcing

## Additional OPSEC Failures Found in Messages

Email addresses leaked in private messages:
- `renwoxing@smtp.ru` -- from the Hong Kong-based methoxetamine seller
- `bockzu@hush.com` -- from the EU marijuana seller  
- `obscure@safe-mail.net` -- from the Canadian MDMA seller
- `random58949340@cmail.nu` -- from an anonymous heroin dealer approaching pink
- `greg.wilson@yandex.ru` -- from a buyer asking maxvendor for a tracking number
- `deepinsidethejungle@hotmail.com` -- from an early inquirer to the admin
- `andhil` -- a buyer who signed their message to gasy2you with what appears to be a real name fragment

Additionally, in the `bcacct` (Bitcoin address) field:
- `blitzop` entered their actual IP address: `213.103.195.84`
- `joeskissonu2` entered `joeskissonu2@lavabit.com` (Lavabit was the encrypted email service later shut down during the Snowden affair)
- Several users entered test strings or "n/a"

## Possible Product Misrepresentation

A buyer left feedback on psynom's LSD blotters:

> "Strong stuff. I think it was actually DOB, lasted much longer than 12 hours."

DOB (2,5-dimethoxy-4-bromoamphetamine) is a psychedelic amphetamine with a much longer duration than LSD. If this assessment was correct, it raises the possibility that some "LSD" sold on early Silk Road was actually a research chemical -- a problem that would plague darknet markets for years.

## Safe or Scam (SoS) Integration

Multiple inboxes show users trading Safe or Scam invite codes -- SoS was an external vendor review site that served as an early trust layer for darknet markets. Users exchanged these codes as social currency:

- pink traded a "The Farmers Market" forum link for a SoS invite
- Multiple users received unsolicited SoS invite codes from established community members
- Vendors were aware of and cared about their SoS reputation

## gasy2you's Ketamine Sourcing Problem

gasy2you (the EU-based LSD/ketamine vendor) canceled their ketamine listing and explained to the admin:

> "I am having trouble sourcing the quality of ketamine I would be happy to sell at that price and computer problems mean I've only just seen and been able to cancel the order. I think I'm also going to redesign [my listings]"

The admin responded: "completely, thank you for exercising caution." This shows that at least some vendors had quality standards and were willing to cancel orders rather than sell subpar product.
