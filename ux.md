## Fix scrollbar behavior
When I click above or below the scrollbar "thumb", I want to page up/down, not jump to the click location.  
> Found the answer here:
> https://forums.gentoo.org/viewtopic-t-948904-start-0.html
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
