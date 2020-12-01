---
title: Seemba SDK Integration Guide

language_tabs: # must be one of https://git.io/vQNgJ
  - csharp

toc_footers:
  - <a href='https://dashboard.seemba.com/index.html'>Sign Up for a Developer Key</a>
  - <a href='https://seemba.com'>Seemba</a>, All Rights Reserved

includes:
  - errors

search: true
---

# Introduction

Welcome to the Seemba SDK documentation page! You can use this documentation to integrate the Seemba Game Tournament and Monetization system.

# Importing the Seemba SDK

installing our SDK is really simple, just open a new cmd prompt and execute the following commands :

1. Go into your game's folder : <code>cd YOUR_UNITY_PROJECT_FOLDER</code> .
2. Install OpenUPM using : <code>npm install -g openupm-cli</code>.
3. Add Seemba to your poject using : <code>openupm add com.seemba.unitysdk</code>.

Now go back to Unity and wait for SeemabSDK while being imported.

# Configuring the SDK
Once SeembaSDK is imported you have 4 simple steps to finish your configuration : 
## Entering your game info
On the Unity Editor menu go to <code>Seemba --> Integartion parameters</code>

![Step 1](/images/screenshots/EditorMenu.png)

This window should appear :

![Step 2](/images/screenshots/seembaIntegration.png)

Fill the informations with the ones on your dahshboard

<aside class="warning">
Make sure that your game is configured on the dashboard side.
</aside>

1. Change the attribute <code>gameId</code> value with the ID of your game indicated on the dashboard .
2. Change the attribute <code>GameName</code> value with the name of your game.
3. Change the attribute <code>GameSceneName</code> value with the name of your game scene.
4. Click Apply and close the window.

## Configuring your menu scene

Go to your first scene, create a new GameObject named seemba and <code>Seemba.cs</code> script to it.

![Step 3](/images/screenshots/createobject.png)

1. Create a new Button to launch Seemba Tournaments.
2. Assign the OnClick action of this button with the Enter() function of Seemba.cs.

![Step 4](/images/screenshots/config.png)

## Configuring Seemba game logic
1. Add our package to your GameController.cs script : 

```csharp
using SeembaSDK;
```

2. Configure the score sending by changing your GameOver() function as the example shows :

```csharp
if(Seemba.Get.IsSeemba)
{
    Seemba.Get.setResult((int)score);
}
```

![Step 5](/images/screenshots/sendingscore.png)

<aside class="success">
If your <strong>GAME SCENE</strong> is different than your <strong>MENU SCENE</strong>, ignore the rest you are done.
</aside>
<aside class="warning">
If not, please follow this last step.
</aside>

 If your <strong>GAME SCENE</strong> is the same as your <strong>MENU SCENE</strong>, add these 3 lines to your <code>Start()</code> function in your GameController script.

```csharp
if(EventsController.Get != null)
{
    Play();
}
```

![Step 6](/images/screenshots/onesceneconfig.png)

# Troubleshooting

If any questions please feel free to reach us on support@seemba.com 
[//]: # "<span style="color:#F3F7F9"> you won't have any unless you're dumb </span>"