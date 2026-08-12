# FactoryFlow Android Releases

This repository distributes signed Android APKs for FactoryFlow through **GitHub Releases**.
It does not contain the Flutter source code, signing keys, keystores, passwords, or APK binaries in Git history.

## Publish a release

1. In the FactoryFlow Flutter project, increase the app version in `pubspec.yaml`:

   ```yaml
   version: 1.0.1+2
   ```

   `1.0.1` is the user-visible version. `2` is Android's internal version code and must be greater than every previously published release.

2. Build the signed production APK:

   ```powershell
   flutter build apk --release
   ```

3. Open [Releases](../../releases) and choose **Draft a new release**.

4. Create a new tag matching the visible version, for example `v1.0.1`.

5. Use the release title `FactoryFlow 1.0.1`, attach the APK as `factoryflow-v1.0.1.apk`, and add concise release notes.

6. Publish the release, then copy the asset's direct URL. It should have this shape:

   ```text
   https://github.com/Zain1098/factoryflow_app_release_version/releases/download/v1.0.1/factoryflow-v1.0.1.apk
   ```

7. In the private FactoryFlow Platform Control Center, open **Mobile app releases** and publish the same version metadata:

   - Version name: `1.0.1`
   - Version code: `2`
   - Minimum supported version code: `1` for an optional update, or `2` to require this release
   - GitHub Release APK HTTPS URL: the copied asset URL
   - Release notes, mandatory-update flag, and optionally the APK SHA-256 checksum

The mobile app reads this metadata after sign-in and from Settings. It prompts for optional updates and blocks versions below the minimum supported code until the user installs the new APK.

## Release rules

- Keep this repository public if the app must download APKs without GitHub authentication.
- Never commit APKs, `.jks`/`.keystore` files, `key.properties`, passwords, or Flutter source here.
- Test the download and installation on a physical Android device before publishing release metadata in the dashboard.
- Android requires the user's confirmation to install an APK; the app cannot silently update itself.
- Do not delete or replace a published APK asset. Publish a new tag and a higher version code instead.

## Suggested release notes

```markdown
## What's new
- Brief user-facing change

## Required action
- Optional update / Update required before continuing
```
