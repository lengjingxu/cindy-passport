<p align="right"><a href="README.zh_CN.md">简体中文</a> · <strong>English</strong></p>

# Cindy Passport

Turn [AI Passport](https://ai-passport.folotoy.cn) into a pocket companion for Cindy: see task status, read replies, record a response, check the transcription, and confirm sending it to the original task.

<img src="assets/images/cindy-passport-cover.png" width="420" alt="UI illustration: task status and reviewed voice replies" />

## What is AI Passport?

AI Passport is FoloToy's open-source wearable device with a screen, buttons, microphone and speaker. It runs replaceable firmware and community applications. This repository contains independent Cindy firmware, derived from the [official board template](https://github.com/FoloToy/ai-passport).

- [Official community and applications](https://ai-passport.folotoy.cn)
- [Official hardware/source repository](https://github.com/FoloToy/ai-passport)
- [Cindy](https://github.com/makecindy/cindy)
- [Cindy companion PR #4360](https://github.com/makecindy/cindy/pull/4360) — pending upstream review; use the PR branch until it is included in a Cindy release.
- [Firmware v0.1.0](https://github.com/lengjingxu/cindy-passport/releases/tag/v0.1.0-cindy-passport). Community submission: project 313, revision 516, pending review (not publicly approved).

## Use it

1. Install the matching Cindy companion on your Mac and enable Cindy Passport under Settings → Shortcuts → Accessories.
2. Open **Cindy BLE** on AI Passport. Select the device in Cindy and enter the pairing code if requested.
3. Use UP/DOWN to select a task and OK to enter. UP/DOWN pages through Cindy's latest reply; OK records a response.
4. Press OK again to stop. The device shows the transcription: UP records again, DOWN reads its pages, and OK confirms sending to the original task.
5. Hold OK to leave. Unconfirmed recordings are discarded; an already submitted message continues normally.

Speech recognition follows Cindy's configured voice-input service and ASR model. Credentials stay on the Mac. Firmware and companion must be updated together; installing unmodified Cindy does not imply this integration is available yet.

## Firmware and build

Download the checked complete image from [Releases](https://github.com/lengjingxu/cindy-passport/releases). The default build has no personal Wi-Fi credentials or device identity data.

Target: ESP32-C3, 8 MB Flash, no PSRAM, ESP-IDF 5.5.3. The application is limited to 3 MB; the protected `cardid` partition remains at `0x356000`.

```sh
# Activate your ESP-IDF 5.5.3 environment first.
./tools/validate.sh
```

The complete gate produces `build/FoloToy-AI-Passport-full.bin`. On an already provisioned device, follow [segmented flashing instructions](docs/development/engineering/protected-flash-layout.md); a raw complete-image write may overwrite pairing data. Never erase Flash or overwrite `cardid` merely to update Cindy.

See [interaction and protocol](docs/development/engineering/cindy-device.md) and [hardware guide](docs/hardware-design/AI_HARDWARE_DEVELOPMENT_GUIDE.md). This standalone repository does not belong to GitHub's fork network; the original FoloToy license and attribution are retained.

## License

Firmware derives from FoloToy AI Passport under the [MIT license](LICENSE). The embedded Noto font has its own [SIL Open Font License](assets/fonts/OFL.txt). Generated UI illustrations are marked as illustrations and are not device screenshots.
