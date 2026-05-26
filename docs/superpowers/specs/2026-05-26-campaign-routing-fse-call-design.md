# Kinetic Age panel — campaign routing + split Sales/FSE call flows

Date: 2026-05-26

## Goal
Rework the admin panel so leads from different campaigns land in the right
section, the AI call lives only in **Sales**, and **FSE** gets a simplified,
AI-free call flow.

## How leads arrive (decided on the website, before the panel — not built here)
| Campaign | Condition | Lands in | FSE call type |
|---|---|---|---|
| Outside BLR | books FSE slot on site | FSE | `outside` (online) |
| Inside BLR | address + offline ₹99 trial | FSE | `offline-trial` — offline trial booked, **FSE conversion call scheduled at end of session** (→ offline subscription); sales call skipped |
| Inside BLR | online trial + slot | FSE | `online-trial` |
| Inside BLR | phone only, no address | Sales | — (AI sales call) |

## Sections (2)
- **Sales** (renamed from "Leads"): lead cards show **name + phone only**.
  "Start Sales Call" opens the existing **AI cockpit** (unchanged). After the
  call, the existing qualify → "Move to FSE" path still works.
- **FSE**: simplified, no AI. Panel grouped into *Outside Bangalore*,
  *Inside BLR · Online Trial*, *Inside BLR · Offline Trial*.

## FSE card
- Collapsed: name, phone, campaign name, time booked for.
- Expanded: full info (booking-for, age/gender, location/address, pain points,
  goals, physio, best time) + offline-trial conversion-call note + **Start Call**.

## FSE call (new full-screen view, no AI)
- Top bar: name, phone · campaign, rec timer, End Call.
- **Write PPT** → opens an auto-generated briefing deck built from the client's
  info (Cover · Profile · Pain points & conditions · Goals · Recommended plan &
  talking points · Trial→conversion path) for the FSE to refer to.
- Free-text **notes** block.
- **Label 1 / Label 2 / Label 3** to mark the client profile.
- End Call saves label + notes, marks the call done.
- Removed: AI prompter/feed, AI summaries, conversion-% blocks, the old guided
  "assessment cockpit".

## Data model
Single `LEADS` array; each lead gets `pool` ('sales'|'fse'), `campaignType`
('inside-blr'|'outside-blr'), `campaignName`, and for FSE leads `fseType`,
`bookedTime`, `address`, plus `trialSession`/`conversionCall` for offline-trial.
`isBLR(d)` switches to `campaignType === 'inside-blr'`. Alerts/Weekly Summary
operate on the sales pool.
