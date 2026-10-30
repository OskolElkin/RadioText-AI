# Preliminary privacy notice — draft for review

**Not a final legal policy or a compliance certification.** Reviewed 2026-10-31 against privately retained implementation material and existing evidence for RadioText AI 0.2.0 Test. No new device/network tests were performed. The draft covers the supplied on-device preview design; future cloud or customized builds need a new review.

Before public distribution, the owner must confirm the responsible operator/contact, applicable jurisdictions, participant age arrangements, retention/feedback procedures and any store disclosures. No unverified legal identity, address or contact is supplied here.

## Current intake status and prerequisites

This public repository is not a feedback-data intake form. Do not post histories, recordings, diagnostic bundles, personal screenshots, contact details, disability/health information or identifying third-party speech in public issues or pull requests. Public GitHub activity exposes account identifiers and contribution text under GitHub's own policies; project maintainers can also receive and retain contributions. "Local recognition" does not describe that separate processing.

**Do not begin wider tester recruitment or project collection of personal feedback until the owner establishes:**

- The responsible person/entity, a working private contact and the countries/activities covered.
- Each purpose, data category, necessity and applicable lawful basis; meaningful consent where required, including a withdrawal process where applicable. Android permission is not a complete legal basis or privacy notice.
- Recipients/processors, hosting and transfer destinations, access safeguards, retention periods and deletion handling, including copies in issue/email systems.
- A usable process for access/correction/deletion and other applicable rights, incident handling and any required regulator notices, localization or transfer arrangements.
- Age eligibility and any required guardian arrangements before involving minors; there is no current child-testing recruitment program.

These are unresolved project gates, not a statement that the software enforces an intake block. Do not send personal data merely to ask for a contact. Non-personal documentation corrections may use the public repository.

## Jurisdiction review — unresolved

Applicable law depends on the operator, actual processing, users, locations and activities. A country filter or station's country does not decide applicability. This draft makes no declaration of compliance with any national law.

