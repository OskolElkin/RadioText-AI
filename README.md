# RadioText AI

**0.2.0 Test — an Android test candidate, not a production or public beta release.**

RadioText AI turns selected radio audio into readable captions and suggests possible contest announcements. It aims to help people follow spoken radio information visually, including deaf and hard-of-hearing listeners. It does not guarantee accurate transcripts, contest eligibility, accepted keywords or prizes.

This public repository publishes documentation only. The owner authorized publication of these five documents on 2026-10-31. Application sources, APKs, signing material, private implementation reports and local Git history are not published here. Device acceptance remains incomplete; do not redistribute private project material without separate authorization.

## Implemented capabilities and evidence

| Capability | Implemented scope | Verification limit |
|---|---|---|
| Live Captions | Bundled Vosk small English 0.15 and Russian 0.22; manual language selection while stopped | Host synthetic checks exist; Android accuracy and long sessions still need testing |
| Audio inputs | Direct HTTPS radio via Media3, microphone, Android playback capture with system consent | Device and source restrictions vary; not every input has device acceptance |
| Reading | Interim/final text, timestamps, adjustable caption size, reading view, pause/resume scrolling | TalkBack and large system fonts need device review |
| Contest Detection | Conservative final-text rules, literal word/phrase matching, configurable confidence and duplicate suppression | Suggestions can be wrong; context confirmation is not official acceptance |
| History and notifications | Local text/events, review/dismiss/delete controls, visual alerts and optional vibration | Notification delivery, lock-screen privacy and battery behavior need Android tests |
| Manual participation | Separate official source/rules/entry links; drafts or external apps for supported methods | No automatic SMS, calls, messages, registration or entry submission |

Artist watches detect names mentioned in captions; they do **not** identify the playing song. Acoustic reference-matching infrastructure exists, but the production reference list is empty. Signal detection and music fingerprint recognition are therefore unavailable.

## Russia, CIS and Canada registry

The registry supports country filters for Canada, Russia, Belarus, Kazakhstan and Other CIS, together with active, cash-only and keyword-based filters. Country coverage in the UI is not proof that every country has verified contests or working streams.

- Russia/Belarus station profiles: Radio MAXIMUM, Avtoradio, Radio SI, Russkoe Radio, Radio Dacha and Unistar.
- The previous review recorded published official Moscow HLS URLs for MAXIMUM, Avtoradio and Russkoe Radio. Stable official streams for the other three profiles remain unverified.
- One new Russian contest record, Avtoradio's 2026 campaign, was reviewed against official rules. It involves registration, ringback-tone and organizer-call conditions; it is not a simple keyword-to-SMS contest.
- Canada's CHUM 104.5, STAR 95.9 and 93.7 JR Country records remain, including incomplete dates and conflicting-condition notes. Verified metadata is distinct from an active round.
- There is no automatic contest/keyword feed. Curated verification expires after 24 hours. Local Refresh recalculates status; it does not renew source verification. No current contest-source refresh was performed for this documentation package.

See source review (retained privately; not published here) and feature details (retained privately; not published here). Unavailable sources must leave radio/captions usable and display an honest unverified/empty state. No production fixture represents a real contest.

## Trying the test candidate

1. Obtain the APK privately from the owner and verify the supplied SHA-256. Do not use a public mirror.
2. `RadioText AI 0.2.0 Test` uses package `ai.radiotext.preview` and can sit beside 0.1.9. It has its own empty local store; it does not migrate old data. Do not uninstall 0.1.9 to install an APK with a different signature. The original signing key is required for an in-place upgrade of the original package.
3. While stopped, select **English captions** or **Russian captions**, then choose a station/input and press **Start**. Radio needs internet. Microphone recognition is designed to use the bundled model without internet; verify that on your device.
4. Grant only the permissions required for the chosen mode. Android playback capture additionally needs a system grant and a source that permits capture.
5. Use **Stop** or the ongoing notification's **Stop Listening** control. Review detected words against official instructions before taking any action.

See [TESTING.md](TESTING.md) before reporting a successful device scenario. APK installation, Android 10–16, notifications, accessibility and background behavior are not certified by host tests.

## Local catalog and external links

Permitted manual JSON imports remain unverified. The existing catalog limit is 500 local records, separate from bundled records; country codes now include the supported Russia/CIS set. Preserve stable IDs when updating a card. The import UI limits text to 200,000 characters. Do not import credentials or personal entry data.

```json
[{"id":"your-stable-id","title":"Official contest title","country":"CA","province":"ON","stationName":"Station name","entryMethod":"WEB_FORM","entryUrl":"https://station.example/contest/entry","officialRulesUrl":"https://station.example/contest/rules","sourceUrl":"https://station.example/contest","timezone":"America/Toronto"}]
```

This example is documentation only. Existing methods include website, official app information page, SMS, phone, email, on-air, in-person, messenger and unknown. ContestScoop's automatic adapter remains disabled because of its access restrictions.

External links use the existing HTTPS/DNS/redirect checks and a confirmation dialog. A reachable destination is not official contest verification. HEAD rejection or conservatively rejected IPv6/dual-stack destinations can leave legitimate links unverified; the browser may make further redirects. Always inspect the destination and official conditions.

## Privacy, accessibility and collaboration

Read the [preliminary privacy notice](PRIVACY.md). Local processing is not a promise that all app operations are offline: station search, playback and external destinations use third parties.

Accessibility development is planned with voluntary participation by deaf and hard-of-hearing people, accessibility specialists and QA testers. Planned work includes a tested accessibility mode, TalkBack/focus review, text scaling, contrast and clear non-audio states. These are goals, not completed certification or a medical service.

Android developers, speech specialists, QA engineers and volunteers are welcome to discuss improvements with the owner through an authorized private channel. See [CONTRIBUTING.md](CONTRIBUTING.md) and [ROADMAP.md](ROADMAP.md). Core features remain independent of optional developer support; support opens an external website with its own privacy practices.

## Project references

Implementation reports, source files, historical README/changelog and raw evidence remain in the private project backup. Names below identify privately retained records, not downloadable files in this repository.

- [Testing plan and known findings](TESTING.md)
- 0.2.0 implementation report, Russian (retained privately; not published here)
- Recorded evidence (retained privately; not published here)
- Earlier README, preserved verbatim (retained privately; not published here)
- Changelog (retained privately; not published here), license (retained privately; not published here) and third-party notices (retained privately; not published here)
- Existing deployment notes (retained privately; not published here) — historical backend options are not evidence of a deployed cloud-caption service

No application code, APK build or application test was run for this documentation-only package.
