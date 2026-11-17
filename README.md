# Secret Calculator Vault (Android starter)

A Kotlin + Jetpack Compose Android Studio project implementing a calculator-style PIN gate and an encrypted local file vault with separate Personal and Work *in-app* areas.

## Open and build
1. Install Android Studio (Koala or newer) and Android SDK 35.
2. Open this folder in Android Studio.
3. Allow Gradle sync, then run the `app` configuration on an Android 8.0+ device/emulator.

## Included in this starter
- Calculator-style entry screen; first launch sets a PIN (minimum 4 digits).
- AES-256-GCM encryption with a non-exportable Android Keystore key.
- Import arbitrary files through Android's system document picker.
- Separate Personal and Workspaces within app-private storage.
- Screenshot blocking while the app is open (`FLAG_SECURE`).
- Biometric authentication demonstration hook.
- App-private storage; imported originals are not deleted from their original locations.

## Important security and product limitations
- This is a starter implementation, not a production-ready HideU replacement.
- The current PIN is stored as a preference for prototype simplicity. Before release, replace this with a salted, memory-hard PIN verifier (Argon2id/scrypt where available) and rate limiting. Do not ship this prototype PIN storage unchanged.
- Biometric button is a demonstration and is not yet wired as a mandatory vault-unlock factor.
- Files are decrypted into the app cache only when opened by another app. Add timed cache cleanup, explicit export warnings, and robust temporary-file handling before release.
- The vault index is not encrypted in this starter; filenames and MIME metadata are visible inside the app sandbox. Encrypt/authenticate the index before production.
- Cloud backup, private browser, camera capture, image editing, audio/video in-app playback, decoy vault and recovery questions are not implemented yet.
- Android Work Profile provisioning is controlled by Android Enterprise / a device policy controller (DPC), the OS, and often an organization administrator. An ordinary consumer app cannot silently create, hide, or make a managed profile invisible in Settings. This project therefore provides a separate in-app Workspace. A compliant managed-profile/DPC integration would be a separate, explicitly provisioned enterprise module.
- Android launcher icon/name disguise must follow Google Play policies and must not be used to deceive users or evade device security controls.

## Before production release
Add PIN verifier + lockout, biometric-bound key authorization, encrypted index, secure media preview, scoped storage tests, backup/recovery design, accessibility, privacy policy, threat model, penetration testing, and Play policy review.
