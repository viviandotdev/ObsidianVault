
tags:: [[ubuntu]]

**Keyboard Configuration**
Open this file

```
sudo vim /etc/default/keyboard
```

**Update Keyboard Configuration file, XBOPTIONS**
swap ctl and caps lock

```
# KEYBOARD CONFIGURATION FILE

# Consult the keyboard(5) manual page.

XKBMODEL="pc105"
XKBLAYOUT="us"
XKBVARIANT=""
XKBOPTIONS="ctrl:swap_lalt_lctl,caps:swapescape"

BACKSPACE="guess"
```

**gsettings reset**
```
gsettings reset org.gnome.desktop.input-sources xkb-options
```

**gsettings report**
```
gsettings get org.gnome.desktop.input-sources xkb-options
```


**caps lock**
https://www.reddit.com/r/vim/comments/1d6xv5a/esc_to_capslock_on_ubuntu_2204/
**update xkb options**
https://askubuntu.com/questions/950020/setting-multiple-options-in-etc-default-keyboard

**ctl swap**
https://bbs.archlinux.org/viewtopic.php?id=187295

