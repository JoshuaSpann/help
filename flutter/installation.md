# Flutter Help
---

## Installing without Android Studio
### Setup Environment Variables
In your `~/.bashrc` file or the like, set your `$ANDROID_HOME` variable: to the location of your Android SDK folder. In this case it is in `~/android_sdk`:  
`ANDROID_HOME=/home/user/android_sdk/`

You may want to set your android binary folder for running some android tools like sdkmanager:  
`ANDROID_BIN=/home/user/android_sdk/tools/bin`

### Use Android SDK Tools to Install Requisites
Since flutter requires the sdk, platform tools,and  build tools install the platform and build tools:  
`sdkmanager "platform-tools" "build-tools;26.0.3" "platforms;android-26"`

Install gradle via your package manager or the binary executable, then config flutter:  
`flutter config --gradle-dir /usr/bin/gradle`  
> `Setting "gradle-dir" value to "/usr/bin/gradle".`

Don't allow spying:  
`flutter config --no-analytics`

---
## Resources
- [Setting up Flutter without Android Studio](https://medium.com/@aubykhan/setting-up-flutter-without-android-studio-6f7abdeb353c)
