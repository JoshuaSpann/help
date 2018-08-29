# LXDE Help
---

## Adding a Custom Application to the LXDE panel

### Create `desktop` File Entry
The desktop entry is needed in `/usr/share/applications/` to see the app in your main menu and list of apps in lxde:  
`sudo vim /usr/share/applications/app.desktop`

Copy an existing desktop file or add a new one, having the bare minimum. Note that the `#` lines are not mandatory:  
```
[Desktop Entry]
Type=Application
Name=My App
#GenericName=Text Editor
#Comment=My application
Icon=app
Exec=app %u
#Categories=Development;GTK;Utility;AudioVideo;Office;Game;Settings;
StartupNotify=true
Terminal=true
```

### Add Custom Icon
`sudo cp ~/app.png /usr/share/pixmaps/`

### Restart LXDE Panel Control `lxpanelctrl`
`lxpanelctl restart`

## Resources
- [Main Menu (LXPanel)](https://wiki.lxde.org/en/Main_Menu)
- [Location to put application icons](https://ubuntuforums.org/showthread.php?t=1380254)
 - **Penguin Guy - /usr/share/icons/** "You should store all your program's custom icons in: /usr/share/icons/hicolor/<resolution>/<type>/<name>.png"
 - **coyotle - Re: Location to put application icons** "or /usr/share/pixmaps"
