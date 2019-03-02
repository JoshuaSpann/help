# VASM Cross-Assembler
---

## Building VASM Natively on Windows (no Cygwin, MinTTY, WSL, etc)

### Install Visual Studio with C++ Desktop Support
In order to use vasm, install Visual Studio (Commuity works too) v12.0 or higher (2013+). 
During the install, ensure that C++ options for desktop development are selected. 
Once installed, open the VS#### x64 Native Tools Command Prompt (#### is the year number).
You may find it in `C:\Program Files (x86)\Microsoft Visual Studio ##.#\Common7\Tools\Shortcuts\` folder, where `##.#` is the VS version you are using (like `12.0`).

### Open VSx64 Tools Command Prompt to the VASM Directory
With the VSx64 Tools Command Prompt open, change to the VASM source directory. 
Before you can build the project, you must ensure that all references to `snprintf` are changed to `_snprintf` in the source code. This is because Windows. 
You may try it without changing anything, but this had to be done for my build attempt.
You need to change the references if you get an `unresolved externals` error message with a `return code '0x460'` and an `unresolved external symbol snprintf referenced in function *`.

### Change References from `snprintf` to `_snprintf`
The calls to `snprintf` are in "two" main files. 
Assuming that the vasm source dir is the current one, these files are `.\output_hunk.c` and `.\syntax\*\syntax.c`, where the `*` means the syntax that you want to use. 
If you are using the standard syntax, that would be in `.\syntax\std\syntac.c`.

Change all references from `snprintf` to `_snprintf` using your text editor. 
Save the files and the build should go through.

### Building VASM
To build VASM, use `md obj_win32` and then `nmake /f makefile.win32 CPU=<cpu> SYNTAX=<syntax>`. 
Make sure that you replace `<cpu>` with your target CPU architecture and `<syntax>` With your target assembler syntax.
