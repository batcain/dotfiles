# README
It is pretty tiring set new systems from scratch, so this repo includes patched and changed dwm/st folders and shell configs.

To start with, if you want to make dwm fonts to work use `pacman -Ss <fontname>`. Otherwise your terminal will be pretty f\*cked up. I use *Hack* font, so I had to install that with command below:
> sudo pacman -S ttf-dejavu ttf-opensans

Since you are dealing with st terminal it is recommended to use mono fonts. Anyways here are some patches that I have applied on dwm and st:

* dwm -> dwm-activetagindicatorbar-6.2.diff
* dwm -> dwm-autoresize-20160718-56a31dc.diff
* dwm -> dwm-awesomebar-20191003-80e2a76.diff
* dwm -> dwm-systray-20200610-f09418b.diff
* dwm -> scrollback
* dwm -> scrollback-mouse

* st -> st-alpha-0.8.2.diff
* st -> st-dracula-0.8.2.diff
* st -> st-font2-20190416-ba72400.diff
* st -> st-scrollback-20200419-72e3f6c.diff
* st -> st-scrollback-mouse-20191024-a2c479c.diff

How to set up dwm:

`git clone https://github.com/batcain/config/`



`cd config/dwm-stuff ; tar -xzvf dwm.tar.gz ; tar -xzvf st.tar.gz`

Go to dwm folder. Run the command below then do the same thing for st folder.

`make && sudo make clean install`

then;

`mv .xinitrc ~/`

At this point if there are no problems about compiling you are good to go. Just keep in mind that xorg server should be already down before you run the command below.

`startx`

### STUFF TO ADD:
 -> Emoji patch for dwm (not st it still crashes if you add any modern emoji (; __ ;)
Here is how:
* First, make sure you downloaded `ttf-joypixels` package.
* Second, Turn following command snippet to comment block.

```
/*
         * Do not allow using color fonts. This is a workaround for a BadLength
         * error from Xft with color glyphs. Modelled on the Xterm workaround. See
         * https://bugzilla.redhat.com/show_bug.cgi?id=1498269
         * https://lists.suckless.org/dev/1701/30932.html
         * https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=916349
         * and lots more all over the internet.
         *
        FcBool iscol;
        if(FcPatternGetBool(xfont->pattern, FC_COLOR, 0, &iscol) == FcResultMatch && iscol) {
                XftFontClose(drw->dpy, xfont);
                return NULL;
        }
*/
```

-> Add new keybindings to oftenly used programs; such as firefox, discord, blueman-applet, some IDES maybe? 
Here is how one simply add new keybinding;

* Open dwm/config.def.h
* Under `/* commands */` line there are char arrays of commands to be added. For example if I want to add firefox on ModKey+W binding I will add:
`static constant char *firefox[] = { "firefox", NULL};`
* Than go to modifiers and add following line:
`{ MODKEY,                       XK_w,      spawn,          {.v = firefox } },`
* cp config.def.h config.h ; make ; sudo make clean install
* restart dwm
