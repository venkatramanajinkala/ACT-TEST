# ACT-R33 / R37 / R25 — Standalone Repro

Minimal, self-contained reproduction pages for three ticketed findings.
This package is deliberately separate from the main `a11y-rule-fixtures`
suite — nothing here is combined with or dependent on that project.

## Directory structure

```
act-r25-r33-r37-repro/
├── fail.html
├── pass.html
├── index.html
├── media/
│   ├── r33-demo-video.mp4
│   ├── r37-demo-video.mp4
│   ├── r37-demo-video-en.vtt
│   ├── r37-demo-video-ad.vtt
│   ├── r25-demo-video.mp4
│   ├── r25-demo-video-en.vtt
│   └── r25-demo-video-ad.vtt
└── README.md
```

All videos are original generated content (`ffmpeg`/`drawtext` for
visuals, `espeak-ng` for narration) — no external assets or network
dependencies.

## Original ticket findings this repro is based on

### ACT-R33 — AMP-0108 — Valid Issue

- **Tested page:** `https://act-testing.netlify.app/accessibility-rules-fail`
- **Description:** The detected alternative for this media element may
  not fully represent all its content. Verify that the alternative is
  accurate, complete, and equivalent.
- **Test method:** Compare a video with its transcript. If the video
  shows an important event that the transcript doesn't mention, flag it.
- **WCAG mapping:** 1.2.1, Level A.
- **Result:** Tool detected 4 occurrences. Manual verification confirmed
  all 4 as valid — classified as a **Valid Issue**.
- **Reviewer:** Venkat. **Status:** Verified.

### ACT-R37 — AMP-0073 — Duplicate + False Positive

- **Tested page:** `https://projects.accesscomputing.uw.edu/au/before.html`
  (Accessible University — Inaccessible Version demo page)
- **Description:** Pre-recorded video must include a synchronised audio
  description track (or an alternative version) that describes important
  visual events not covered by the existing audio.
- **Test method:** Play a video without looking at the screen. Important
  visual actions should be explained in the audio description.
- **WCAG mapping:** 1.2.5, Level AA.
- **Result:** Tool detected 1 occurrence. Manual verification found the
  existing audio in the AU Promo Video already adequately conveys the
  important visual information — no additional audio description or
  alternative version was actually needed. Classified as a
  **False Positive** (Invalid Issue). Also noted as a **duplicate** of R25.
- **Reviewers:** Venkat (initial), Ankush (review).

### ACT-R25 — AMP-0081 — Duplicate

- **Tested page:** same as R37 above.
- **Description:** Pre-recorded video must include a synchronized audio
  description track, or an equivalent alternative version, for important
  visual information not conveyed by the existing audio.
- **Test method:** Watch a video without looking at the screen. Important
  visual events should be communicated through audio description or an
  equivalent alternative.
- **WCAG mapping:** 1.2.5, Level AA.
- **Result:** Tool detected 0 occurrences on its own scan pass, but the
  finding is tracked as a **duplicate of R37** — both rules check the
  same underlying condition (audio description for visual-only
  information) and fired together against the same page/video.
- **Reviewers:** Venkat (initial), Ankush (review).

## Why R25 and R37 are kept as separate pages here anyway

Even though the real-world tickets found R25 and R37 duplicate each other
on the same source page, this repro keeps them as two independently
reproducible scenarios (different video, different visual event) so each
ticket can still be verified on its own without one masking the other.
This mirrors the same "one dedicated video per rule" approach used
throughout the main fixture suite.

## Manual test steps

- **R33 FAIL** — watch the video, then read the transcript below it;
  confirm the on-screen "Session expires in 2 minutes" warning is visible
  in the video but never mentioned in the transcript.
- **R33 PASS** — same comparison; confirm the transcript now mentions it.
- **R37 FAIL** — play the video without looking at the screen; confirm
  the "Toggles Email Alerts OFF" action is not communicated by the audio
  at all.
- **R37 PASS** — play again without looking at the screen; confirm the
  audio-description track now narrates that action during the pause.
- **R25 FAIL** — watch the video without looking at the screen; confirm
  the "72% of goal reached" figure is not communicated by the audio.
- **R25 PASS** — watch again without looking at the screen; confirm the
  audio-description track now narrates that figure.

## Notes

- No CDN, framework, or external network dependency anywhere.
- Asset paths are local and relative throughout (`media/…`).
