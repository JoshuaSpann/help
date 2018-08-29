# Linux Help
---

## Installing Kotlin Native Compiler on Arch Linux

### Get and Extract the Git Repo
`git clone https://github.com/JetBrains/kotlin-native` or go to the [releases GitHub page](https://github.com/JetBrains/kotlin-native/releases) and download the linux `.tar.gz` (my version is 0.8.1)

From the `tar` file, simply extract it to your desired install location:  
`tar -xvf ~/Downloads/kotlin-native-linux-0.8.1.tar.gz -C ~/apps_dir/`

Add the bin folder to your `PATH`, I like my `~/.bashrc` for this:  
```
export KOTLIN_NATIVE_BIN=/home/<user>/apps_dir/kotlin-native-linux-0.8.1/bin/
PATH=$PATH:$KOTLIN_NATIVE_BIN
```

### Fixing `` Error
You run `kotlinc-native test.kt -o test` and you get this:  

```
/home/<user>/.konan/dependencies/clang-llvm-5.0.0-linux-x86-64/bin/llvm-lto: error while loading shared libraries: libtinfo.so.5: cannot open shared object file: No such file or directory
error: compilation failed: The /home/<user>/.konan/dependencies/clang-llvm-5.0.0-linux-x86-64/bin/llvm-lto command returned non-zero exit code: 127.
                                                                                                                                                                                                                                              
 * Source files: test.kt
 * Compiler version info: Konan: 0.8.1 / Kotlin: 1.2.70
 * Output kind: PROGRAM
                                                                                                                                                                                                                                              
exception: org.jetbrains.kotlin.konan.KonanExternalToolFailure: The /home/<user>/.konan/dependencies/clang-llvm-5.0.0-linux-x86-64/bin/llvm-lto command returned non-zero exit code: 127.
        at org.jetbrains.kotlin.konan.exec.Command.handleExitCode(ExecuteCommand.kt:100) 
        at org.jetbrains.kotlin.konan.exec.Command.execute(ExecuteCommand.kt:66) 
        at org.jetbrains.kotlin.backend.konan.LinkStage.runTool(LinkStage.kt:55) 
        at org.jetbrains.kotlin.backend.konan.LinkStage.runTool(LinkStage.kt:51) 
        at org.jetbrains.kotlin.backend.konan.LinkStage.llvmLto(LinkStage.kt:71) 
        at org.jetbrains.kotlin.backend.konan.LinkStage.access$llvmLto(LinkStage.kt:29) 
        at org.jetbrains.kotlin.backend.konan.LinkStage$linkStage$1.invoke(LinkStage.kt:240) 
        at org.jetbrains.kotlin.backend.konan.LinkStage$linkStage$1.invoke(LinkStage.kt:29) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager$phase$$inlined$with$lambda$1.invoke(KonanPhases.kt:139) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager$phase$$inlined$with$lambda$1.invoke(KonanPhases.kt:118) 
        at org.jetbrains.kotlin.konan.util.UtilKt.profileIf(Util.kt:34) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager.phase$backend_native_compiler(KonanPhases.kt:138) 
        at org.jetbrains.kotlin.backend.konan.LinkStage.linkStage(LinkStage.kt:232) 
        at org.jetbrains.kotlin.backend.konan.KonanDriverKt$runTopLevelPhases$5.invoke(KonanDriver.kt:109) 
        at org.jetbrains.kotlin.backend.konan.KonanDriverKt$runTopLevelPhases$5.invoke(KonanDriver.kt) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager$phase$$inlined$with$lambda$1.invoke(KonanPhases.kt:139) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager$phase$$inlined$with$lambda$1.invoke(KonanPhases.kt:118) 
        at org.jetbrains.kotlin.konan.util.UtilKt.profileIf(Util.kt:34) 
        at org.jetbrains.kotlin.backend.konan.PhaseManager.phase$backend_native_compiler(KonanPhases.kt:138) 
        at org.jetbrains.kotlin.backend.konan.KonanDriverKt.runTopLevelPhases(KonanDriver.kt:108)
        at org.jetbrains.kotlin.cli.bc.K2Native.doExecute(K2Native.kt:73)
        at org.jetbrains.kotlin.cli.bc.K2Native.doExecute(K2Native.kt:40)
        at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.java:94)
        at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.java:50)
        at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:88)
        at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:66)
        at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:34)
        at org.jetbrains.kotlin.cli.common.CLITool$Companion.doMainNoExit(CLITool.kt:180)
        at org.jetbrains.kotlin.cli.common.CLITool$Companion.doMain(CLITool.kt:171)
        at org.jetbrains.kotlin.cli.bc.K2Native$Companion$main$1.invoke(K2Native.kt:197)
        at org.jetbrains.kotlin.cli.bc.K2Native$Companion$main$1.invoke(K2Native.kt:188)
        at org.jetbrains.kotlin.konan.util.UtilKt.profileIf(Util.kt:34)
        at org.jetbrains.kotlin.konan.util.UtilKt.profile(Util.kt:29)
        at org.jetbrains.kotlin.cli.bc.K2Native$Companion.main(K2Native.kt:190)
        at org.jetbrains.kotlin.cli.bc.K2NativeKt.main(K2Native.kt:202)                                                                                                                                                                   
        at org.jetbrains.kotlin.cli.utilities.MainKt.main(main.kt:27)     
```

In the midst of all the gobbledygook, there is an answer: `llvm-lto` is whining because it wants to work with its girlfriend, `libtinfo.so.5`.
It's on strike until they get back together or unless you find a sexier, better alternative.
In Arch Linux, it is frowned upon yo use `yaourt` to fix things, but you can use `yaourt` or manually build a package from the AUR.
You are looking for the `ncurses5-compat-libs-6.1-1` deal. It gives you the wonderful `libtinfo.so.5`.

#### Building `libtininfo.so.5` from the AUR

Clone and get into the AUR repo:  
`git clone https://aur-dev.archlinux.org/ncurses5-compat-libs.git; cd ncurses5-compat-libs`

Create the pacman package (you may `--skippgpcheck` if you dare to live stupidly on the edge:  
`makepkg -Acs --skippgpcheck`

You now have a couple `tar.gz` files, just `pacman` the correct one!
`sudo pacman -U ncurses5-compat-libs-6.1-1-x86_64.pkg.tar.xz`

BOOM! Installed! You may drop the cheap mic now.
