# TempleOS Help

## Changing Startup from Default

The default startup gives you a blue wallpaper with three terminal windows open.
The top term has debug info and error messages printed to it, and is not usable.
The left term has the startup and tour prompt by default.
The right term in in its default mode.
Autocomplete is hogging the screen real estate on the right.

### Changing the Wallpaper Background Color
Edit `C:/Adam/WallPaper.HC.Z`, do a find and replace on BLUE to your color of choice.

### Disabling the Top Term
Edit `C:/StartOS.HC.Z` and comment out or remove lines 20-22:
```HolyC
Dbg("Type 'Gl'");
DocTermNew;
WinVert(2,10);
```

### Disabling Left Term Tip of Day and Tour
To change the initial left term startup behavior, from the defaults, edit `C:/Once.HC.Z`.
Find `case BOOT_SRC_HARDDRV:` if you want to change the default behavior when booting from hard disk.

### Control Number and Layout of Startup Terms
For the number of terms, either add or remove users on lines 24-26 in `C:/HomeSys.HC.Z`:
```HolyC
CTask *user1,*user2;
user1=User;
user2=User;
```

For the terms startup layout, edit `C:/HomeSys.HC.Z` and comment out line 28: `WinTileVert;`

### Have AutoComplete in the Background
Edit `C:/Adam/AutoComplete/ACInit.HC.Z` and change line 160 from `ON` to `OFF`:
`AutoComplete(OFF);`
