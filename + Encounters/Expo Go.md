---
modified: 2025-04-30T06:30:59-04:00
---
How to create expo app
```
npx create-expo-app@latest
```
**starts a expo go development server**
```
npx expo start
```

 A development build is essentially your **own version of Expo Go** where you are free to use any native libraries and change any native config.
**Create your first build**
[Create your first build - Expo Documentation](https://docs.expo.dev/build/setup/#configure-the-project)
```
eas build:configure
```

```
npx expo install expo-dev-client
```


```
eas build --profile development --platform ios
```

```
eas build:run
```


```
npx expo start --dev-client
```