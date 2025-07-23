---
created: 2025-07-23 07:28
modified: 2025-07-23T07:28:38-04:00
---
up::
tags::

#Using Environment Variables in Expo with EAS Build

## Key References:

  * [Environment Variables in Expo](https://docs.expo.dev/guides/environment-variables/)
  * [Environment Variables and Secrets in EAS Build](https://docs.expo.dev/build-reference/variables/)

## How It Works

  * **`app.json` / `app.config.js`**: Defines core project details (app name, version, plugins, platform configs). **Does NOT directly manage environment variables.**
  * **`eas.json`**: Instructs the EAS build service on how to build your project based on its configuration. This is where you link to your **EAS Secrets**.

-----

## Step-by-Step Guide

### 1\. Local Development (`.env` file)

  * **Create a `.env` file** in your project root.
  * **Prefix your variables with `EXPO_PUBLIC_`**:
    ```
    EXPO_PUBLIC_SUPABASE_ANON_KEY="eyJ..."
    EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN="pk.eyJ..."
    ```
  * **Access variables in your code**:
    ```typescript
    const myVariable = process.env.EXPO_PUBLIC_SUPABASE_ANON_KEY;
    console.log(`Proof that this loads: ${myVariable}`);
    ```
  * **Best Practice: Centralized Config File (`config.ts`)**:
    ```typescript
    const config = {
      MAPBOX_ACCESS_TOKEN: process.env.EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN ?? "",
      SUPABASE_URL: process.env.EXPO_PUBLIC_SUPABASE_URL ?? "",
      SUPABASE_KEY: process.env.EXPO_PUBLIC_SUPABASE_ANON_KEY ?? "",
    };

    export default config;
    ```
    **Important Note**: `.env` files are **NOT included** in your EAS build by default.

### 2\. EAS Builds (Secrets Management)

To use your environment variables during **EAS builds (cloud or local)**, you *must* manage them as **EAS Secrets**.

  * **Create Secrets**: Set up your variables in your Expo project's secrets.

      * **Dashboard**: Go to `https://expo.dev/accounts/<username>/settings/secrets`
      * **CLI (Recommended)**: Push your `.env` file directly:
        ```bash
        eas secret:push --scope project --env-file .env
        ```

  * **Update `eas.json`**: Tell EAS which secrets to expose for specific build profiles (e.g., `development`, `production`).

    ```json
    {
      "build": {
        "development": {
          "autoIncrement": true,
          "developmentClient": true,
          "distribution": "internal",
          "env": {
            "EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN": "EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN",
            "EXPO_PUBLIC_SUPABASE_URL": "EXPO_PUBLIC_SUPABASE_URL",
            "EXPO_PUBLIC_SUPABASE_ANON_KEY": "EXPO_PUBLIC_SUPABASE_ANON_KEY"
          },
          "channel": "development"
        },
        "production": {
          // ... your production build settings
          "env": {
            "EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN": "EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN",
            "EXPO_PUBLIC_SUPABASE_URL": "EXPO_PUBLIC_SUPABASE_URL",
            "EXPO_PUBLIC_SUPABASE_ANON_KEY": "EXPO_PUBLIC_SUPABASE_ANON_KEY"
          }
        }
      }
    }
    ```

    This configuration tells EAS to look up the value of `EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN` (and others) from your **EAS Secrets** and make it available in the build environment.

-----

## Key Takeaways

  * **Local (`.env`) vs. Build (`EAS Secrets`)**: These are separate mechanisms. You need both if you develop locally and use EAS Builds.
  * **`EXPO_PUBLIC_` Prefix**: Essential for variables to be bundled and accessible in your client-side code.
  * **`eas secret:push`**: Simplifies secret management by syncing your `.env` with EAS secrets.
  * **`eas.json` `env` block**: Explicitly declares which secrets EAS should inject into the build process for a given profile.
  * **`.env` and `.gitignore`**: **Do NOT remove your `.env` from `.gitignore`.** Local environment files contain sensitive data and should not be committed.
  * **No `app.config.js` / `app.json` modification**: You do not add environment variables directly to these files.

-----

This refined version maintains all your crucial information while making it even easier to read and act upon. Excellent work\!