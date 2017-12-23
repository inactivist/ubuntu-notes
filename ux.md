## Fix scrollbar behavior
When I click above or below the scrollbar "thumb", I want to page up/down, not jump to the click location.  

>
> Edit (or create) the file:
> ```
> ~/.config/gtk-3.0/settings.ini
> ```
> And add the following:
> 
> ```
> [settings]
> gtk-primary-button-warps-slider = false
> ```

Source: [How to fix GTK3 scrollbar behavior](http://askubuntu.com/a/296406)
https://forums.gentoo.org/viewtopic-t-948904-start-0.html

## Gnome Shell / Unity Stuff
### Window manager Aero Snap 
I Like Windows 7 Aero Snap feature, and it's fully-enabled by default in to Linux Mint (Cinnamon) desktop, using Super key + arrows.  Ubuntu Unity seems to support it using Ctrl-alt-numpad keys.  Would be nice if those of us without numpad keyboards could use the full range of Snap destinations.
- [How can I set up a keyboard shortcut to Aero snap windows in Gnome shell](https://askubuntu.com/questions/89666/how-can-i-set-up-a-keyboard-shortcut-to-aero-snap-windows-in-gnome-shell#401339)
- [Set up hot corners for Compiz Grid](http://www.webupd8.org/2011/01/set-up-hot-corners-for-compiz-grid.html)
