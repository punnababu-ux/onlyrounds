# OnlyRound landing page — context handoff

## What this is
A single-file marketing landing page for **OnlyRound**, an AI voice-interview
platform for recruiters and recruitment firms. File: `Rounds Landing.dc.html`
(Design Component — template + logic class in one file; edit with the DC tools,
not `write_file`).

## Product (source of truth: `uploads/OnlyRound People matters.pdf`)
OnlyRound runs the screening round with voice AI. Candidates apply, scan a QR,
or get called; recruiters get an explainable report and only meet candidates
worth meeting.

- ~500 agentic interviews per day on the platform today.
- Referenceable enterprise logos: **eClerx** and **Digitide** only. No others.
- Audio + video rounds, English + Hindi with live mid-call language switching.
- **Inbound** = candidate opens a web link (shared directly or scanned from a
  QR) and interviews in the browser. **Outbound** = the agent phones the
  candidate from an uploaded list.
- Screening engine: agentic job setup from a JD, two-way reach, custom criteria
  (Must Have / Good To Have / Red Flag, separate fresher and experienced
  tracks), candidate FAQ handling from a client knowledge base.
- Attachable assessment modules: CEFR English (score or hard gate, e.g. B1 on
  Loan Sales), enterprise question banks with randomiser, industry knowledge
  tests, behavioral evaluation, proctoring on video rounds.
- Governance: custom Gen AI reports, candidate CRM timeline, configurable
  re-engagement (retries / channels / cadence), RBAC + multi-tenant,
  governance dashboard with audit trail, credits + self-serve.
- Demo library: 11 live bots (Credit Card Sales En/Hn inbound+outbound, Credit
  Card video, Insurance En/Hn, Loan Sales CEFR gate, Interview Scheduler,
  Mobile Sales Promoter retail, Deep Interview behavioral+proctored).
- Positioning note from the deck: sell it as a replacement for manual
  phone-screen effort and static assessment budget, not new AI spend.

## Decisions made with the user
- Audience: startup founders / hiring managers and recruitment agencies.
- Tone: professional, enterprise-trustworthy. Full-length page.
- Pricing = contact sales (credits + self-serve messaging, no tiers shown).
- ATS names used generically (Greenhouse, Lever, Ashby, Workday, etc.).
- Inspiration: bland.ai, sarvam.ai, decagon.ai — dark, motion-heavy, glassy.
- Real proof points still pending; candidate names/numbers are placeholders.
- Demo bot URLs from the PDF are NOT wired up yet.

## Design system
- Dark by default, light/dark toggle in the nav (persists to
  `localStorage["onlyround-theme"]`). Themes are CSS vars set in JS (`THEMES`).
- Vars: `--bg --ink --mut --line --card --card2 --head --panel --glow1 --glow2
  --shadow --accent(#3EBA8D) --accent2(#7BB9E5) --gold(#FFD975)`.
- Brand mark `assets/logo-mark.svg` (mint/sky/gold gradient) drives the palette.
- Type: Familjen Grotesk (display/body) + IBM Plex Mono (labels, data).
- Inline styles only. Helmet holds `@keyframes` (rise, marq, pulse, drift, spin,
  shimmer, morph, breathe, grow) and body resets — nothing else.
- Motion: ambient blurred glow fields, morphing "AI blob" orbs (not equalizers),
  scroll reveals via IntersectionObserver, marquee, staggered row entrances.

## Page structure (top to bottom)
1. **Nav** — full-bleed sticky bar; links How it works / Reach / Assessment /
   Governance / Pricing; theme toggle; **Log in** CTA.
2. **Hero** (full viewport) — badge "~500 agentic interviews a day"; headline
   "AI interview rounds with <shimmering phrase>"; the phrase and the chips
   below it are driven by the front card of the stack; CTAs Talk to sales +
   See the demo library; "Live in enterprise production · eClerx · Digitide".
   Right: **vertical card stack** of 5 demo bots, auto-advancing, up/down
   arrows, opaque cards with only the front card's content visible. Clicking
   the front card opens a **call modal** (ready → connecting → live, with the
   typed transcript and timer) — a UI shell, not a real agent connection.
3. **How it works** — "Automation of the hiring process." Four selectable steps
   (Create the job / Add the assessments / Interview candidates / Review and
   decide) with icons and an auto-advance progress bar, driving a live panel on
   the right (desc + four data rows + note). Below 760px the steps become a
   swipeable snap carousel (`mobile` flag from a resize listener).
4. **Two ways in** (`#reach`) — two equal cards: Inbound (real QR + shareable
   link + 3 points) and Outbound (live dial queue + 3 points), plus a shared
   facts strip (languages, FAQ, 24/7, audio or video).
5. **Assessment modules** — five cards (CEFR, question banks, industry tests,
   behavioral, proctoring).
6. **Explainable reports** — evaluation card with Must Have / Good To Have /
   Red Flag rows and evidence, beside the narrative.
7. **Demo library** — table of all 11 bots (language, mode, flow, proves);
   horizontally scrollable, min-width 760px.
8. **Built for enterprise** — six tagged governance capabilities beside a
   candidate audit-trail timeline.
9. **Integrations** — ATS marquee.
10. **Pricing** — credits + contact sales. 11. **FAQ** accordion.
12. **Closing CTA** + footer.

## Implementation notes
- Logic class constants: `SCRIPT` (transcript lines), `STEPS`, `PANELS`,
  `THEMES`; `CARDS` (hero deck, each with `hero` phrase, `tags`, orb gradients)
  lives inside `renderVals()`.
- State: `li/ch` typing, `secs`, `open` (FAQ), `idx` (deck), `theme`, `call`,
  `phase`, `callSecs`, `how`, `howTick`, `vw`.
- Responsiveness is done with `repeat(auto-fit, minmax(min(100%,Npx),1fr))`
  grids plus a JS `mobile` flag (<760px) — there are no media queries, because
  the DC format allows inline styles only.
- The QR is rendered at runtime into `#or-qr` from a CDN QR library
  (cdnjs qrcodejs), encoding `https://onlyround.ai/i/credit-card-sales`, with a
  plain "QR" fallback tile if the script is blocked. Replace the URL with a
  real interview link. jsDelivr was blocked in this environment.
- Tweakable props: `theme` (dark/light), `accent` (color), `typingSpeed`
  (range, default 34), `reduceMotion` (boolean).

## Open items
- Wire the 11 demo bot interview/dashboard links (PDF has them) to the hero
  cards, the demo table rows and the modal.
- Replace placeholder metrics/candidate names with real ones.
- Connect the call modal to the live agent endpoint.
- Confirm which ATS integrations are genuinely live before publishing.
