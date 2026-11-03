# WePlay AutoDraw

Native Kotlin Android app that converts a gallery photo into a strict black-and-white line drawing and can optionally send drawing paths to a user-selected WePlay app through Android Accessibility Service.

## Build & Operate

- `cd android/weplay-autodraw && ./gradlew copyDebugApk` — build and copy the installable debug APK
- Minimum supported OS: Android 9 (API 28)
- APK output: `generated-artifacts/WePlay-AutoDraw-debug.apk`
- `android/weplay-autodraw/README.md` contains setup, service-consent, and use instructions.

## Stack

- Kotlin, Android Gradle Plugin 8.7.3, Gradle 8.9
- Android SDK Platform 35; minSdk 28
- ML Kit face contours and on-device binary edge extraction
- No backend or photo upload

## Where things live

- `android/weplay-autodraw/app/src/main` — Android manifest, accessibility-service configuration, and Kotlin app code
- `android/weplay-autodraw/README.md` — build, setup, consent, and installation instructions

## Architecture decisions

- Photos are processed on-device and are never uploaded.
- The service does not read window content. It checks the selected app package, lets the user position and resize a drawing-area overlay, and requires a separate explicit start tap before sending gestures.
- A real-device attempt showed the Android gesture counter increasing and screen activity, but no visible drawing in WePlay. Android gesture completion does not prove WePlay accepted the strokes.

## Product

Choose a gallery photo, preview and tune a black-and-white line drawing, then optionally send its paths to the selected WePlay app.

## User preferences

- Never claim WePlay control works until it has been tested with the real app.

## Gotchas

- Enable the Accessibility Service manually in Android settings; Android 9 (API 28) is the minimum.
- Stop immediately prevents later strokes; an in-flight touch may finish within 300 ms.

## Pointers

- See `android/weplay-autodraw/README.md` for instructions and limitations.
