# Tap for Tap Basic4Android Plugin

Do you want to use Tap for Tap with Basic4Android? Then we got you covered.

Help make this plugin better. Head to https://github.com/tapfortap/Basic4Android, fork the repo and submit pull requests.

Help make this documentation better. Head to https://github.com/tapfortap/Documentation fork the repo and update Basic4Android.md

### Minimum Requirements
- Android 2.2.0 and up

##  Installation
If you don't have the plugin yet then [download it here](https://github.com/tapfortap/Basic4Android/raw/master/release/TapForTapBasic4Android.zip).

Installing the Tap for Tap plugin is super easy. We'll guide you through it. This isn't a Basic4Android tutorial so we assume that you have a Basic4Android project (or projects) already set up and working.

1. Copy the `TapForTapBasic4Android.jar` and `TapForTapBasic4Android.xml` into your libraries folder. By default this is the `Libraries` folder typically located in: `C:\Program Files\Anywhere Software\Basic4android\Libraries.` You can also configure an `Additional Libraries` folder by opening `Tools -> Configure Paths`.
2. Add the following permissions to the `AndroidManifest.xml`
  - See Basic4Android's [how to edit the manifest](http://www.basic4ppc.com/android/wiki/index.php/Manifest_Editor) for more details.

```vbnet
'TapForTap Permissions
AddApplicationText (
  AddPermission (android.permission.INTERNET)
  AddPermission (android.permission.READ_PHONE_STATE)
  AddPermission (android.permission.ACCESS_NETWORK_STATE)
  AddPermission (android.permission.ACCESS_WIFI_STATE)
  AddPermission (android.permission.WRITE_EXTERNAL_STORAGE)
)
'End TapForTap Permissions
```
3. Add the `FullScreenAdActivity` to `AndroidManifest.xml`

```vbnet
  'TapForTap
  AddApplicationText(
   <activity android:name="com.tapfortap.FullScreenAdActivity" android:theme="@android:style/Theme.Translucent.NoTitleBar"/>
  )
  'End of TapForTap
```

That's it! Now you're ready to use Tap for Tap in your app.

##  Usage

1. Add the following to `Activity_Create`:

```vbnet
Sub Activity_Create(FirstTime As Boolean)
  'Initialize Tap for Tap
  Dim tftApiKey As String = "My Tap for Tap API key"
  Dim tft As TapForTap
  tft.initialize(tftApiKey)

  'Create an AdView
  Dim adview As TapForTapAdView
  adview.initialize()

  'Set the AdViews event handler
  adview.setEventHandler("AdViewEventHandler")

  'Calculate the x and y coordinate to center the AdView
  Dim adHeight = 50dip
  'Maintain the correct aspect ratio so ads look good
  Dim adWidth As Int = adHeight * 320/50
  Dim left As Int = (GetDeviceLayoutValues.Width - adWidth) / 2

  'Add the AdView to the actvities layout
  Activity.AddView(adview, left, 100%y - 50dip, adWidth, adHeight)
End Sub
```
2. Add the following subroutines to listen to the events produced by the adview

```vbnet
  'Event to handle when a new ad is received
  Sub AdViewEventHandler_ReceiveAd
  Log("AdViewEventHandler_ReceiveAd")
  End Sub

  'Event to handle when a new ad fails to download
  Sub AdViewEventHandler_FailedToReceiveAd (Reason As String)
  Log("AdViewEventHandler_FailedToReceiveAd" + Reason)
  End Sub

  'Event to handle when an ad is tapped
  Sub AdViewEventHandler_TapAd
  Log("AdViewEventHandler_TapAd")
  End Sub
```

Congratulations, you are done.

For more examples look at the test app located at https://github.com/tapfortap/Basic4Android/tree/master/test-app.

##  API Documentation
The API lets you create, position, and remove Tap for Tap ad views, interstitials and app walls. You can also pass in optional info about your users to help us with targetting. Please make sure your privacy policy allows this before giving us their personal information.

