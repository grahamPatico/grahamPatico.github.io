# REQ-PORTFOLIO-01: Portfolio maintenance

Task: TRI-218. Exit impact: none (requested personal-site maintenance).
Baseline: 8227ac3. Scope: grahamPatico/grahamPatico.github.io only.

## Intent

Help a recruiter, investor or engineer understand Graham's hardware and software work within ten seconds, then explore it. Preserve the static site and existing datasheet identity. Graham merges the PR; never push to main.

## Acceptance criteria

- Audit Vercel and GitHub Pages before changes at 1440px and 390px; capture hero, selected work, build log, about and contact. Rank findings before implementation.
- Tighten the hero using existing facts; retain the six-layer stack and improve mobile density without hiding the layer controls.
- Preserve real filter buttons and aria-pressed. Support keyboard focus after a hero jump and clearing an empty result. Provide a skip link, clear focus and reduced motion.
- Use appropriately sized compressed images, intrinsic dimensions, lazy loading below the fold and responsive sources that update with each screen switch.
- Remove the external font stylesheet bottleneck while retaining IBM Plex typography and its license.
- Provide a descriptive title and a dedicated public-safe 1200 by 630 social preview, with canonical and image metadata pointing to the primary Vercel URL.
- Maintain readable layout and no horizontal overflow at 320, 390, 768 and 1440px. Improve card alignment and small-screen build-log hierarchy.
- Preserve grahampatterson14@gmail.com; use no em dashes in visitor copy. No new phone numbers, OcuTrap fleet counts, customer names, pricing, fundraising or modem/part numbers. Existing screenshots are approved by Graham. Golf project remains imaging only.
- Record mobile Lighthouse before/after with methodology and limitations. Check console errors, image switches, filters, reduced motion, internal targets and external HTTP links. Report blocked links honestly.
- Leave missing dates, inferred layer tags, vague descriptions, OcuGate images and proposed additions as questions. Do not invent facts or add sections/frameworks/domains.
- Deliver one PR with ranked findings, before/after scores, screenshots and questions. Exclude secrets and local environment files.

## Ranked baseline findings (before implementation)

1. **Image review and preview:** existing OcuTrap UI images contain fleet counts and device labels. Graham reviewed the concern during this audit and confirmed the existing screenshots are fine. Retain these approved images; add no new sensitive content. Use a typographic social preview for clearer personal identity.
2. **First impression on mobile:** decorative plates and the parts list stack vertically, pushing selected work below approximately 1,300px. Copy says founder/engineer but can state hardware and software directly; a visible work jump makes the next action clear.
3. **Performance:** first Vercel Lighthouse mobile run is 82/100/100/100, FCP 3.1s, LCP 3.9s. Google Fonts CSS blocks rendering; JPEGs have no responsive variants. Preserve typography with local fonts and optimize images. Existing intrinsic dimensions and lazy loading are mostly good; no measured horizontal overflow or console errors.
4. **Mobile hierarchy:** at 320px the build-log title competes with year, revision and right-hand link, wrapping names into narrow columns. Section headings also wrap awkwardly. About paragraphs lack separation; paired card actions do not align consistently.
5. **Keyboard navigation:** native filter/screen buttons, pressed states, alt text and focus outlines already exist. Hero jumps scroll without transferring focus; clearing empty filters hides the focused button. Add deliberate focus destinations and a skip link. Disable transitions as well as initial motion for reduced-motion users.
6. **SEO and preview:** canonical, description and OG image already exist. Name-only title lacks context; preview is a crowded application screenshot, missing image size/alt metadata.
7. **Links/content:** ten unique external URLs return HTTP 200; LinkedIn returns automation-blocking 999. Five log years are missing, layer tags need confirmation, and OcuGate uses an information tile pending real images. Keep these explicit questions.

## Verification and delivery

See the audit report added with this PR. Acceptance is reviewed at PR time; merge is Graham's decision.
