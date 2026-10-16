# Portfolio audit, 15 October 2026

Spec: [REQ-PORTFOLIO-01](../portfolio-polish.md). Task: TRI-218.
Baseline: `8227ac3`. Tested implementation: `7e22eed`.
The later evidence commit changes documentation and font-license whitespace only.

## Ranked findings and fixes

1. **First impression and mobile hierarchy.** At 390px, selected work started 1,311px down the live page. The decorative stack and controls consumed separate vertical blocks. Compact side-by-side plates and controls bring work to 878px, about 33% sooner. The hero now names hardware, firmware and software directly and offers an explicit work link. Detailed tools remain in About on phones.
2. **Render-blocking fonts and oversized images.** The primary site's mobile performance score was 82 with a 3.87s LCP. Local IBM Plex fonts eliminate the external stylesheet chain; licensed Latin subsets preserve typography. Responsive WebP images reduce the preview's measured page transfer from 938 to 463 KiB. Images retain intrinsic dimensions, lazy loading and alt text. Both switchers update responsive sources and intrinsic dimensions together.
3. **Small-screen reading and visual consistency.** At 320px, log titles shared a narrow row with revision, year and external links. Titles and descriptions now use the full row, metadata remains above them, and section headings can wrap cleanly. Card links align within each desktop row. The OcuGate information tile fits narrow screens. About paragraphs have breathing room.
4. **Keyboard navigation.** The baseline already used real buttons, aria-pressed, visible focus and live result counts. Hero jumps now transfer focus to the log heading. Clearing an empty result restores focus to Everything. Added a skip link; controls have 44px minimum heights. Reduced motion disables transitions as well as entrance animation and smooth scrolling.
5. **SEO and sharing.** The baseline already had a canonical URL, description and working OG image. A descriptive title and dedicated 1200×630 portfolio preview now identify Graham instead of showing a dense application screen. Added image dimensions, MIME type and alt metadata; the canonical remains the primary Vercel URL.
6. **Images, links and unresolved content.** No broken on-page images were found. Graham explicitly confirmed that the existing OcuTrap screenshots are fine after the fleet-count/device-label concern was raised; those images are retained. OcuGate still needs approved images. All ten other unique external destinations returned HTTP 200; LinkedIn returned 999 and could not be independently verified. Five dates and project-specific facts remain questions below.

No horizontal document overflow or console errors were found on either baseline host at the four tested widths. The fixes preserve the paper, soldermask green, copper and IBM Plex identity; the site remains plain HTML/CSS/JavaScript without a build step or CDN scripts.

## Lighthouse mobile results

| Environment | Performance | Accessibility | Best practices | SEO | FCP | LCP | CLS | Transfer |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Before: live Vercel | 82 | 100 | 100 | 100 | 3.05s | 3.87s | 0 | 938 KiB |
| Before: live GitHub Pages | 89 | 100 | 100 | 100 | 2.60s | 3.26s | 0.0008 | 937 KiB |
| Before: baseline on local test server | 80 | 100 | 100 | 100 | 2.47s | 4.58s | 0.0008 | 965 KiB |
| After: branch on same local test server | 99 | 100 | 100 | 100 | 1.35s | 2.18s | 0 | 496 KiB |
| After: protected Vercel preview | 100 | 100 | 100 | 61* | 1.14s | 1.44s | 0 | 463 KiB |

All runs have 0ms total blocking time. Lighthouse 13.0.1, Chromium for Testing, default mobile emulation (412×823, DPR 1.75), simulated throttling (150ms RTT, 1,638.4 Kbps throughput, 4× CPU slowdown). Screenshots and functional checks separately use 320, 390, 768 and 1440 CSS pixels. These are single lab runs, not field Core Web Vitals or promises about every connection. The paired local runs use the same Node static server and cache headers; remote hosts and preview authentication introduce additional variation.

