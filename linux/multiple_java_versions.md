# Linux Help
---

## Installing and Using Multiple Versions of Java, Manually on Arch Linux

Let's say you need to Android something fierce. Let's say you're cheap. You have an outdated API that needs to use a completely different JDK version than the current version. Arch acts a bit different.

### Install a Previous OpenJDK/OpenJRE
If you are devving, use `pacman -S jdk#-openjdk` where `#` is the java version number you want. I'm doing Android 7.0 dev work, so I needs the `jdk8-openjdk`

`pacman -S jdk8-openjdk`

### Defaulting to A Specific Java Installation Manually
Arch uses `/usr/lib/jvm/default` and `/usr/lib/jvm/default-runtime/` symlinks to determine the default java stuff you use when you type `java --version`. Exporting or setting `JAVA_HOME` is pointless, as Arch uses the default symlinks. If you think `JAVA_HOME` does it, then why does setting it to `java-8-openjdk` have `java --version` do this?  
`java --version`
> ```
openjdk 10.0.1 2018-04-17
OpenJDK Runtime Environment (build 10.0.1+10)
OpenJDK 64-Bit Server VM (build 10.0.1+10, mixed mode)
```

Simply update the symlinks for your default java install if you want to persistently use java 8 instead of 10 for the current project, though Arch comes with a simple tool to update the symlinks for you.

### Defaulting to A Specific Java Installation with `archlinux-java`
Simple enough, install with `pacman` or copy your unzipped java version to `/usr/lib/jvm/` then simply run:  
`sudo archlinux-java set <myJavaVersion>` where `<myJavaVersion>` is the name of the java folder you wish to use.
