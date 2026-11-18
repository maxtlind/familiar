# Site builder brief

Working name: [name TBD]. Part of Belleview Group.

## The idea

A website builder for people on Apple devices. Updating your site should feel like writing in Apple Notes. You type, the app handles the design, and Publish pushes it live.

It's a native app for iPhone, iPad and Mac. Content syncs across devices through iCloud. Price target: $5/month or less.

## Why now

The old site builders are drifting away from small, simple sites. Webflow is going upmarket, Framer is aimed at designers, and Squarespace is getting heavier. AI site generators make a first draft fast, but they don't help anyone keep a site tidy a year later. That second part is the gap.

## First audience

Small associations, guilds and nonprofits. The reference case is the Iowa Brewers Guild's i-BEST site (iabrewersconference.org), which runs on Squarespace today.

What's true about these sites:
- They're run by volunteers who change over every year or two.
- The person updating the site is usually on their phone.
- The site is a brochure plus a few links out (tickets on Eventbrite, payments elsewhere).
- They drift: empty placeholder pages, events that already happened, the same thing named four different ways, headings used for layout, stale share images.

What visitors come for:
1. What is this group?
2. When's the next event, and how do I get a ticket?
3. How do I join, sponsor or donate?
4. Who runs it?
5. How do I reach them?

## Product principles

1. **Content types, not layouts.** People fill in fields. The system decides how it looks.
2. **Three look settings, nothing else.** Type (Clean sans or Classic serif), width (Narrow or Wide), accent color. Same idea as Notion's page settings.
3. **A quiet editor.** The app notices drift and suggests fixes. It never changes the live site without a Publish.
4. **Audience starters are packaging.** "Association," "Nonprofit," "Church" and "Club" are presets that pick and relabel the same content types. One system to maintain.
5. **Link out, don't rebuild.** Ticketing, payments and member logins stay with the tools people already use.

## Content types (v1)

| Type | Fields | Notes |
|---|---|---|
| Event | name, date, time, place, ticket link, note | Moves to Past events the day after. "Start next year's" copies it. |
| Person | photo, name, role, organization, bio | Board, staff, speakers. Starters relabel the section. |
| Partner | logo, name, tier, link | Tiers group and size themselves. |
| Update | headline, date, body, optional photo | Newest three show on Home. |
| Resource | file, name | File type and size show automatically. |
| Question | question, answer | FAQ hides itself when empty. |
| Membership | tier name, price, what's included, join link | Links out for payment. |
| Contact | email, address, social links | Footer plus Contact section. |

Pages (Home, About) are free-form notes that can embed any of the types above through an Insert menu.

## Tidy up (the quiet editor)

Starting checks, from the i-BEST site:
- An event's date has passed. Offer to archive it and start next year's.
- The same name is spelled several ways. Offer to pick one.
- A section is empty. Hide it from the menu until it has content.
- The share image is old. Ask for a new one.
- Photos have no description. Ask for one line each.

Some of these are simple rules. The naming check and the descriptions are a good place for on-device AI.

## App screens (v1)

1. Pick a starter and name the site
2. Site home: sections, Tidy up card, Look, Publish
3. Edit an event
4. Write a page like a note, with an Insert menu for content types
5. Tidy up
6. Look sheet: type, width, accent
7. Publish sheet: list of changes, then live in seconds, with undo through History

## Architecture sketch

- **App**: SwiftUI multiplatform (iOS, iPadOS, macOS). SwiftData models for each content type, synced with CloudKit.
- **Publish**: the app sends the site's content as JSON to a Cloudflare Worker.
- **Site**: the Worker renders pages from the template using that content and stores published versions in R2 so undo is easy. No build step, so publishing feels instant.
- **Domains**: a free subdomain by default, plus custom domains through Cloudflare's custom hostnames. This has to be close to automatic, because domain help is the biggest support cost.
- **Accounts and billing**: Sign in with Apple and a StoreKit subscription.

Open to change once we prototype. This route is close to the Astro and Cloudflare Workers setup already planned for Belleview web work.

## Risks to keep in view

- **Price isn't the pitch.** Carrd costs $9 to $19 a year. The reason to switch has to be "update from my phone, and it always looks right."
- **Support is the real cost.** At $5/month, one long support thread can wipe out a year of revenue from that customer. Domains, handoffs between volunteers and billing need to work without help.
- **App Store fees.** Apple takes 15% under the Small Business Program.
- **Hosting is the product.** Apple's iWeb died partly because publishing was tied to a hosting service that shut down. Publishing and hosting have to be rock solid.
- **Distribution.** These groups aren't shopping for a site builder. Early growth is word of mouth through real organizations Max knows.

## Out of scope for v1

Ticketing, payments, member logins, blogs with comments, ecommerce, restaurants and shops.

## Open questions

- Product name.
- Handoff: how a volunteer passes the site to the next person.
- Multiple editors on one site, and what happens when two people edit at once.
- Migration: can we pull in an existing Squarespace site's content?
- Who are the first three organizations to try it?

## Design

- App screens: https://claude.ai/artifact/B5mRbrNuy6Rx2VE3cosPFZ
- Website system and content types: https://claude.ai/artifact/K44Q1pMFJr7i2dqsSyzvFS

Both use BelleviewOS. The website's serif option and the Narrow width are customer settings, not Belleview tokens.
