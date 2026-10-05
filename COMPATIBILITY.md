# Mac compatibility & verification

Updated 2026-10-05. This record covers the fourteen projects in the [catalogue](PROJECTS.md). It distinguishes processor support, automated checks and physical device testing.

## Supported delivery paths

| Projects | Delivery | Intel Mac | Apple Silicon Mac |
| --- | --- | --- | --- |
| [Pati Cepte](https://github.com/metealpkarvan/touch-bar-pet), [Şerit](https://github.com/metealpkarvan/touch-bar-post), [Mazi Sandığı](https://github.com/metealpkarvan/mazi-sandigi), [Touch Bar Arcade](https://github.com/metealpkarvan/touch-bar-arcade) | Native Universal macOS apps | x86_64, macOS 11+ | Native arm64, macOS 11+ |
| [Link Loom](https://github.com/metealpkarvan/link-loom), [Context Capsule](https://github.com/metealpkarvan/context-capsule), [Veil Paste](https://github.com/metealpkarvan/veil-paste), [Claim Lantern](https://github.com/metealpkarvan/claim-lantern), [Return Ticket](https://github.com/metealpkarvan/return-ticket), [Trial Tally](https://github.com/metealpkarvan/trial-tally), [Patch Atlas](https://github.com/metealpkarvan/patch-atlas), [Later Lane](https://github.com/metealpkarvan/later-lane), [Reply Harbor](https://github.com/metealpkarvan/reply-harbor) | HTML / CSS / JavaScript browser apps | Modern browser | Modern browser |
| [Ship Notes](https://github.com/metealpkarvan/ship-notes) | Python CLI, no compiled extensions | Native Python 3.9+ and Git | Native Python 3.9+ and Git |

Rosetta is not required for these delivery paths. Browser apps do not need processor-specific binaries. Node.js is used for development checks; follow each release's instructions to run downloaded browser files. Modern development toolchains may require a newer macOS than an app's deployment target.

## Native apps

The four Mac apps compile x86_64 and arm64 executables into a Universal binary with Apple's `lipo`. Packaging checks verify both architectures and ad-hoc signatures. Core behavior and AppKit integration checks run on native Intel and Apple Silicon hosts.

| Application | Published verification run |
| --- | --- |
| Pati Cepte | [128 core + 44 AppKit checks; native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-pet/actions/runs/37312113310) |
| Şerit | [44 core + 21 AppKit checks; native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-post/actions/runs/37297187041) |
| Mazi Sandığı | [Native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/mazi-sandigi/actions/runs/37265016759) |
| Touch Bar Arcade | [Native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-arcade/actions/runs/37259185558) |

Pati Cepte stores completed pet progress in Application Support, with atomic saves and previous-record recovery. Acceptance checks also exercised an extracted Universal release package. Şerit uses the public Touch Bar API while the app is frontmost; its desktop strip supports Macs without the hardware.

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

**Türkçe:** Dört Mac uygulaması Intel ve Apple Silicon sürümlerini aynı pakette içerir. Tarayıcı uygulamaları modern bir tarayıcıda, Ship Notes ise Python 3.9+ ve Git ile çalışır. Yukarıdaki bağlantılar gerçek test kayıtlarına gider; fiziksel Touch Bar ve eski macOS sürümlerindeki test sınırları ayrıca belirtilmiştir.
