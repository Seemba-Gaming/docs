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

# Importing the Seemba SDK Base Code

installing our SDK is really simple, just open a new cmd prompt and execute the following commands :

1. Go into your game's folder : <code>cd YOUR_UNITY_PROJECT_FOLDER</code> .
2. Install OpenUPM using : <code>npm install -g openupm-cli</code>.
3. Add Seemba to your poject using : <code>openupm add com.seemba.unitysdk</code>.

Now go back to Unity and wait for SeemabSDK while being imported.

# Configuring the SDK
Once SeembaSDK is imported you have a few simple steps to finish your configuration : 
## Entering your game info
On the Unity Editor menu go to <code>Seemba --> Integartion parameters</code>

![Step 1](/images/screenshots/1.png)

This window should appear :

![Step 2](/images/screenshots/seembaIntegration.png)

Fill the informations with the ones on your dahshboard

<aside class="warning">
Make sure that your game is configured on the dashboard side.
</aside>

1. Change the attribute **GAME_ID** value with the ID of your game indicated on the dashboard .
2. Change the attribute **GAME_NAME** value with the name of your game.
3. Change the attribute **GAME_SCENE_NAME** value with the name of your game scene.
4. Click **Apply** and close the window.

## Installing the Main Package

On the Unity Editor menu go to <code>Seemba --> Install Package</code>

![Step 3](/images/screenshots/Install-package.png)

## Configuring your menu scene

Go to your first scene, create a new GameObject named seemba and <code>Seemba.cs</code> script to it.

![Step 4](/images/screenshots/createobject.png)

1. Create a new Button to launch Seemba Tournaments.
2. Assign the OnClick action of this button with the Enter() function of Seemba.cs.

![Step 5](/images/screenshots/config.png)

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

![Step 6](/images/screenshots/sendingscore.png)

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

![Step 7](/images/screenshots/onesceneconfig.png)

# Troubleshooting
## I can't see the accept terms of use and privacy policy text !
To fix this issue, you need to import the essential ressources of TextMeshPro.
in order to this follow these steps.

<code>Window --> TextMeshPro --> Import TMP Essential Ressources</code>

If any other questions please feel free to reach us on support@seemba.com 
[//]: # "<span style="color:#F3F7F9"> you won't have any unless you're dumb </span>"
# Advanced Integration
## Deep Linking
Deep links are links that point directly to content within your application. Unity uses the Application.absoluteURL property and Application.deepLinkActivated event to support deep links on the following platforms:

* Android
* iOS

We will need the **ProcessDeepLinkMngr.cs** class file: 

```csharp
public class ProcessDeepLinkMngr : MonoBehaviour
{
    public static ProcessDeepLinkMngr Instance { get; private set; }
    public string deeplinkURL;
    private void Awake()
    {
        if (Instance == null)
        {
            Instance = this;                
            Application.deepLinkActivated += onDeepLinkActivated;
            if (!String.IsNullOrEmpty(Application.absoluteURL))
            {
                // Cold start and Application.absoluteURL not null so process Deep Link.
                onDeepLinkActivated(Application.absoluteURL);
            }
            // Initialize DeepLink Manager global variable.
            else deeplinkURL = "[none]";
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }
 
    private void onDeepLinkActivated(string url)
    {
        // Update DeepLink Manager global variable, so URL can be accessed from anywhere.
        deeplinkURL = url;
    }
}
```
### I already have Deep Linking integrated in my project
In this case, we assume that you already have the file **ProcessDeepLinkMngr.cs**.
You just need to add this line in the **onDeepLinkActivated** method :

<code>Seemba.Get.OnDeepLinkActivated(url);</code>

The process to configure an application to react to specific URLs is platform-specific.
### IOS
if you already have Deep Linking in your project, it means you have added your scheme to open with Deep Linking.
You don't need to do anything, you're all set!

### Android
if you already have Deep Linking in your project, it means you have an <code>AndroidManifest.xml</code> file, just add this line to your file :

<code> &lt;data android:scheme="YouSchemeName" android:host="seemba" /&gt;</code>

### I want to integrate Deep Linking in my project
### IOS
To add a URL scheme, follow these steps:

1. Open the iOS Player Settings window (menu: **Edit** > **Project Settings** > **Player Settings**, then select iOS).
2. Select **Other Settings**, then scroll down to **Configuration**.
3. Expand the Supported URL schemes section and, in the Element 0 field, enter the URL scheme associated with your app (for example, GameName).

This makes your app open any link that starts with <code>GameName://</code> and allows you to process the URL in the <code>Application.deepLinkActivated</code> event.

### Android

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools">
  <application>
    <activity android:name="com.unity3d.player.UnityPlayerActivity" android:theme="@style/UnityThemeSelector" >
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
      </intent-filter>
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="YouSchemeName" android:host="seemba" />
      </intent-filter>
    </activity>
  </application>
</manifest>
```

To enable deep linking, you need to set up an intent filter that overrides the standard app manifest to include a specific intent-filter section for Activity. The simplest way is to place the following <code>AndroidManifest.xml</code> file into your Project’s <code>Assets/Plugins/Android</code> folder. Unity automatically processes this file when you build your app:



<aside class="notice">
If you already have an AndroidManifest.xml file in <code>Assets/Plugins/Android</code>, just create a Folder in that path and put the new <code>AndroidManifest.xml</code> there (for example, <code>Assets/Plugins/Android/Seemba</code>).
</aside>



