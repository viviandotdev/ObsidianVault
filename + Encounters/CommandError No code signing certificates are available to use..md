type:: #note/error
tags:: [[expo]]

**trigger**
```
npx expo run:ios
```

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




Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons:
1. You might have mismatching versions of React and the renderer (such as React DOM)
2. You might be breaking the Rules of Hooks
3. You might have more than one copy of React in the same app