### 3.0.9 / 2014-01-05
  * Fix a crashing bug when user's country is unavailable

### 3.0.8 / 2013-12-09
  * Fix a bug calling banner delegate methods (tftBannerWasTapped)

### 3.0.7 / 2013-10-29
  * Fix interstitial and app wall not covering bottom of screen on iOS 7

### 3.0.6 / 2013-10-11
  * Bug fixes

### 3.0.5 / 2013-10-07
  * Fix app wall/interstitial landscape issues
  * Add support for arm64 to library

### 3.0.4 / 2013-09-23
  * Workaround for spurious warnings about private API usage when submitting apps to the store

### 3.0.3 / 2013-09-16
  * iOS 7 support
  * Various minor bug fixes

### 3.0.2 / 2013-09-06
  * Ad AdMob library
  * Minor fixes to support AdMob

### 3.0.1 / 2013-09-03
  * Rework of the API. Minor semantic changes from 2.x. The most notable being that AppWall/Interstitial are no longer accessed via class methods.
  * Introduced new Interstitial and App Wall assets
    * Both are now anmiated
    * Both have transparent backgrounds
  * Added a new event to App Wall / Interstial
    * onTap

### 2.3.3 / 2013-07-18
  * If initializeWithDelegate is called more than once, delegates are now set properly on subsequent calls
  * Interstitial/AppWall ads are now properly cached
  * Implement back-off in a better way for failed banner requests
  * Scale banners up if necessary

### 2.3.2 / 2013-05-09
  * Rename MM*.* to TFT*.* to fix conflict with Millennial multimedia

### 2.3.1 / 2013-04-04

  * Fixed not being able to show app wall regression

### 2.3.0 / 2013-04-03

  * Earning can now be turned off from the web interface
  * Added new events to app wall and interstitial
    * DidShow
    * DidReceiveAd
  * Upgraded AdMob to 6.3.0
  * Added support for AdMob interstitial mediation

### 2.2.0 / 2013-03-11

  * Added in caching for interstitials/app-walls
  * Add close call to AppWall/Interstitial
  * Add a failedToDownload for app-walls and interstitials
  * Add ability for interstitial ads to hide the menu bar.

### 2.1.1 / 2013-01-14

  * Fix an issue where interstitials and app walls may show repeatedly
  * TapForTapAdMobBanner now release delegate properly

### 2.1.0 / 2012-11-15

  * Add app wall & interstitial delegates that get notified on dismissal
  * Accept more user data: year of birth, user account ID
  * Fix a memory leak and three crashing bugs
  * Support iOS 6's advertising ID and tracking settings
  * Force initialization if the API key changes

### 2.0.1 / 2012-10-24

  * Remove the check for enough space to show banners
  * Make -[TapForTapAdViewDelegate rootViewController] optional with a sane default
  * Fix a potential crashing bug when quickly closing the modal view controller

### 2.0.0 / 2012-10-15

  * Major new version!
  * Add interstitials
  * App an app wall
  * Banners are now full-width
  * Add apps simply by integrating the SDK

### 1.1.10 / 2012-09-28

  * Include the correct header files
  * show a message when trying to open an iTunes URL in the simulator
  * fix a crashing bug when a request is interrupted (e.g. server killed)
  * fix duplicate symbol error
  * bug fixes

### 1.1.9 / 2012-09-17

  * Update OpenUDID
  * Build with iOS 6 SDK and include armv7s for iPhone 5
  * Drops support for armv6 (iPhone 3G, iPod touch 2nd generation)

### 1.1.8 / 2012-09-14

  * expose the SDK version as +[TapForTap sdkVersion]
  * optimize the amount of data transferred

### 1.1.7 / 2012-08-10

  * Plug a memory leak in OpenUDID

### 1.1.6 / 2012-07-30

  * Bug fixes and fixes for AdMob

### 1.1.5 / 2012-06-30

  * Add support for AdMob mediation via TapForTapAdMobBanner
  * call -[delegate tapForTapAdViewDidReceiveAd] after loading all images
  * add autoRollover property to TapForTapAdView (for mediation layers)
  * add -[AdView stopLoadingAds]
  * Load ads even if the view is not is not in the view hierarchy

### 1.1.4 / 2012-05-07

  * fix a memory leak in MMHTTPClient
  * add OpenUDID support
  * only check in once
  * document TapForTapAdViewDelegate


### 1.1.3 / 2012-04-18

  * Only print debugging info if DEBUG is defined.
  * TapForTapAdView now has a delegate via the TapForTapAdViewDelegate protocol.


### 1.1.2 / 2012-04-13

  * add a changelog
  * Fix a bug where ads may not be loaded after failing to fill ads


### 1.1.1 / 2012-04-12

  * prevent stretching of ads on the iPad


### 1.1.0 / 2012-04-11

  * don't load ads in the background
  * allow removing the TapForTapAdView
  * de-ARC-ify
