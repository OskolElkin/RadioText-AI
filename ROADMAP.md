# Roadmap

Status: 0.2.0 Test. Documentation reviewed 2026-10-31. Checked items require existing source or recorded evidence; unchecked items are future work, not promises of dates or outcomes. This package does not authorize code changes, new scans, builds or publication.

## 1. Security and release blockers

- [ ] Triage the supplied APKLint findings and obtain the actual completed Ostorlab #219340 report. No Ostorlab findings are inferred from an unfinished/missing report.
- [ ] Produce and inspect a non-debuggable, properly signed release candidate in a separately authorized development cycle. Current Test is debug-signed/debuggable.
- [ ] Review each Android permission against each input mode and verify denial/revocation behavior on devices.
- [ ] Resolve the API 35 versus current Play submission requirement described in [TESTING.md](TESTING.md); confirm any account-specific exception rather than assume one.
- [ ] Verify access to privately retained project material, protect signing keys and define a private vulnerability-reporting contact before inviting wider participation.

## 2. APK optimization

- [ ] Measure APK, installation, model storage and runtime memory separately; record ABI and language-model contributions.
- [ ] Evaluate ABI-specific packaging/AAB and model delivery or compression without breaking offline use, licensing or existing data.
- [ ] Measure cold start, heat and battery on representative devices before choosing optimizations. No size-reduction result is claimed.

## 3. Russian and English recognition

- [x] Bundle both models with manual selection; keep model provenance/checksums. Evidence: model verification (retained privately; not published here).
- [x] Record controlled host recognition, including a Russian neural-synthetic example. Evidence: synthetic results (retained privately; not published here).
- [ ] Evaluate Android microphone/radio/playback inputs with independently reviewed transcripts, WER/CER, exact keyword accuracy and latency.
- [ ] Cover accents, music, noise, names, low-confidence text and language changes. Fix the stale microphone status that still says “speak English” even when testing Russian.

## 4. Radio and source verification

- [x] Record a bounded host check of an official Avtoradio stream, without saving radio audio. Evidence: host smoke check (retained privately; not published here).
- [ ] Verify playback/captions and reconnect behavior on Android, including regional differences and permitted capture.
- [ ] Confirm stable official streams for Radio SI, Radio Dacha and Unistar; leave unknown values unverified until then.
- [ ] Recheck current contest rules, schedules, timezones, eligibility and entry destinations. Document a lawful update workflow; do not automatically renew stale evidence.

## 5. Keyword and contest detection

- [x] Implement final-text suggestions, contextual states, literal phrase/artist watches and duplicate suppression. Evidence: targeted results (retained privately; not published here).
- [ ] Measure false positives/misses on labelled material; verify adjacent segments and notifications on devices.
- [ ] Add acoustic signal detection only with reviewed, legally usable reference samples and measured false positives. Production has no samples today.
- [ ] Consider music identification only with an available mechanism and an approved data/consent model; artist mentions are not song identification.

## 6. Accessibility mode

- [ ] Co-design with deaf and hard-of-hearing volunteers; participation and disclosure of hearing needs must be optional.
- [ ] Test TalkBack, focus order, 200% text, display scaling, contrast, touch targets, reading continuity and all non-audio states.
- [ ] Validate clear controls for live scrolling, errors, notification privacy, vibration and stopping capture; do not claim accessibility certification prematurely.

## 7. Voluntary testing

- [ ] Agree on a private opt-in cohort, plain-language consent/instructions and a minimal redacted feedback form.
- [ ] Execute the [Android 10–16 matrix](TESTING.md), record exact artifact/device/results and triage reproducible issues.
- [ ] Review retention and private feedback handling with participants; never require diagnoses, banking data or contest entries.

## 8. Public beta preparation

- [ ] Close release/security, privacy, signing, SDK, accessibility and device-test gates; document remaining limits honestly.
- [ ] Finalize a reviewed privacy notice, contact route and applicable store disclosures.
- [ ] Obtain explicit owner approval for any public beta distribution and for exactly what may be shared. A beta plan does not authorize making the repository or APK public.
