# LineageOS_android_packages_apps_build-guide

to get started, you'll need:
- internet
- 64 GB minimum storage
- 16 GB minimum RAM
- Git
- [TemurinJDK 17 and 21 from Adoptium](https://adoptium.net/temurin/releases)
- Gradle (or use the .\gradlew wrapper)
- [SDK build tools](https://developer.android.com/tools/releases/build-tools): skip if you have Android Studio installed
- [uber-apk-signer](https://github.com/patrickfav/uber-apk-signer): crucial for signing the final outputs

# how to build
### 1. clone the repository

only clone repos with branches that has `build.gradle` or `build.gradle.kts`. if it doesn't, it requires the full AOSP build system and will not work standalone with this guide. i recommend using anything more than the lineage-21.0 branch for stability.

example: ExactCalculator with the lineage-23.2 branch
```bash
git clone -b lineage-23.2 https://github.com/lineageos/android_packages_apps_ExactCalculator

cd android_packages_apps_ExactCalculator
```
### 2. compile source

for MacOS/Linux users: grant permissions first:
```bash
chmod +x gradlew
```   

run the Gradle wrapper inside the folder to start building:
```bash
./gradlew assembleRelease
```
(if you are using Windows PowerShell, run .\gradlew assembleRelease instead)

the output is in app/build/outputs/apk/release/

### 3. sign the package

run uber-apk-signer from your root directory:
```bash
java -jar uber-apk-signer.jar --apks app/build/outputs/apk/release/
```
the output is the same as 2.

# troubleshooting

### SDK location not found

- create a local.properties file in the root directory, then define your SDK path.

Windows:
```bash
sdk.dir=C:\Users\username here\AppData\Local\Android\Sdk
```
Linux/MacOS:
```bash
sdk.dir=/home/username here/Android/Sdk
```

### Java version mismatch

- ensure environment variables point to TermurinJDK 8, 11, 17 or 21.
- in the terminal, check the active version:
```bash
java -version
```

# apks

if you want to try using these apks built from pure LineageOS source, they are available in the releases page.

# credits
- The LineageOS Team
- marcone
- patrickfav
- The Adoptium Working Group

---
notes from arimotofu:

*i can't guarantee if these works on Linux/MacOS so feel free to try and commit changes :P
