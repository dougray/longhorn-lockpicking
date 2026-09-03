# Longhorn Lockpicking Club

One-page website for the Longhorn Lockpicking Club — Austin, Texas.
Chartered 2006 at UT Austin; a chapter of Locksport International.

**Live site:** https://dougray.github.io/longhorn-lockpicking/

## Structure

Single self-contained `index.html` — all CSS inline, no build step, no framework.
The only external requests are one Google Font (Oswald) and the OpenStreetMap
embed in the "When & Where" section.

## The calendar

Two data files drive the Calendar section. They are loaded with `<script src>`
rather than `fetch()` on purpose: a fetch of JSON fails under `file://`, which
would make the calendar look broken when you open `index.html` locally.

| File | Who maintains it |
|---|---|
| `data/meetings.js` | **Generated.** Do not hand-edit. |
| `data/conferences.js` | **Yours.** Nothing overwrites it. |

`data/meetings.js` is refreshed from the club's public Meetup iCal feed by
`scripts/update_meetings.py`, run daily by `.github/workflows/update-meetings.yml`.
It commits only when the dates actually change. You can also trigger it by hand
from the repo's Actions tab, or run it locally:

```
python3 scripts/update_meetings.py
```

`data/conferences.js` is a hand-maintained list of Texas security conferences.
The file header documents every field. Entries with a `start` date sort
chronologically and drop off the page once past; entries with only a `when`
string collect at the bottom under "Dates not yet announced".

## Assets

- `assets/logo.jpg` — the club logo, taken from the Instagram avatar. **150×150
  is the largest copy available anywhere public**; the original artwork is with a
  member who is currently dormant. If a high-resolution or vector version ever
  turns up, replace this file and regenerate the icon below — the footer logo and
  favicon are both soft because of this limit.
- `assets/apple-touch-icon.png` — 180×180, the horned-keyhole mark cropped clear
  of the wordmark so it stays legible at favicon sizes. Regenerate with:

```
sips -s format png -c 78 122 --cropOffset 19 14 assets/logo.jpg --out /tmp/m1.png
sips -p 122 122 --padColor FFFFFF /tmp/m1.png --out /tmp/m2.png
sips -Z 180 /tmp/m2.png --out assets/apple-touch-icon.png
```

Brand colours are sampled from the logo: orange `#C96A2B`, slate `#2B333C`.
