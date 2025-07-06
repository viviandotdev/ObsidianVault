---
created: 2025-06-23 22:15
modified: 2025-07-06T11:35:17-04:00
---
up:: [[CHUWI MiniBook X]]
type:: #note/how-to 
tags:: [[linux]]
status:: #🟥
## How i set up ubuntu on minibook

I swapped esc with caps recently on ubuntu. Steps i followed:
```
sudo vim /etc/default/keyboard (open up this file)
```

There is an option XKBOPTIONS="", just change it to XKBOPTIONS="caps:swapescape"
Reboot

**Reference**
- [Esc to Capslock on ubuntu 22.04 : r/vim](https://www.reddit.com/r/vim/comments/1d6xv5a/esc_to_capslock_on_ubuntu_2204/)
[GitHub - rvaiya/keyd: A key remapping daemon for linux.](https://github.com/rvaiya/keyd)

