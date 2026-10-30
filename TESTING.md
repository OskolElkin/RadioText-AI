# Testing plan — RadioText AI 0.2.0 Test

Documentation date: 2026-10-31. This is a plan plus references to **existing** evidence, not a new test execution or a fresh security audit. No APK build, application test, radio retest or external scan was launched for the documentation package.

## Artifact and known findings

| Item | Recorded/reported state | Required follow-up |
|---|---|---|
| Test artifact | `RadioText AI 0.2.0 Test`, package `ai.radiotext.preview`, versionName 0.2.0, versionCode 11 | Confirm the privately supplied file and hash before each new device session |
| SHA-256 | `1548ec3e367ac8df1b991d54cc0f4e0c2d808c253978674d41a9ef859c90de44` | A different artifact needs its own record; never reuse this hash for a rebuild |
| APKLint: debuggable | `android:debuggable=true` reported for the Test APK; consistent with a debug build | A debug-signed, debuggable candidate is not a production release. Verify final merged release manifest, signing and exposure before public beta |
| APKLint: target SDK | `targetSdkVersion=35`, corroborated by saved package evidence (retained privately; not published here); minSdk is 29 | Review/implement a separately authorized SDK migration and device checks; do not change SDK merely to silence a warning |
| APKLint: size | Reported 151.4 MiB (approximately 158.8 decimal MB) | Measure APK/download/installed/model/ABI sizes separately in a later authorized pass; no new measurement was made here |
| Permissions | Manifest declares the audio/network/foreground/notification permissions listed below | Validate necessity, denial, revocation and OS-specific behavior; a declaration is not proof of correct use |
| Ostorlab #219340 | Completed results have not been supplied for analysis in this package | Obtain the actual report privately and triage it. Do not invent findings, severity, clean status or completion |

The APKLint points above are the findings supplied in the task, not a claim that the complete original APKLint report was newly inspected. Existing build/signature evidence (retained privately; not published here) and the implementation report (retained privately; not published here) remain available.

### Google Play target API review

Official Google documentation checked **2026-10-31** states that, from August 31, 2026, new phone/tablet apps and app updates must target Android 16/API 36 or higher. API 35 is the stated availability threshold for existing published apps; that is not the same as permission to submit a new app or update. An extension to November 1, 2026 may be requested, but no project-specific approval has been verified. A private GitHub repository does not itself establish a Play policy exception or a published app status.