*The protected preview intentionally sends `X-Robots-Tag: noindex`. Lighthouse also encounters Vercel's authentication response while checking `robots.txt`, producing a 61 SEO score. This is preview infrastructure, not a production SEO regression. The branch scores 100 for SEO on the local static server. Production remains on the baseline until Graham merges. A temporary CLI automation credential was revoked after verification; credentials are excluded from evidence.*

[Machine-readable scores and settings](lighthouse/summary.json). Compressed full reports: [live Vercel before](lighthouse/before-vercel.json.gz), [GitHub Pages before](lighthouse/before-github.json.gz), [controlled baseline](lighthouse/before-local-controlled.json.gz), [local after](lighthouse/after-local-final.json.gz), [preview after](lighthouse/after-preview.json.gz). The preview report has its authentication cookie redacted; all scores and audit results are retained.

## Verification

- Both baseline hosts: HTTP 200, screenshots of every section at 1440 and 390px, overflow checks at 320/390/768/1440px.
- Branch locally and on protected Vercel preview: no horizontal overflow, browser console errors, page exceptions or failed requests at any tested width.
- All 28 kind/layer combinations at each width produce the expected rows and pressed states. Tested no-results feedback, reset, hero-to-log focus transfer, and the next Tab destination.
- All seven image views activated with the keyboard at each width. Verified decoded image, matching alt text, responsive source and a single pressed button per group.
- Skip link and focus outlines checked; reduced motion reports no plate animation, no transitions and automatic scrolling. All 18 log entries remain readable with JavaScript disabled.
- Every internal anchor resolves. Both email links use `grahampatterson14@gmail.com`. No visitor-facing em dashes. No drone delivery content or new project facts.
- Responsive assets return HTTP 200. External URLs are unchanged and were rechecked: ten return 200, LinkedIn returns 999. Mail links are verified as addresses, not HTTP resources.
- Automated accessibility score remains 100. This is not a substitute for a full assistive-technology audit; no manual screen-reader session was performed.

Evidence: [local interactions](verification.json), [deployed-preview interactions](verification-preview.json), [asset responses](assets.json), [external link responses](links-after.json).

## Questions for Graham

1. What years belong to Weather station, R1 production trap, OcuCam, Image recognition and OcuTrap platform?
2. Are all per-entry layer tags correct, especially school projects with no tags? The existing tags and chronology are retained.
3. Which approved OcuGate product photos or your own app captures should replace the information tile? No App Store screenshots were added.
4. TailSafe says both “first prototype board done” and “nothing built yet.” Does “done” mean PCB design complete, ordered, or assembled? Copy remains unchanged pending confirmation.
5. Does “R1, production trap” / “Ships today” still describe the product you want featured? No new production claim was added.
6. What specific outcome should Weather station and OcuRover communicate? The existing short descriptions remain unchanged rather than guessing.
7. Should polycase-mcp, Tidy Rover or Tasker HQ join selected work? Which existing project would each replace or complement?
8. Please confirm the LinkedIn profile opens publicly. Automated HTTP checks receive 999, and a browser navigation does not yield a stable independently verifiable profile.

## Larger proposals, not implemented

- Add one short engineering case study with verified constraints, decisions and results if deeper evaluation becomes a priority. Keep any OcuTrap details public-safe.
- Consider an owned personal domain if desired; retain this static implementation. A framework or redesign is not justified by this audit.
- Replace the OcuGate information tile when approved imagery is available; confirm dates/tags before changing the log or adding candidate projects.

## Risk and rollback

Low-risk static changes. New responsive image derivatives and local fonts add checked-in assets; original JPEGs remain available. Latin font subsets cover current copy; future non-Latin copy may need additional subsets. Revert this PR to return to the baseline. Graham reviews and merges; main was not pushed or merged by this task.

## Screenshot index

The images below cover each section. “Viewport” includes navigation and the first 900px; “Hero” captures the entire hero. All screenshots use DPR 1 and settled entrance animations.

### Before: Vercel

