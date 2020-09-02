---
title: Build and run your first Teams app
author: heath-hamilton
ms.author: heath-hamilton
description: Run your first Microsoft Teams app.
ms.date: 08/31/2020
ms.topic: quickstart
---
# Build and run your first Microsoft Teams app

You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.

## Create an app project

Use the Microsoft Teams Toolkit in Visual Studio Code to quickly set up your first app project.

1. In Visual Studio Code, select the **Microsoft Teams** icon on the left Activity Bar and choose **Create a new Teams app**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="create teams app image":::
1. Enter the name for your Teams app. (This is the default name for your app and also the name of the app project directory on your local machine.)
1. On the **Add capabilities** screen, select **Tab** then **Next**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="create teams app image":::
1. Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.

## Understand important app project files

Once the toolkit sets up your project, you have the components to build a basic Teams app. The project directories and files display in the Explorer area of Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="App project files in Visual Studio Code.":::

Let's take time to understand some of the key files Teams app developers work with.

### App manifest (`manifest.json`)

Located in the `.publish` directory, the app manifest is the starting point for any app project. The manifest defines your app's fundamental attributes and points to required resources. When you install an app, Teams parses the manifest to understand how to render your app in the client.

In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.

### App scaffolding (`src`)

The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.

If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app. It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.

### App package (`Development.zip`)

Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams. The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).

Here are some details about the app package files:

|Name|Type|Size|Manifest location|Toolkit filename|
|---|---|:---:|:---:|-----|
|**App manifest**|`.json`| — | — |`.publish/manifest.json`|
|**Color logo**|`.png`|192&times;192 pixels|`icon.color`|`.publish/color.png`|
|**Outline logo**|`.png`|32&times;32 pixels|`icon.outline`|`.publish/outline.png`|

## Run your app

In the interest of time, you'll build and run your app locally. Production-level Teams apps are hosted in the cloud.

(This information is also available in the toolkit `README`.)

1. In a terminal, go to the root directory of your project and run `npm install`.
1. Run `npm start`. Once complete, there's a **Compiled successfully!** message in the terminal.
1. Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)
:::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Viewing the app in a browser.":::

## Set up a tunnel between Teams and your app

Your app is up and running on your local web server. To run your app in Teams, you must make your `localhost` accessible through HTTPS.

Install [ngrok](https://ngrok.com/download) if you haven't already. The tool creates two globally available URLs that point to your local web server (`http://localhost:3000`). You need the forwarding URL that begins with `HTTPS`.

1. Open a new terminal and run `ngrok http 3000`.
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="ngrok running image":::
1. Copy the HTTPS URL (for example, *<https://85528b2b3ba5.ngrok.io>*).
1. In your `.publish` directory, open `Development.env`. 
1. Replace the `baseUrl0` value with the copied URL. (For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)

## Sideload your app in Teams

With your app running and accessible via HTTPS, you're ready to upload it to Teams.

> [!TIP]
> Before trying to sideload your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist#teams-app-validation-tool). You must fix red errors to successfully sideload your app.

1. Log in to the Teams client with your account that allows app sideloading. (If you aren't sure what that means, see more about [Teams development accounts](../build-your-first-app/building-real-world-app.md).)
1. Select **Apps**, then choose **Upload a custom app**. 
1. Go to your app project `.publish` folder and select `Development.zip`. An install modal displays.
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="add teams app":::
1. Select **Add** to install your app.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Screenshot showing an example Hello, World! app in Teams.":::

🎉 Congratulations! You have a running Teams app.

## Next step

Learn how to get started with other types of Teams apps.

:::row:::
   :::column span="":::
> [!div class="nextstepaction"]
> [Expand on your personal tab](../build-your-first-app/add-personal-tab.md)
   :::column-end:::
   :::column span="":::
> [!div class="nextstepaction"]
> [Build a channel tab](../build-your-first-app/add-channel-tab.md)
   :::column-end:::
   :::column span="":::
> [!div class="nextstepaction"]
> [Build a bot](../build-your-first-app/add-bot.md)
   :::column-end:::
:::row-end:::