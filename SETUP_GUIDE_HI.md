# LG TV Remote - Windows Setup & APK Build Guide

## Project requirements
- Windows 10/11
- Android Studio (latest stable)
- JDK 17 (Android Studio can use its bundled JBR)
- Android SDK Platform 35
- Gradle 8.9 (only needed once to generate the Gradle Wrapper if it is not already present)
- Android phone running Android 7.0 or newer
- LG webOS TV and phone on the same private Wi-Fi network

## 1. Extract and open
1. Extract `LGRemoteAndroid.zip` to a simple path, for example `C:\Projects\LGRemoteAndroid`.
2. Open Android Studio.
3. Select **Open** and choose the extracted `LGRemoteAndroid` folder (the folder containing `settings.gradle`).
4. Wait for Gradle sync. If Android Studio asks to install Android SDK Platform 35 or Build Tools, accept the installation.
5. Open **File > Settings > Build, Execution, Deployment > Build Tools > Gradle**.
6. Set **Gradle JDK** to Android Studio's bundled JDK 17 (or another installed JDK 17).

## 2. Generate the Gradle Wrapper (one-time, because this ZIP has no wrapper)
Open Android Studio's Terminal at the project root. First check that Gradle is installed:

```bat
gradle --version
```

If the command is not found, install Gradle 8.9 and add its `bin` folder to Windows PATH, then reopen the terminal. Run:

```bat
gradle wrapper --gradle-version 8.9
```

This should create `gradlew`, `gradlew.bat`, and the `gradle/wrapper` folder. Keep these files in the project for future builds.

## 3. Build the debug APK
From the project root in Android Studio Terminal, run:

```bat
.\gradlew.bat assembleDebug
```

If the build succeeds, the APK will be here:

```text
app\build\outputs\apk\debug\app-debug.apk
```

## 4. Install on your Android phone
Option A - USB:
1. Enable Developer options and USB debugging on the phone.
2. Connect the phone to the PC and approve the debugging prompt.
3. Run:

```bat
.\gradlew.bat installDebug
```

Option B - APK file:
1. Copy `app-debug.apk` to your phone.
2. Open it and allow **Install unknown apps** for the file manager/browser if Android asks.
3. Install and launch **LG TV Remote**.

## 5. Connect to the LG TV
1. Connect the phone and LG TV to the same home Wi-Fi network. Avoid guest Wi-Fi or client isolation.
2. Find the TV's local IPv4 address in the TV network settings.
3. Open the app and enter the TV IP address, e.g. `192.168.1.100`.
4. Tap **Connect TV**.
5. Accept the pairing prompt on the TV. Keep the app open while pairing.
6. Test Home, arrows, OK, Back, Volume and Mute.
7. For Wake-on-LAN, enter the TV's MAC address. Wake may not work unless the TV/network supports wake from standby and the relevant TV setting is enabled.

## 6. Troubleshooting
- **Gradle sync/build fails:** confirm JDK 17, SDK Platform 35, internet access for dependency downloads, and Gradle 8.9 wrapper.
- **Cannot connect:** verify the TV IP, same Wi-Fi, no guest-network isolation, and that the TV is powered on.
- **Pairing does not appear:** restart the TV/app and retry; check whether the TV's webOS version and model support the used remote-control protocol.
- **Some buttons do not work:** app commands depend on TV model, webOS version, installed apps and supported SSAP APIs.
- **Wake does not work:** many TVs disable network wake in standby; confirm TV settings, MAC address and router behavior.

## Important limitations / security note
- The supplied source says it has not been compiled or tested against a physical TV. A successful APK build does not prove every remote command works on your TV.
- The Java code currently trusts all TLS certificates for the TV's secure WebSocket connection and permits cleartext traffic. Use only on a trusted private home network. Do not use this app on public/shared Wi-Fi without correcting certificate validation.
- This project does not include a cloud service or internet-based remote control; it is designed for local-network control.