| Review area | Required owner/legal determination |
|---|---|
| Russia | Assess 152-FZ applicability and current requirements for notices, lawful bases, security, retention, localization and cross-border processing before collecting tester data. The [Ministry's published text](https://mintrud.gov.ru/docs/laws/130) is a starting reference, not a verified current consolidated 2026 edition; confirm subsequent amendments and regulator procedures. |
| Belarus and Kazakhstan | Obtain current official texts and assess operator duties, grounds for processing and transfer/localization rules where applicable. The Belarus authority site was unavailable during this check; the [Kazakhstan official legal portal](https://adilet.zan.kz/rus/docs/Z1300000094) required JavaScript. Neither jurisdiction is cleared by this review. |
| Canada | Determine whether federal PIPEDA, provincial laws or other rules apply to the actual activity. The [Canadian privacy regulator](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/pipeda_brief/) explains commercial-activity scope and provincial distinctions; a Canadian registry entry alone is insufficient. |
| EU/EEA, if relevant | Assess GDPR material/territorial scope, including establishment, offering services or monitoring criteria; mere worldwide page availability does not settle applicability. See [GDPR Articles 2–3](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX%3A02016R0679-20160504). Other destinations need their own assessment. |

References identify review topics, not legal approval. Where an official page was inaccessible or not current, verification remains open; no access restriction was bypassed.

## Audio and recognition

| Input | Source-reviewed behavior | Still requires confirmation |
|---|---|---|
| Microphone | `AudioRecord` captures after the relevant Android grant and explicit start; PCM is fed to bundled Vosk | Runtime permission revocation, actual stop/release and offline behavior across devices |
| Direct radio | Media3 connects to the selected remote HTTPS stream; decoded PCM feeds local Vosk | Full device traffic, reconnect behavior and each broadcaster/CDN's practices |
| Android playback capture | Uses `RECORD_AUDIO` and a separate MediaProjection grant; only source-permitted audio is intended to be captured | Android/OEM/source restrictions and capture-stop behavior on devices |

`VoskEngine.kt` and `ModelFiles.kt` select a bundled English or Russian model and use an in-memory audio queue. The reviewed input paths do not intentionally write captured audio files or upload captured audio for recognition. This is a source-level finding, **not** a forensic or network-audit guarantee about the operating system, every dependency or every custom build. Model files themselves are extracted to app-private no-backup storage; they are not recordings.

Microphone recognition is designed to operate without internet because the models are bundled. This does not mean the whole application works offline: new station searches, live internet radio, destination checks and external pages need network access. Existing local history/catalog data can be read without fetching a feed; device-level airplane-mode validation is pending.

The repository also contains optional server/client scaffolding, including `RemoteCaptionSource.kt` and `backend/`. The reviewed `ListeningService` selects local radio or recorded-input sources, not that remote caption class. Those files are not evidence of a deployed cloud service. Enabling a cloud path requires an explicit design, a lawful-basis and privacy review, any required consent and transfer safeguards before use.

## Data stored on the phone

The source uses app-private SharedPreferences, including `captions` and `contest_catalog_019`, for:

- Recognized final text, timestamps, source/session identifiers, confidence, suggested words, context and detection/review state.
- User-entered entry instructions, words/phrases/artist watches and detection settings.
- Selected, recent and favorite stations; caption/input/language/sound/vibration settings.
- Local contest cards, verification metadata and saved contests.

`HistoryCodec.retain` keeps the latest 200 non-contest caption rows plus contest-marked rows; it does not impose a fixed maximum or automatic expiry for all detection events. The live view separately limits its current-session display. Do not interpret “200 captions” as a universal retention/deletion guarantee.

Settings provides deletion of local caption/contest-detection history; timeline events can also be deleted individually. **Dismiss marks an event rejected; it does not delete it.** Clearing caption history does not clear station favorites, watch settings, saved catalog cards or every preference. Catalog cards have separate controls; bundled curated records are read-only. Secure forensic erasure and the deletion behavior of copies outside the app have not been verified.

No account is required by the reviewed app UI. Private storage is not a claim of application-level encryption. The manifest disables Android backup and the data-extraction rules exclude cloud backup and device transfer; effective OEM/OS behavior still needs validation. Uninstalling normally removes app-local data, so do not uninstall an older installation just to resolve a signing mismatch. Preview and original package stores are separate and no migration between them is claimed.

## Network recipients and user-directed disclosure

| Operation | Possible recipient/data |
|---|---|
| Station search | Radio Browser directory; search terms/region/country/genre parameters and ordinary network metadata such as IP address |
| Stream playback | Broadcaster/CDN; selected stream request and ordinary connection metadata |
| Contest destination check | Target server, redirects and DNS resolution; URL/HEAD requests, not intended caption/audio uploads |
| Open rules, entry, support or other links | External browser/app and destination operators; their own privacy practices apply |
| Copy text/keyword/diagnostics | Android clipboard, then any destination the user pastes into; review sensitive text before copying/sharing |
| SMS/email/dialer drafts | The selected external app receives the prepared destination/text; this is user-directed disclosure, not automatic submission by RadioText AI |

Optional developer support opens Boosty in a browser. The reviewed app does not embed a payment form or receive payment credentials; the external service's practices require separate review. No analytics or advertising SDK is declared in the app's direct dependency list, but this documentation-only pass is not a complete transitive-SDK or runtime traffic audit. Do not claim “no third-party data transfer” for the whole application.

Contest notifications can expose station names, words, text and other event details to people viewing the device/lock screen. Review Android notification privacy settings. Optional vibration is not consent to share captured information.

## Android permissions

The manifest declares `INTERNET`, `ACCESS_NETWORK_STATE`, `WAKE_LOCK`, `VIBRATE`, `POST_NOTIFICATIONS`, `RECORD_AUDIO`, `FOREGROUND_SERVICE` and its `MEDIA_PLAYBACK`, `MICROPHONE`, `MEDIA_PROJECTION` variants. These map to network/audio, optional alerts and foreground listening; declaration does not by itself prove every permission is necessary or correctly scoped. See the per-mode review matrix in [TESTING.md](TESTING.md).

Listening uses an ongoing foreground notification with a Stop action; the service returns `START_NOT_STICKY`. Continued user-started foreground listening is different from hidden monitoring. Stopping after interruptions, revocation, process death and device sleep remains a device-test requirement.

## Voluntary feedback and open questions

The template in CONTRIBUTING.md is for future arranged tests after the intake prerequisites above are met. A private route alone does not resolve those prerequisites. Do not send diagnoses, identity/bank documents, credentials, complete histories, recordings or third-party conversations by default. See [CONTRIBUTING.md](CONTRIBUTING.md) for redaction. The owner's feedback retention, deletion request handling, processors and contact details are **not yet confirmed** and must be agreed before recruiting a wider cohort.

Remaining validation includes runtime network observation, effective backup/deletion, notification/clipboard exposure, permission behavior, background stop behavior and dependency data practices. This draft must be updated when those findings or the implementation change; it must not be presented as an approved final policy.
