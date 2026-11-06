# EVCseven — Android Video Editor

- **GitHub repository:** `EVCseven`
- **Application label:** `EVCseven`
- **Project version:** `0.2.196` (`versionCode 396`)
- **Application ID / Kotlin package:** `com.evc.app` (intentionally unchanged to preserve app identity)
- **Native ABI:** `armeabi-v7a` only (32-bit ARM / ARMv7)

## Project configuration

- Android module: `app`
- Gradle root project: `EVCseven`
- Minimum Android SDK: 24
- Compile / target SDK: 35
- Java and Kotlin JVM target: 17
- Debug shrinking: disabled

## Git setup (MGit)

This ZIP is a clean project import. It intentionally contains **no `.git` directory, remote URL, branch metadata, or previous commit history**. No remote has been selected or configured for this project.

1. Extract this ZIP and open the single folder `EVCseven` in MGit (the folder containing `settings.gradle.kts`).
2. Initialize a new Git repository in that folder only when you are ready, and choose your preferred branch name.
3. Stage all files, including the hidden `.github/workflows/android.yml` file, then create the initial commit.
4. Leave the remote unset for now. Choose and configure a GitHub remote yourself later, when you decide which repository should receive the project.
5. After you have deliberately configured a remote and pushed the commit, open **Actions** on that repository and check the `EVCseven Android Build` workflow.

### If the Commit appears but Actions does not start

- In the GitHub **Code** tab, confirm the latest commit is on the branch you pushed and `.github/workflows/android.yml` is present.
- The workflow listens for pushes and pull requests on all branches (`"**"`) and supports manual execution (`workflow_dispatch`).
- In repository **Settings → Actions → General**, confirm Actions are enabled and the repository policy permits the workflow's actions.
- Check the workflow file for YAML errors if GitHub does not list it. A workflow cannot be triggered by a commit if the file is absent from that commit or Actions are disabled by repository policy.

## ARMv7 FFmpeg build

The app uses a local FFmpegKit AAR built by GitHub Actions for `armeabi-v7a`. The workflow builds from maintained source tag `v6.0.4-lts-android` using Android NDK `27.2.12479018`, with Android API level 24. The build script is expected at `android-6.0-lts/android.sh`; the workflow checks this path and the NDK compiler before building.

The workflow passes FFmpegKit arguments as a Bash array, expects exactly one generated AAR, copies it to `app/libs/ffmpeg-kit-full.aar`, and verifies that the archive contains ARMv7 native libraries without 64-bit or x86 ABIs. This AAR is generated during CI and is not committed in the source ZIP.

## Existing behavior and constraints retained

- Existing application source and Kotlin package are preserved.
- `applicationId` remains `com.evc.app` to avoid changing the app's installation identity.
- Native ABI remains restricted to `armeabi-v7a`.
- Minimum SDK remains 24; Java and Kotlin targets remain 17.
- The current Split implementation and its existing safeguards are retained without feature changes.
- The workflow builds the native FFmpegKit dependency before running `assembleDebug` and uploads the resulting debug APK as an artifact.

## Verification status

This package cleanup updates repository-facing names and removes the old Git metadata. It does **not** claim that the remote GitHub Actions build or on-device behavior has passed. Confirm both from the first EVCseven Actions run and an installation/test on the target Android device.
