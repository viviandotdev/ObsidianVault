type:: #note/error

![[Pasted image 20251104061845.png]]

zsh: correct 'expo' to '.expo' [nyae]? n
✔ Created native directory
✔ Updated package.json
✔ Finished prebuild
✔ Installed CocoaPods
› Your computer requires some additional setup before you can build onto physical iOS devices.
  Learn more
CommandError: No code signing certificates are available to use.

```
xed ios
```

**Add person team under Signing and capabilitities**
![[Pasted image 20251104061930.png]]



```
npx expo run:ios
```