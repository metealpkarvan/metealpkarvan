# Intel and Apple Silicon support

Updated 2026-10-05. These are the thirteen portfolio projects developed in this work. Compatibility depends on the delivery format; a browser project does not need a processor-specific application binary.

| Project | Delivery | Intel Mac | Apple Silicon Mac |
| --- | --- | --- | --- |
| [Şerit · Touch Bar Post](https://github.com/metealpkarvan/touch-bar-post) | Native macOS app | x86_64 in Universal package, macOS 11+ | Native arm64 in the same package, macOS 11+ |
| [Mazi Sandığı](https://github.com/metealpkarvan/mazi-sandigi) | Native macOS app | x86_64 in Universal package, macOS 11+ | Native arm64 in the same package, macOS 11+ |
| [Touch Bar Arcade](https://github.com/metealpkarvan/touch-bar-arcade) | Native macOS app | x86_64 in Universal package, macOS 11+ | Native arm64 in the same package, macOS 11+ |
| [Link Loom](https://github.com/metealpkarvan/link-loom) | Browser app and source | Modern browser | Modern browser |
| [Context Capsule](https://github.com/metealpkarvan/context-capsule) | Browser app and runnable static ZIP | Modern browser | Modern browser |
| [Veil Paste](https://github.com/metealpkarvan/veil-paste) | Browser app and runnable static ZIP | Modern browser | Modern browser |
| [Claim Lantern](https://github.com/metealpkarvan/claim-lantern) | Browser app and runnable static ZIP | Modern browser | Modern browser |
| [Return Ticket](https://github.com/metealpkarvan/return-ticket) | Browser app and runnable static ZIP | Modern browser | Modern browser |
| [Trial Tally](https://github.com/metealpkarvan/trial-tally) | Browser app and runnable static ZIP | Modern browser | Modern browser |
| [Patch Atlas](https://github.com/metealpkarvan/patch-atlas) | Browser app and standalone ZIP | Modern browser | Modern browser |
| [Later Lane](https://github.com/metealpkarvan/later-lane) | Browser app and standalone ZIP | Modern browser | Modern browser |
| [Reply Harbor](https://github.com/metealpkarvan/reply-harbor) | Browser app and standalone ZIP | Modern browser | Modern browser |
| [Ship Notes](https://github.com/metealpkarvan/ship-notes) | Python CLI, no compiled extensions | Native Python 3.9+ and Git | Native Python 3.9+ and Git |

Rosetta is not required for these supported delivery paths. The browser apps' runtime files are HTML/CSS/JavaScript; Node.js is needed only for development tests/build steps. Python 3 can serve a downloaded static ZIP locally. Modern toolchains may require a newer macOS than a native app's deployment target.

## Verification boundaries

All three native applications compile x86_64 and arm64 executables into one Universal binary using Apple's lipo tool. Packages verify architecture presence and ad-hoc signing and run actual AppKit smoke checks. Native CI runs rule and UI integration checks on Intel and Apple Silicon hosts. Physical Touch Bar finger sensitivity and every Mac model are separate hardware checks.

All nine browser projects run their rule checks with native Node.js on Intel and arm64 macOS runners. This checks architecture compatibility of the rules and build, not every browser/device combination. Existing browser acceptance records separately describe the engines and viewports exercised. Ship Notes installs and runs its CLI on both Mac architectures, with Linux and Windows coverage retained.

Patch Atlas, Later Lane and Reply Harbor ZIPs open directly through `index.html`; they require neither Node.js nor a local server for use. Local-file boot, sample interaction and record creation were checked with Chromium and a macOS WKWebView harness on Intel. Their live apps also passed offline reopening checks in Chromium. Native arm64 CI verifies the rules and standalone build separately from this browser acceptance.

Each repository's Actions tab contains the actual results. Universal macOS apps are ad-hoc signed for bundle integrity and are not Apple notarized; see their first-launch instructions. macOS 11 is a deployment target, not a claim of physical verification on every older OS.

[Apple: Building a universal macOS binary](https://developer.apple.com/documentation/apple-silicon/building-a-universal-macos-binary)

## Latest native Mac verification

- [Mazi Sandığı: native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/mazi-sandigi/actions/runs/37265016759).
- [link-loom: both Mac jobs passed](https://github.com/metealpkarvan/link-loom/actions/runs/37264515440).
- [context-capsule: both Mac jobs passed](https://github.com/metealpkarvan/context-capsule/actions/runs/37264518508).
- [veil-paste: both Mac jobs passed](https://github.com/metealpkarvan/veil-paste/actions/runs/37264521936).
- [claim-lantern: both Mac jobs passed](https://github.com/metealpkarvan/claim-lantern/actions/runs/37264525294).
- [return-ticket: both Mac jobs passed](https://github.com/metealpkarvan/return-ticket/actions/runs/37264528032).
- [trial-tally: both Mac jobs passed](https://github.com/metealpkarvan/trial-tally/actions/runs/37264530683).
- [ship-notes: both Mac jobs passed](https://github.com/metealpkarvan/ship-notes/actions/runs/37264534136).
- [touch-bar-arcade: both Mac jobs passed](https://github.com/metealpkarvan/touch-bar-arcade/actions/runs/37259185558).
- [patch-atlas: both Mac jobs passed](https://github.com/metealpkarvan/patch-atlas/actions/runs/37288282047).
- [later-lane: both Mac jobs passed](https://github.com/metealpkarvan/later-lane/actions/runs/37288309717).
- [reply-harbor: both Mac jobs passed](https://github.com/metealpkarvan/reply-harbor/actions/runs/37288331565).

- [Şerit: native Intel, native arm64 and Universal package passed](https://github.com/metealpkarvan/touch-bar-post/actions/runs/37297187041).

Şerit uses the public frontmost-app Touch Bar API. The shared desktop strip supports Macs without physical Touch Bar hardware. Its 44 core and 21 AppKit checks passed on both native CPU families; physical tap ergonomics and actual notification delivery remain documented device checks.
