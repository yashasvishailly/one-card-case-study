# The One Card

**One scan. Every way to reach you.**

A free contact-sharing tool from The One Labs. Add your details, watch a phone-style contact preview update, and generate a QR card or a downloadable contact file.

[Create your card](https://yashasvishailly.com/one-card/) · [The One Labs products](https://yashasvishailly.com/products/)

<p align="center">
  <img src="./assets/phone-preview.png" width="42%" alt="One Card phone preview with fictional Jamie Rivera contact details and a QR">
  <img src="./assets/contact-card.png" width="49%" alt="One Card alternate contact-card view with the same fictional details">
</p>

*Local browser captures of the implemented interface using fictional example data. No real subscriber information is shown. Contact imports look different across devices.*

## Why I built it

Sharing contact details often means sending a phone number, then an email, then a LinkedIn profile. The One Card puts those ways to reach someone into one contact that can be saved.

The product should be useful in a single visit. No app installation, account, or hosted profile is needed.

## What I built

- A contact editor with a live phone-style preview and an alternate card view.
- Name, role, company, email, international phone and WhatsApp numbers, website, social profiles, note, and optional photo.
- Social usernames that become full profile links, while still accepting pasted URLs.
- A built-in + prefix that accepts phone numbers pasted with or without it.
- A QR containing the contact details directly, plus a downloadable .vcf contact file.
- A shareable QR design showing the contact's name and the credit **by @yashasvishailly**.
- Responsive layouts using the existing website's typography and colour palette.
- Email capture with explicit consent, stored in Google Sheets through a separate backend.
- GA4 and PostHog events for product usage, with card content excluded from event properties.

Email and agreement to the stated follow-up consent are required to generate a card. The email comes from the card itself; there is no second signup field.

## The decisions that shaped it

| Decision | Reason | Trade-off |
| --- | --- | --- |
| Keep the card in browser memory | Avoid accounts and persistent profiles for a single-use tool | The creator must download before leaving |
| Encode contact details directly in the QR | A saved QR does not need a hosted profile page to provide its contact payload | Edits require a new QR; previously shared files cannot be recalled |
| Show a phone-style preview while typing | Make the result visible before generation | It is illustrative, not an exact preview of every contacts app |
| Accept social usernames | Remove repeated URL typing | A username must still belong to the correct profile |
| Keep photos in the contact file | Preserve a useful photo option without overcrowding the QR | QR imports do not include the photo |
| Store a limited subscriber record | Let a free tool support consent-based follow-up | Email collection must be explained separately from card storage |

## Data and consent

The card is assembled in the browser. There is no stored card profile, account database, or KV card store.

The subscriber record contains the email, optional website, source tool, consent status and version, first subscription time, latest consent time, and subscription status. It does not contain the card's name, phone, WhatsApp, photo, social profiles, or notes.

The form explains consent for exclusive launches or content and links to the [privacy policy](https://yashasvishailly.com/legal/#privacy). The backend validates the request, and the sheet deduplicates by email.

The QR and downloaded contact file intentionally contain the details the creator chose to share. Anyone receiving those files can read and keep them.

## Measuring the product

Implemented events cover visits, starts, generation attempts and outcomes, validation failures, QR/contact downloads, email-save outcomes, photo actions, and link types.

Card contents are excluded from analytics properties. One Card disables session recording and autocapture, and respects Do Not Track and Global Privacy Control. The PostHog identifier is temporary for the visit. GA4 uses its own pseudonymous measurement.

A direct-contact QR cannot report an offline scan. Download events are not evidence that a recipient scanned or saved the contact.

## What changed during the build

The first local prototype used a stored card and a stable recipient URL. The live product moved to a simpler model: generate in the browser, download, and leave.

The interface then moved from a static card preview to a contact screen that updates with each field. Testing and feedback led to visible social links, support for usernames, international phone entry, neutral placeholders, a larger product name, and a QR shown inside the phone preview.

## Validation and current limits

As of 29 September 2026, the creator confirmed successful QR scans on Android and iOS. Automated local browser checks covered layouts from 320px to 2560px, both preview modes, long content, number paste behaviour, decoded QR payloads, and downloaded contact values.

These checks are not a claim of exhaustive testing on every device. Contacts apps control the final import experience. Very large contact payloads can exceed the QR limit; the contact-file download remains the fallback. Editing a generated card invalidates its previous downloads until it is generated again.

Analytics code and local event behaviour have been checked. Production event arrival in the GA4 and PostHog dashboards still needs a live check. This case study makes no claims about adoption, conversion, or revenue.

## What I learned

A live preview can explain a product more clearly than another paragraph of copy. The most useful improvements came from ordinary actions: pasting a number, entering a username, trying a small screen, and seeing what a recipient actually receives.

Keeping cards temporary also made the data boundary easier to explain. Contact generation, subscriber collection, and product analytics each have a different purpose and should collect only what that purpose needs.

## About this case study

These pages describe the live product, its visual direction, and its system boundaries. See [Visual product notes](./VISUAL_PRODUCT.md) and [Architecture](./ARCHITECTURE.md).

This repository contains documentation and synthetic screenshots only. Production application code, subscriber records, credentials, and deployment secrets are excluded.

## Built by

[Yashasvi Shailly](https://yashasvishailly.com), under The One Labs. Product, design, implementation, and testing.
