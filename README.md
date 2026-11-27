# LG TV Remote Android
Native Android project for LG webOS 32LM636BPTB, using the bundled website UI. No website hosting or Node server is required for Android.

## Build without Android Studio
Create a GitHub repository and push the contents of this folder, including the hidden .github directory. Open Actions > Build Android APK > Run workflow. Once successful, open the run and download LG-TV-Remote-APK from Artifacts. Extract app-debug.apk and install it on your Android phone. Android may ask permission to install from your file manager. The APK is debug-signed, not a Play Store release.

Connect phone and TV to the same trusted Wi-Fi, enter the TV private IPv4 address and accept pairing on TV. The TV uses self-signed TLS; this prototype does not authenticate its certificate, so use only a trusted network. Wake-on-LAN requires TV support and MAC address. JioHotstar requires an installed compatible TV app and app-list permissions. Physical TV testing and APK compilation have not been performed here.