There are four main classes:

1. TapForTap
  - This is used to intialize and pass in information about the user
2. TapForTapAdView
  - This is used to show banner ads
3. TapForTapInterstitial
  - This is used to show full screen interstitial ads
3. TapForTapAppWall
  - This is used to show full screen app wall ads

### TapForTap

Create a TapForTap object via the following code. This object will be used throughout the following documentation.

```vbnet
  'Create a TapForTap object
  Dim tft As TapForTap
```

#### initialize(ApiKey as String)
This method needs to be called before you can use any of the other API calls. This method initializes your app with the TapForTap so we can begin serving you ads.

Usage:

```vbnet
  'Initialze TapForTap with my API key
  Dim tftApiKey As String = "My Tap for Tap API key"
  tft.initialize(tftApiKey)
```

#### setGender(Gender as Int)
Sets the gender of the user. This is sent along with ad requests and helps with matching the best ads for your app.
- MALE = 0
- FEMALE = 1
- NONE = -1

Usage:

```vbnet
  'Set the gender to male
  tft.setGender(0)
```

#### setYearOfBirth(YearOfBirth as Int)
Sets the year of birth of the user. This is sent along with ad requests and helps with matching the best ads for your app.

Usage:

```vbnet
  'Set the year of birth to 1984
  tft.setYearOfBirth(1984)
```

### TapForTapAdview

Create a TapForTapAdView using the following code. This object will be used throughout the following documentation.

```vbnet
  'Create an adview object
  Dim adview as TapForTapAdView
```

#### initialize()
Create a new AdView and start loading ads.

Usage:

```vbnet
  'Initialize the adView and start loading ads
  adview.initialize()
```

#### loadAds()
Loads and displays Tap for Tap ads. This only needs to be called to start show ads if stopLoadingAds has previously been called.

Usage:

```vbnet
  'Start loading ads
  adview.loadAds()
```

#### stopLoadingAds()
Stops the adview from downloading new ads.

Usage:

```vbnet
  'Stop loading ads
  adview.stopLoadingAds()
```

#### setEventHandler(EventName As String)
Sets the event name for this adView. The adView fires the following 3 events:

1. ReceiveAd()
  - Fired when a new ad is successfully downloaded.
2. FailedToReceiveAd(Reason As String),
  - Fired when an ad fails to download with the given reason.
3. OnTap
  - Fired when a user taps on an ad.

You will need to create the following subroutines to receives these events. Note that you need to replace the `EventName` with the string that you passed to setEventHandler.

```vbnet
  Sub EventName_ReceiveAd
    ...
  End Sub

  Sub EventName_FailedToReceiveAd (Reason As String)
    ...
  End Sub

  Sub EventName_TapAd
    ...
  End Sub
```

Usage:

```vbnet
  ...
  'Set the adView's event handler
  adview.setEventHandler("AdViewEventHandler")
  ...

  ...
  'Event to hande when a new ad is received
  Sub AdViewEventHandler_ReceiveAd
    Log("AdViewEventHandler_ReceiveAd")
  End Sub

  'Event to handle when an ad fails to download
  Sub AdViewEventHandler_FailedToReceiveAd (Reason As String)
  	Log("AdViewEventHandler_FailedToReceiveAd: " + Reason)
  End Sub

  'Event to handle when an ad is tapped
  Sub AdViewEventHandler_TapAd
  	Log("AdViewEventHandler_TapAd")
  End Sub
  ...
```

### TapForTapInterstitial

Create a TapForTapInterstitial using the following code. This object will be used throughout the following documentation.

```vbnet
  'Create an interstitial object
  Dim interstitial as TapForTapInterstitial
```

#### prepare()
This prepares the interstitial ad type. This method will pre-fetch an interstitial so when
show is called, the interstitial is shown with no delay. This is only useful for preparing
the very first interstitial. show() automatically prepares the next interstitial.

Usage:

