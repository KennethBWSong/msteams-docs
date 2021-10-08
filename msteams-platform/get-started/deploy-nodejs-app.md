---
title: Deploy your first app using Node.js
description: Learn how to deploy Microsoft Teams apps with Node.js.
keywords: getting started node.js nodejs
ms.topic: tutorial
ms.localizationpriority: medium
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
---

# Deploy your Teams Node.js app

After you build and test your Teams app, you can host it using Azure.

Let's deploy the first Hello World app on Azure using Teams Toolkit.

:::image type="content" source="../assets/images/get-started/app-roadmap/roadmap-p-3.png" alt-text="Image showing phase 3 of building an app." border="false":::

In this page, you'll learn to:
- [Deploy your app to Microsoft Teams](#deploy-your-app-to-microsoft-teams)
- [Update the credentials for your hosted app](#update-the-credentials-for-your-hosted-app)
- [Configure your sample app](#configure-your-sample-app)

## Deploy your app to Microsoft Teams

After deploying your app on the internet, deploy it to Teams by creating an app package. This package contains the app manifest and app icons. The Teams uses these files to display and brand the app. You can create this package manually or use App Studio or Developer Portal that are recommended for creating it. These tools run in Teams and you can use them for registering your app with Teams.

To register your app with Teams, you need:

- The URL where your app can be found on the internet.
- Icons that Teams will use to brand your app. The sample comes with placeholder icons located in "src\static\images. App Studio also will provide default icons, if needed.

**Update the app package**

# [Developer Portal](#tab/DP)

**To upload Hello World app to Developer Portal in Teams**

1. Open Microsoft Teams.

1. Select the **Store** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-store-icon.png"::: icon from the left-hand bar.

1. Search for **Dev Portal** in the search bar, and select **Dev Portal (Int)***.

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-dev-portal-app.png" alt-text="Select Developer Portal app" border="false":::

1. Select **Open**.
    
    :::image type="content" source="../assets/images/teams-toolkit-v2/open-dev-portal.png" alt-text="Image showing open Developer Portal app" border="false":::

    The Developer Portal opens.

1. Select the **Apps** tab.

    :::image type="content" source="../assets/images/teams-toolkit-v2/dev-portal-app.png" alt-text="Developer Portal app" border="false":::

1. Select **Import an existing app**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/import-app-in-dev-portal.png" alt-text="Image showing Import app button" border="false":::

1. Select /path to manifest/  and select **Import**.


    The **Hello World** app is imported in Developer Portal.

    nj-app-manifest-1

    **Additional configuration options in Developer Portal**

    You can configure your app using the Teams Developer Portal. The Manifest is found under Distribute. You can use the Manifest to configure capabilities, required resources, and other important attributes for your app. For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).

    :::image type="content" source="../assets/images/teams-toolkit-v2/configured-tdp.png" alt-text="Image showing configured tdp" border="false":::

### Configure your app capabilities


**Tab**
nj-add-tab-1
nj-tab-save-2
nj-tab-saved-3

**Bot**
same as C#
nj-bot-add-1
nj-bot-saved-1
nj-bot-added-2

Add bot to app
nj-add-bot-app-3

configure bot scope
nj-tab-chat-tab-conf-4

**Msg Ext**
same as C#
nj-add-msgext-1

App capabilities conf - 1


## Update the credentials for your hosted app

The sample app requires the following environment variables to be set to the values you made a note of earlier:

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

The environment variables are a part of your environment. Only your app's code can access them. They aren't exposed to any third parties.

If you're running the app using ngrok, you'll need to set up local environment variables. You can use Visual Studio Code to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

Where:

- The authorization credentials for your bot are as follows:
  - MICROSOFT_APP_ID is ID
  - MICROSOFT_APP_PASSWORD is password
- NODE_DEBUG show you what's happening in your bot in the Visual Studio Code debug console
- NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for the root directory in the `src` folder).

> [!Note]
> If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.

<a name="ConfigureTheAppTab"></a>

## Configure your sample app

After you install the app into Teams, you need to configure it to show content.

### Test your tab in Teams

1. Go to a channel in Teams, and select the **'+'** button to add a new tab.
1. You can then choose `Hello World` from the **Add a tab** list.
1. In the configuration dialog, select the tab you want to display in the channel. Then, select **Save**. 

You can see the `Hello World` tab loaded with the tab you chose:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### Test your bot in Teams

You can now interact with the bot in Teams. Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message. This type of message is called an **\@mention**. Whatever message you send to the bot will be sent back to you as a reply:

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### Test your messaging extension

**To test your messaging extension**
1. Select the three dots below the input box in your conversation view. A menu with the **'Hello World'** app is displayed.
1. Select the menu. A set of random texts is displayed. You can select one of the random texts and that is inserted into your conversation.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Select one of the random texts. The formatted card appears ready to send with your own message included at the bottom:

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|**Back** : [Build and test your app](build-and-test-csharp-app.md) | [Overview](code-samples.md) : **Next** |
|