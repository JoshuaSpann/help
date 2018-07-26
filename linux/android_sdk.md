# Linux Help
---

## Installing the Android SDK for Command-Line Use on Arch Linux

You may not want an entire IDE like Android Studio to bog down your computer and you may prefer using other utilities, such as VS Code or Vim.
You may find it more efficient to manage android projects from the command-line, in which case you can get the Command-Line Tools only.

### Getting the Command-Line Tools from Google
Go to the [developer site for Android](https://developer.android.com/studio/#command-tools) and locate the SDK for download. It'll be underneath the overly advertised Android Studio, probably under the name ["Command line tools only"](https://developer.android.com/studio/#command-tools). Once you have downloaded your appropriate zipfile for your OS (Linux), you may then unzip it to the directory of your choice.

### Setting up the Command-Line SDK Tools
Create a directory for the Android SDK:  
`mkdir ~/android_sdk`

Unzip the SDK tools to a folder of your choosing:  
`unzip sdk-tools-linux-#######.zip -d ~/android_sdk/`

Then ensure that it is in your `.bashrc`'s `$PATH` like so:  
```
ANDROID_BIN=~/android_sdk/tools/bin
PATH=$PATH:$ANDROID_BIN
```

Now, assuming you have Oracle's JDK 1.8 (version 8 of Java) installed, you should be able to run `sdkmanager --list` and whatnot without a hitch.
However, if you have a different version of Java, such as the OpenJDK or an Oracle JDK version > 8, you may need to install the appropriate JDK or hack yet another environment variable.
It will give you an error like this:  
'sdkmanager --list`
> ```
Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/annotation/XmlSchema
	at com.android.repository.api.SchemaModule$SchemaModuleVersion.<init>(SchemaModule.java:156)
	at com.android.repository.api.SchemaModule.<init>(SchemaModule.java:75)
	at com.android.sdklib.repository.AndroidSdkHandler.<clinit>(AndroidSdkHandler.java:81)
	at com.android.sdklib.tool.sdkmanager.SdkManagerCli.main(SdkManagerCli.java:73)
	at com.android.sdklib.tool.sdkmanager.SdkManagerCli.main(SdkManagerCli.java:48)
Caused by: java.lang.ClassNotFoundException: javax.xml.bind.annotation.XmlSchema
	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:582)
	at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:190)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:499)
	... 5 more
```


### Work with Different Java than Java 1.8
Edit your `~/.bashrc` file to allow the sdk to work with versions of Java other than Oracle's Java 1.8 (version 8):  
`export JAVA_OPTS='-XX:+IgnoreUnrecognizedVMOptions --add-modules java.se.ee'`

### Setting Up a Basic Environment
Use `sdkmanager --list` to see all available packages. Install some basics as below:  
`cd ~/android_sdk; sdkmanager "platform-tools" "build-tools;26.0.3" "platforms;android-26"`

Install gradle with your package manager.

---

## Resources
- [Android SDK is not installed or is not configured properly, environment looks ok #3139](https://github.com/NativeScript/nativescript-cli/issues/3139)
