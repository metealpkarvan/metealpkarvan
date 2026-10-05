# Mac compatibility & verification

Updated 2026-10-05. This record covers the fifteen projects in the [catalogue](PROJECTS.md). It distinguishes processor support, automated checks and physical device testing.

## Supported delivery paths

| Projects | Delivery | Intel Mac | Apple Silicon Mac |
| --- | --- | --- | --- |
| [Pati Cepte](https://github.com/metealpkarvan/touch-bar-pet), [Şerit](https://github.com/metealpkarvan/touch-bar-post), [Mazi Sandığı](https://github.com/metealpkarvan/mazi-sandigi), [Touch Bar Arcade](https://github.com/metealpkarvan/touch-bar-arcade), [Run Receipt](https://github.com/metealpkarvan/run-receipt) | Native Universal macOS apps | x86_64, macOS 11+ | Native arm64, macOS 11+ |
| [Link Loom](https://github.com/metealpkarvan/link-loom), [Context Capsule](https://github.com/metealpkarvan/context-capsule), [Veil Paste](https://github.com/metealpkarvan/veil-paste), [Claim Lantern](https://github.com/metealpkarvan/claim-lantern), [Return Ticket](https://github.com/metealpkarvan/return-ticket), [Trial Tally](https://github.com/metealpkarvan/trial-tally), [Patch Atlas](https://github.com/metealpkarvan/patch-atlas), [Later Lane](https://github.com/metealpkarvan/later-lane), [Reply Harbor](https://github.com/metealpkarvan/reply-harbor) | HTML / CSS / JavaScript browser apps | Modern browser | Modern browser |
| [Run Receipt](https://github.com/metealpkarvan/run-receipt) | Standalone HTML and optional Node CLI | Modern browser; CLI with supported Node 20+ | Modern browser; CLI with supported native Node 20+ |
| [Ship Notes](https://github.com/metealpkarvan/ship-notes) | Python CLI, no compiled extensions | Native Python 3.9+ and Git | Native Python 3.9+ and Git |

Rosetta is not required for these delivery paths. Browser apps do not need processor-specific binaries. Node.js is used for development checks; follow each release's instructions to run downloaded browser files. Modern development toolchains may require a newer macOS than an app's deployment target.

## Native apps

The five Mac apps compile x86_64 and arm64 executables into a Universal binary with Apple's `lipo`. Packaging checks verify both architectures and ad-hoc signatures. Core behavior and AppKit integration checks run on native Intel and Apple Silicon hosts.

| Application | Published verification run |
| --- | --- |
| Pati Cepte | [180 core + 73 AppKit checks; native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-pet/actions/runs/37320771529) |
| Şerit | [1.2.0: 71 core + 44 AppKit checks passed on native Intel and arm64](https://github.com/metealpkarvan/touch-bar-post/actions/runs/37369937036) · [Universal release verified locally; public Intel download passed 44 AppKit checks](https://github.com/metealpkarvan/touch-bar-post/releases/tag/v1.2.0) |
| Run Receipt | [56 core/CLI tests + 29 WebKit checks per delivery surface on native Intel and arm64](https://github.com/metealpkarvan/run-receipt/actions/runs/37365734051) · [Universal release verified locally](https://github.com/metealpkarvan/run-receipt/releases/tag/v1.0.0) |
| Mazi Sandığı | [Native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/mazi-sandigi/actions/runs/37265016759) |
| Touch Bar Arcade | [Native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-arcade/actions/runs/37259185558) |

Pati Cepte stores completed pet progress, world settings, owned decorations and adventure progress in Application Support, with atomic saves and previous-record recovery. Version-1 saves migrate forward to version 2 without losing existing pet progress; old apps cannot read the new format. Acceptance checks also exercised an extracted Universal release package.

Şerit [1.2.0](https://github.com/metealpkarvan/touch-bar-post/releases/tag/v1.2.0) keeps several saved notes in one editor/list and remembers both the selected message and a global 240–560-point strip-width preference, default 400. Version-1 archives and existing message metadata are preserved. Native Intel and arm64 CI jobs each passed 71 core and 44 AppKit checks. The local Universal package and its Intel acceptance harness were verified before publication. An anonymous download of the public ZIP matched its SHA256 manifest and source guides, contained both processor slices targeting macOS 11, passed strict signature verification and passed all 44 AppKit checks on Intel. [Source verification details](https://github.com/metealpkarvan/touch-bar-post/blob/v1.2.0/docs/VERIFICATION.md) describe the harness and its testing limits.

Şerit uses the public Touch Bar API while the app is frontmost; its window strip supports Macs without the hardware. macOS owns the Control Strip and may compress the requested message width to the available app space.

Run Receipt opens user-selected logs in a local WebKit window. The source UI and standalone HTML each passed 27 page checks plus two native export bridge checks on both native Mac architectures. The public Universal download was rechecked for its version, signature, both processor slices and the 29 packaged integration checks. The Node CLI also has Linux and Windows coverage; Windows skips one Unix symlink test.

**Testing limits:** physical Touch Bar finger input, ergonomics, every Mac model and every older macOS version have not been verified. Actual notification delivery for Şerit remains a documented device check. macOS 11 is a deployment target. The apps are **ad-hoc signed and not Apple notarized**; use the first-launch instructions in each repository.

[Apple: Building a universal macOS binary](https://developer.apple.com/documentation/apple-silicon/building-a-universal-macos-binary)

## Browser tools & CLI

All nine browser projects run rule checks with native Node.js on Intel and arm64 macOS runners. These checks establish compatibility of their rules and builds; browser acceptance records separately identify exercised engines and viewports.

Patch Atlas, Later Lane and Reply Harbor ZIPs open directly through `index.html` without Node.js or a local server. Local-file startup, sample interaction and record creation were checked with Chromium and an Intel macOS WKWebView harness. Their live apps passed offline reopening checks in Chromium. Native arm64 CI checks the rules and standalone build separately.

Ship Notes installs and runs its CLI on both Mac architectures, with Linux and Windows coverage retained.

| Project | Native Mac verification |
| --- | --- |
| Link Loom | [Both Mac jobs passed](https://github.com/metealpkarvan/link-loom/actions/runs/37264515440) |
| Context Capsule | [Both Mac jobs passed](https://github.com/metealpkarvan/context-capsule/actions/runs/37264518508) |
| Veil Paste | [Both Mac jobs passed](https://github.com/metealpkarvan/veil-paste/actions/runs/37264521936) |
| Claim Lantern | [Both Mac jobs passed](https://github.com/metealpkarvan/claim-lantern/actions/runs/37264525294) |
| Return Ticket | [Both Mac jobs passed](https://github.com/metealpkarvan/return-ticket/actions/runs/37264528032) |
| Trial Tally | [Both Mac jobs passed](https://github.com/metealpkarvan/trial-tally/actions/runs/37264530683) |
| Patch Atlas | [Both Mac jobs passed](https://github.com/metealpkarvan/patch-atlas/actions/runs/37288282047) |
| Later Lane | [Both Mac jobs passed](https://github.com/metealpkarvan/later-lane/actions/runs/37288309717) |
| Reply Harbor | [Both Mac jobs passed](https://github.com/metealpkarvan/reply-harbor/actions/runs/37288331565) |
| Ship Notes | [Both Mac jobs passed](https://github.com/metealpkarvan/ship-notes/actions/runs/37264534136) |

**Türkçe:** Beş Mac uygulaması Intel ve Apple Silicon sürümlerini aynı pakette içerir. Tarayıcı uygulamaları modern bir tarayıcıda, Ship Notes ise Python 3.9+ ve Git ile çalışır. Run Receipt ayrıca tek HTML dosyası ve isteğe bağlı Node 20+ CLI sunar. Yukarıdaki bağlantılar gerçek test kayıtlarına gider; fiziksel Touch Bar ve eski macOS sürümlerindeki test sınırları ayrıca belirtilmiştir.
