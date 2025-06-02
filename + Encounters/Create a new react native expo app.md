---
modified: 2025-06-02T09:46:09-04:00
---

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