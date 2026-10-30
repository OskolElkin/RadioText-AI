# Preliminary privacy notice — draft for review

**Not a final legal policy or a compliance certification.** Reviewed 2026-10-31 against privately retained implementation material and existing evidence for RadioText AI 0.2.0 Test. No new device/network tests were performed. The draft covers the supplied on-device preview design; future cloud or customized builds need a new review.

Before public distribution, the owner must confirm the responsible operator/contact, applicable jurisdictions, participant age arrangements, retention/feedback procedures and any store disclosures. No unverified legal identity, address or contact is supplied here.

## Audio and recognition

| Input | Source-reviewed behavior | Still requires confirmation |
|---|---|---|
| Microphone | `AudioRecord` captures after the relevant Android grant and explicit start; PCM is fed to bundled Vosk | Runtime permission revocation, actual stop/release and offline behavior across devices |
| Direct radio | Media3 connects to the selected remote HTTPS stream; decoded PCM feeds local Vosk | Full device traffic, reconnect behavior and each broadcaster/CDN's practices |
| Android playback capture | Uses `RECORD_AUDIO` and a separate MediaProjection grant; only source-permitted audio is intended to be captured | Android/OEM/source restrictions and capture-stop behavior on devices |

`VoskEngine.kt` and `ModelFiles.kt` select a bundled English or Russian model and use an in-memory audio queue. The reviewed input paths do not intentionally write captured audio files or upload captured audio for recognition. This is a source-level finding, **not** a forensic or network-audit guarantee about the operating system, every dependency or every custom build. Model files themselves are extracted to app-private no-backup storage; they are not recordings.

Microphone recognition is designed to operate without internet because the models are bundled. This does not mean the whole application works offline: new station searches, live internet radio, destination checks and external pages need network access. Existing local history/catalog data can be read without fetching a feed; device-level airplane-mode validation is pending.

The repository also contains optional server/client scaffolding, including `RemoteCaptionSource.kt` and `backend/`. The reviewed `ListeningService` selects local radio or recorded-input sources, not that remote caption class. Those files are not evidence of a deployed cloud service. Enabling a cloud path requires an explicit design, consent and privacy review before use.

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

Use only an owner-approved private contact route. Do not send diagnoses, identity/bank documents, credentials, complete histories, recordings or third-party conversations by default. See [CONTRIBUTING.md](CONTRIBUTING.md) for redaction. The owner's feedback retention, deletion request handling, processors and contact details are **not yet confirmed** and must be agreed before recruiting a wider cohort.

Remaining validation includes runtime network observation, effective backup/deletion, notification/clipboard exposure, permission behavior, background stop behavior and dependency data practices. This draft must be updated when those findings or the implementation change; it must not be presented as an approved final policy.