| Width | Viewport | Hero | Work | Build log | About | Contact |
| --- | --- | --- | --- | --- | --- | --- |
| 1440 | [viewport](screenshots/before-vercel-1440-viewport.webp) | [hero](screenshots/before-vercel-1440-hero.webp) | [work](screenshots/before-vercel-1440-work.webp) | [log](screenshots/before-vercel-1440-log.webp) | [about](screenshots/before-vercel-1440-about.webp) | [contact](screenshots/before-vercel-1440-contact.webp) |
| 390 | [viewport](screenshots/before-vercel-390-viewport.webp) | [hero](screenshots/before-vercel-390-hero.webp) | [work](screenshots/before-vercel-390-work.webp) | [log](screenshots/before-vercel-390-log.webp) | [about](screenshots/before-vercel-390-about.webp) | [contact](screenshots/before-vercel-390-contact.webp) |

### Before: GitHub Pages

| Width | Viewport | Hero | Work | Build log | About | Contact |
| --- | --- | --- | --- | --- | --- | --- |
| 1440 | [viewport](screenshots/before-github-1440-viewport.webp) | [hero](screenshots/before-github-1440-hero.webp) | [work](screenshots/before-github-1440-work.webp) | [log](screenshots/before-github-1440-log.webp) | [about](screenshots/before-github-1440-about.webp) | [contact](screenshots/before-github-1440-contact.webp) |
| 390 | [viewport](screenshots/before-github-390-viewport.webp) | [hero](screenshots/before-github-390-hero.webp) | [work](screenshots/before-github-390-work.webp) | [log](screenshots/before-github-390-log.webp) | [about](screenshots/before-github-390-about.webp) | [contact](screenshots/before-github-390-contact.webp) |

### After: Vercel preview

| Width | Viewport | Hero | Work | Build log | About | Contact |
| --- | --- | --- | --- | --- | --- | --- |
| 320 | [viewport](screenshots/after-preview-320-viewport.webp) | [hero](screenshots/after-preview-320-hero.webp) | [work](screenshots/after-preview-320-work.webp) | [log](screenshots/after-preview-320-log.webp) | [about](screenshots/after-preview-320-about.webp) | [contact](screenshots/after-preview-320-contact.webp) |
| 390 | [viewport](screenshots/after-preview-390-viewport.webp) | [hero](screenshots/after-preview-390-hero.webp) | [work](screenshots/after-preview-390-work.webp) | [log](screenshots/after-preview-390-log.webp) | [about](screenshots/after-preview-390-about.webp) | [contact](screenshots/after-preview-390-contact.webp) |
| 768 | [viewport](screenshots/after-preview-768-viewport.webp) | [hero](screenshots/after-preview-768-hero.webp) | [work](screenshots/after-preview-768-work.webp) | [log](screenshots/after-preview-768-log.webp) | [about](screenshots/after-preview-768-about.webp) | [contact](screenshots/after-preview-768-contact.webp) |
| 1440 | [viewport](screenshots/after-preview-1440-viewport.webp) | [hero](screenshots/after-preview-1440-hero.webp) | [work](screenshots/after-preview-1440-work.webp) | [log](screenshots/after-preview-1440-log.webp) | [about](screenshots/after-preview-1440-about.webp) | [contact](screenshots/after-preview-1440-contact.webp) |

## Reproduction notes

No packages are required to run the site. Serve the repository with any static server. Audit tooling was installed outside the repository: Playwright 1.58.2, Lighthouse 13.0.1, Sharp 0.34.5. Lighthouse invocation: `lighthouse URL --chrome-flags='--headless' --output=json --output=html --only-categories=performance,accessibility,best-practices,seo`. The protected-preview run additionally used a temporary authentication header, omitted from public evidence.

Image derivatives were made from the existing JPEGs at 480px, 800px and native width without upscaling, using WebP quality 82 (74 for the dense golf maps), effort 6. The app icon is 168px for its 84px display size. The social preview is a 1200×630 browser capture of [its HTML source](../social-preview.html) after local fonts load. Original JPEGs are retained as sources. Evidence screenshots use WebP quality 82 and preserve their original capture dimensions; the two log excerpts intentionally show the top 900px.
