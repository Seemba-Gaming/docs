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

Welcome to the Seemba! You can use this documentation to integrate the Seemba Game Tournament and Monetization system.

# Downloading the Seemba SDK

<aside class="notice">
Please create a game on our dashboard and contact the support to download the SDK as it is in early access and per recommendation only.
</aside>

# Importing the SDK

In the Unity Editor, select from the menu 'Assets', 'Import Package' and then 'Custom Package…'. Navigate to the directory where you downloaded the Seemba for Unity SDK and select <code>SeembaSDK.unitypackage</code>.

![Step 1](/images/screenshots/step1.png)

Import all of the assets in the package.

![Step 2](/images/screenshots/step2.png)

<aside class="notice">
Open <code>./SeembaSDK/Script/Manager/GamesManager.cs</code>
</aside>

![Step 3](/images/screenshots/step3.png)

# Configuring the SDK

> To set those variables, use this code:

```csharp
//Set The Game Name
public static string GameName="";
//Set Scene name of game , Entry point to the game
public static string GameSceneName="";
//Set The Game Id shown in your Dashboard ,you can't start without   setting the correct id
internal static string gameId="";
```

> Set the game URLs:

```csharp
public static string GAME_ANDROID_URL ="";
public static string GAME_IOS_URL = "";
```

> Configure the score sending:

```csharp
Seemba seemba = new Seemba ();
seemba.setResult (int score);
```

Fill the needed informations:

<aside class="warning">
Make sure that your game is configured on the dashboard side.
</aside>

1. Change the attribute <code>GameName</code> value with the name of your game .
2. Change the attribute <code>GameSceneName</code> value with the name of your game scene.
3. Change the attribute <code>gameId</code> value with the ID of your game indicated on the dashboard.


4. Change the attribute <code>GAME_ANDROID_URL</code> value with your Google Play Store    Application Link.
5. Change the attribute <code>GAME_IOS_URL</code> value with your Apple AppStore Application Link.

6. Open your <code>game over</code> script and add this few lines when player get his final score.

# Adding the tournament and duels mode to the game

Add an “eSport tournament” button to your game menu

![Step 4](/images/screenshots/step4.png)

# Building

Select all the Unity Scenes in the 'Scene' folder from above and drag them over to the Build Settings Panel and drop them in the 'Scenes In Build' area. Drag your game menu scene to be in order position 0 as below.

![Step 5](/images/screenshots/step5.png)

# Troubleshooting

If any questions please feel free to reach us on support@seemba.com
