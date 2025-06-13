---
modified: 2025-06-13T06:24:55-04:00
---
#expo
**Create empty expo app**
[Create a project - Expo Documentation](https://docs.expo.dev/get-started/create-a-project/)

```
npx create-expo-app@latest
```

**Set up your env - Create expo development build**
[Set up your environment - Expo Documentation](https://docs.expo.dev/get-started/set-up-your-environment/?platform=ios&device=simulated&mode=development-build)
```
brew update && brew install watchman
```

```
eas build:configure
```
**Adjust your build profile**
```
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal",
      "ios": {
        "simulator": true 
      }
    }
  }
}
```

```
eas build --platform ios --profile development
```




**Add react-native-reusables to your app**
[React Native Reusables | rnr docs](https://rnr-docs.vercel.app/getting-started/introduction/)
**run this init on your repo clean, update the code and styles to work**
**fix the package.json and fix the imports**
```
npx @react-native-reusables/cli@latest init
```

**use this command to update and add new components**
```
npx @react-native-reusables/cli@latest add
```