Sources: [Play Console target API requirements](https://support.google.com/googleplay/android-developer/answer/11926878?hl=en) and [Android Developers guidance](https://developer.android.com/google/play/requirements/target-sdk). Recheck at submission. This task changes documentation only, not targetSdk or publication settings.

## Existing evidence: do not add overlapping counts

| Evidence | Observed scope | What it does not establish |
|---|---|---|
| Prior full summary (retained privately; not published here) | 131 JVM tests passed before the latest Russian-context corrections | A final full-suite rerun after every later change |
| Targeted summary (retained privately; not published here) | 32 selected tests passed: Expansion020Test 18 and CanadianRegistryTest 14 | 32 additional independent tests on top of the earlier 131 |
| Final regional-field check (retained privately; not published here) | One selected case passed after the territory-text adjustment | A second full device or full-suite run |
| Python record (retained privately; not published here) | 8 regression tests passed | Android input/notification/permission behavior |
| Lint record (retained privately; not published here) | No issues found in that recorded run | No vulnerabilities or complete accessibility |
| Russian synthetic result (retained privately; not published here) | 27 nonempty interim updates; literal “север” recognized; other instruction errors remained | Official keyword validity, full instruction accuracy or real-air performance |
| Live host smoke check (retained privately; not published here) | 8 seconds of official Avtoradio stream decoded; 31 nonempty interim updates and 20 final words; no audio saved | Android Media3/JNI behavior, WER/CER, a real contest detection or eligibility |

No Android acceptance matrix is recorded as complete. Host Vosk 0.3.45 differs from Android Vosk 0.3.75. Follow the synthetic recipe (retained privately; not published here) only in a separately authorized test session; never seed synthetic contests/keywords into production.

## Android 10–16 device matrix

All rows below are **pending** for systematic acceptance. Record real hardware/emulator, manufacturer, build number (no unique device ID), app artifact and result. A minimum SDK declaration does not prove compatibility.

| Android | API | Priority observations |
|---|---|---|
| 10 | 29 | Minimum supported OS; playback-capture consent and source restrictions |
| 11 | 30 | Audio/microphone lifecycle and permission revocation |
| 12 | 31 | Foreground service launch restrictions and interruption recovery |
| 12L | 32 | Layout/display scaling and large-screen reading |
| 13 | 33 | Notification permission granted/denied; visual feedback remains usable |
| 14 | 34 | Foreground service types, microphone and MediaProjection grants |
| 15 | 35 | Current target behavior, service interruption and battery restrictions |
| 16 | 36 | Runtime compatibility and preparation for a future target API 36 build |

## Scenarios and acceptance records

For each case record Pass/Fail/Blocked, exact artifact, mode/language/device, steps, actual result and redacted evidence. Do not mark a blocked or unexecuted case passed.

| ID | Scenario | Expected result / evidence needed |
|---|---|---|
| INSTALL-01 | Verify private APK hash; install preview beside 0.1.9 | Distinct Test label/package, independent store; old installation/data untouched |
| UPDATE-01 | Future same-signature update using authorized key | History/settings/favorites preserved; no uninstall workaround. Blocked until matching signing material and a device are available |
| MIC-01 | Grant/deny microphone; start, stop, revoke permission, another recorder active | Clear state/error, no listening without start/grant; release verified after stop/revocation |
| LANG-01 | RU then EN controlled speech; switch only while stopped | Correct selected model, readable interim/final timestamps, raw final text preserved; independently reviewed reference and errors recorded |
| OFFLINE-01 | Airplane-mode microphone after installation/model preparation; repeat after process restart | Local captions or explicit failure, no dependency on server access; search/live radio fail honestly without network |
| RADIO-01 | Select a permitted official station, then another; disconnect/reconnect network and try unavailable/403 stream | Correct source label; no stale station callbacks; clear failures and safe captions behavior; no geographic bypass |
| CAPTURE-01 | Grant/revoke Android playback capture; permitted and blocked sources | No silent capture claim for a blocked source; consent/stop behavior verified |
| DETECT-01 | True synthetic announcement, ad/news/negation, no word, misspelling, low confidence | Literal suggestions only, no invented word/verified acceptance; raw transcription remains inspectable |
| DETECT-02 | Interim/final repeats, adjacent final upgrades, same word across stations, context timeout | No duplicate alert for one episode; correct reset/upgrade and documented cooldown limits |
| REGISTRY-01 | Country/active/cash/keyword filters; expired/stale/unknown rules; dates and timezone | Predictable filters, empty-state messages, no unverified active claim; local Refresh never renews verification |
| ENTRY-01 | Source/rules/entry separation, unsafe URL/redirect, missing destination | Safe review flow and manual action only; no real registration/SMS/call needed for testing |
| SIGNAL-01 | Production signal/song capabilities | Signal unavailable with no references; artist mention is not song identification. Evaluate synthetic reference primitives separately from real signals |
| HISTORY-01 | Restart, review, dismiss, delete event, clear all captions/events | Data retained as designed; dismiss is not delete; no claim that clearing captions clears every preference/catalog item |
| NOTIFY-01 | Notification grant/denial, vibration off/on, duplicate event and lock screen | Captions still readable without alerts; controls work; sensitive notification text exposure reviewed |
| BG-01 | Screen off, Home, notification Stop, audio interruption, process death and battery restrictions | Visible user-started foreground listening and clear stop behavior; no unexpected restart or hidden monitoring |
| POWER-01 | Agreed fixed-duration sessions and idle baseline | Record drain, temperature, RAM, gaps and latency; no battery/performance guarantee based on one phone |
| ERROR-01 | Model preparation/storage failure, network timeout, denied permissions | Readable status and recovery; no fabricated captions/contest cards; no old-session leakage |
| A11Y-01 | TalkBack, focus order, 200% font, display scale, contrast, touch targets and reading view | No clipped critical content; understandable monitoring/errors/alerts without sound; feedback from voluntary deaf/hard-of-hearing testers |

Known wording issue from source review: `RecordedAudioSource` still says “speak English” in the microphone status. Test Russian selection by the actual recognizer result; log the copy issue for future code work rather than editing code in this documentation task.

## Permission-necessity review

| Declared permission / grant | Intended use | What to verify later |
|---|---|---|
| INTERNET | Station search, radio, link checks | Offline microphone is independent; recipients and requests match [PRIVACY.md](PRIVACY.md) |
| ACCESS_NETWORK_STATE | Network-state capability | Locate actual use or justify removal in a future code review; necessity is not confirmed here |
| WAKE_LOCK | Media3 network wake mode | Needed only for active playback; release and battery effect |
| VIBRATE | Optional contest vibration | Off setting and channel behavior; no sound-only requirement |
| POST_NOTIFICATIONS | Listening/contest notifications on relevant OS versions | Grant/denial, foreground visibility and lock-screen privacy |
| RECORD_AUDIO | Microphone and Android playback capture | Not required merely to transcribe directly decoded radio PCM; avoid unnecessary runtime prompts |
| FOREGROUND_SERVICE | Explicit foreground listening | Valid launch, ongoing notification and Stop |
| FOREGROUND_SERVICE_MEDIA_PLAYBACK | Direct radio service type | Correct mode/type and OS behavior |
| FOREGROUND_SERVICE_MICROPHONE | Microphone service type | Correct permission timing and background restrictions |
| FOREGROUND_SERVICE_MEDIA_PROJECTION | Capture service type | Correct system consent and revoked-grant handling |
| MediaProjection system grant | Permission to capture source-permitted device playback | Fresh consent where required; never bypass source restrictions |

## Rights and privacy acceptance gates — not yet passed

This is a documentation review checklist, not a completed legal audit or an implemented application control. Existing technical tests do not establish legal permission.

| Gate | Evidence required before the relevant activity |
|---|---|
| Personal feedback/recruitment | Named operator/contact; defined purpose, minimum data, lawful basis, notice, retention, recipients, rights and incident process; jurisdiction and transfer/localization assessment from [PRIVACY.md](PRIVACY.md) |
| Live/captured test material | Documented permitted use under applicable law and source terms, with permissions/consents where required; no access-control bypass, unpublished personal conversations or unauthorized audio uploads |
| Contest records/entry | Current official rules, organizer and destination, dates/timezone, age/location, fees and method; verification date/provenance and expiry; no assurance of eligibility or organizer acceptance |
| Models and dependencies | Exact distributed component/version inventory; applicable licenses, required license/NOTICE/attribution and modification notices checked inside the eventual artifact |
| Public distribution | Separate owner authorization plus resolved security/privacy/signing/store and rights gates; public documentation alone does not authorize a binary release |

The official [Vosk model list](https://alphacephei.com/vosk/models) identifies small English 0.15 and small Russian 0.22 as Apache-2.0; it does not license radio content or prove all packaged dependencies are compliant. Check the [Apache-2.0 redistribution conditions](https://www.apache.org/licenses/LICENSE-2.0.html), including the license, retained notices and any applicable NOTICE content. Its trademark clause does not grant a general branding license. No complete packaged-notice audit was performed here.

The [Canadian Copyright Act](https://laws-lois.justice.gc.ca/eng/acts/C-42/FullText.html) separately addresses broadcaster/recording rights and conditional exceptions. No blanket personal-use or accessibility exception is asserted for this application's capture, captions or redistribution, in Canada or elsewhere. Obtain an assessment of the actual use and applicable jurisdiction.

Synthetic material is preferred, but still check its text, voice/service terms and sharing rights. Label fixtures clearly. These sources were consulted for this correction; no broadcaster permission, legal opinion or new device test is implied.

## Feedback and release gate

The template in [CONTRIBUTING.md](CONTRIBUTING.md) is for future arranged tests only after the privacy-intake gates above are resolved. Testing is voluntary; do not ask for hearing diagnoses, real contest entry, payment, bank details or unconsented recordings. Keep private artifacts out of public scanners or share links unless specifically authorized.

A future public beta needs resolved security/signing/SDK/privacy gates, recorded device/accessibility results and explicit owner publication approval. Neither this plan nor past host successes authorize distribution. See [ROADMAP.md](ROADMAP.md).