```vbnet
  'Prepare the insterstial ad
  interstitial.prepare()
```

#### show()
This shows an interstitial ad. Calling showing automatically prepares the next interstital, so you do not need to call prepare again.

Usage:

```vbnet
  'Show the insterstial ad
  interstitial.show()
```

#### setEventHandler
Sets the event name for all interstitials. The interstitial fires the following 2 events:

1. ReceiveAd()
  - Fired when an ad is finsihed downloading.
2. ShowAd()
  - Fired when the ad is shown.
3. TapAd()
  - Fired when the user taps on the ad.
4. Dismissed()
  - Fired when the user closes the ad
5. FailedToReceiveAd(Reason As String)
  - Fired when an ad fails to download

You will need to create the following subroutines to receives these events. Note that you need to replace `EventName` with the string that you passed to setEventHandler.

```vbnet
  Sub EventName_ReceiveAd
    ...
  End Sub

  Sub EventName_ShowAd
    ...
  End Sub

  Sub EventName_TapAd
    ...
  End Sub

  Sub EventName_Dismissed

  Sub EventName_Dismissed
    ...
  End Sub

  Sub EventName_FailedToReceiveAd (Reason As String)
    ...
  End Sub
```

Usage:

```vbnet
  ...
  'Set the event handler
  interstital.setEventHandler("InterstitialEventHandler")
  ...

  ...
  'Event to handle when the interstitial is dismissed
  Sub InterstitialEventHandler_Dismissed
    Log("InterstitialEventHandler_Dismissed")
  End Sub

  'Event to handle if the interstitial ad failed to download
  Sub InterstitialEventHandler_FailedToReceiveAd (Reason As String)
	  Log("InterstitialEventHandler_FailedToReceiveAd: " + Reason)
  End Sub
  ...
```

### TapForTapAppWall

Create a TapForTapAppWall using the following code. This object will be used throughout the following documentation.

```vbnet
  'Create an app wall object
  Dim appwall as TapForTapAppWall
```

#### prepare()
This prepares the app wall ad type. This method will pre-fetch an appwall so when
show is called, the app wall is shown with no delay. This is only useful for preparing
the very first appwall. show() automatically prepares the next appwall.

Usage:

```vbnet
  'Prepare the app wall ad
  appwall.prepare()
```

#### show()
This shows an appwall ad. Calling showing automatically prepares the next interstital, so you do not need to call prepare again.

Usage:

```vbnet
  'Show the app wall ad
  appwall.show()
```

#### setEventHandler
Sets the event name for all appwalls. The app wall fires the following 2events:
1. ReceiveAd()
  - Fired when an ad is finsihed downloading.
2. ShowAd()
  - Fired when the ad is shown.
3. TapAd()
  - Fired when the user taps on the ad.
4. Dismissed()
  - Fired when the user closes the ad
5. FailedToReceiveAd(Reason As String)
  - Fired when an ad fails to download

You will need to create the following subroutines to receives these events. Note that you need to replace `EventName` with the string that you passed to setEventHandler.

```vbnet
  Sub EventName_ReceiveAd
    ...
  End Sub

  Sub EventName_ShowAd
    ...
  End Sub

  Sub EventName_TapAd
    ...
  End Sub

  Sub EventName_Dismissed
    ...
  End Sub

  Sub EventName_FailedToReceiveAd (Reason As String)
    ...
  End Sub
```

Usage:

```vbnet
  ...
  'Set the event handler
  appwall.setEventHandler("AppWallEventHandler")
  ...

  ...
  'Event to handle when the app wall is dismissed
  Sub AppWallEventHandler_Dismissed
    Log("AppWallEventHandler_Dismissed")
  End Sub

  'Event to handle if the app wall ad failed to download
  Sub AppWallEventHandler_FailedToReceiveAd (Reason As String)
  	Log("AppWallEventHandler_FailedToReceiveAd: " + Reason)
  End Sub
  ...
```
