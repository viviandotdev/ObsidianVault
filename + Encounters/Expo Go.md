---
modified: 2025-06-02T07:41:06-04:00
---
up:: [[React Native]]
tags: #react-native 

How to create expo app
```
npx create-expo-app@latest
```
**starts a expo go development server**
```
npx expo start
```


 A development build is essentially your **own version of Expo Go** where you are free to use any native libraries and change any native config.
**Create your first Expo Application Services(EAS) build**
[Create your first build - Expo Documentation](https://docs.expo.dev/build/setup/#configure-the-project)
[Async Office Hours: How to make a development build with EAS Build - YouTube](https://www.youtube.com/watch?v=LUFHXsBcW6w)
**configure the build**
```
eas build:configure
```
**update the eas.json file**
```json
{
    "cli": {
        "version": ">= 16.3.3",
        "appVersionSource": "remote"
    },
    "build": {
        "development": {
            "developmentClient": true,
            "distribution": "internal",
            "ios": {
                "simulator": true,
                "resourceClass": "m1-medium"
            }
        },
        "preview": {
            "distribution": "internal"
        },
        "production": {
            "autoIncrement": true
        }
    },
    "submit": {
        "production": {}
    }
}

```
```
npx expo install expo-dev-client
```

**run the build, this will take a while**
```
eas build --profile development --platform ios
```

**if you forget to open the simulator you can run this to open the build again**
```
eas build:run
```

**start the app with dev build**
```
npx expo start --dev-client
```