# iOS - SDK Implementation #

##  Current Version ##
**3.0.0** - [See Changelog](/doc/iOSChangelog)

Supports iOS 5.0 and up.

##  General Information ##

Integrating Tap for Tap into your app is usually really easy. Add our library, `libTapForTap.a`, to your iOS project, add required frameworks, initialize with your API key, and then add a `TapForTapBannerAd` to your view hierarchy or display an interstitial or app wall. That's it!

If you are not displaying TapForTap ads then you only need to call `+[TapForTap initializeWithAPIKey: @"YOUR API KEY"]` once when your app starts up, typically in the `application:didFinishLaunchingWithOptions:` method of your app delegate.

# Instructions #

##  Step 1: Add Tap for Tap to your project. ##

Add the `TapForTap` folder to your project by dragging and dropping it into Xcode, or selecting File ? Add Files to "Your App Name". Have Xcode create groups for the added files and copy them into your project.

![](https://raw.github.com/tapfortap/Documentation/master/images/xcode-01.png)

##  Step 2: Add required frameworks ##

We use SystemConfiguration.framework and AdSupport.framework so you will need to link these frameworks.

In the project explorer on the left side of Xcode 4:

- Select your project from the very top.
- Select your app's target.
- Select the Build Phases tab.
- Expand Link Binaries With Libraries.
- Click the + button.

![](https://raw.github.com/tapfortap/Documentation/master/images/xcode-02a.png)

- Select SystemConfiguration.framework.
- Click the Add button.

![](https://raw.github.com/tapfortap/Documentation/master/images/xcode-02b.png)

Repeat the above steps for AdSupport.framework.

##  Step 3: Initialize Tap for Tap when your app launches. ##

Import `TapForTap.h` in your app delegate and call our check in method.

```objective-c
# import "TapForTap.h"

- (void) application: (UIApplication *)application didFinishLaunchingWithOptions: (NSDictionary *)launchOptions
{
  [TapForTap initializeWithAPIKey: @"YOUR API KEY"];

	// Set up the main window and root view controller

	return YES;
}
```

##  Step 4: Display a banner, interstitial, or app wall. ##

### Banner ###

In the view controllers in wich you would like to display ads, in your `viewDidLoad` method create a `TapForTapBannerAd` and add it to your view.

For banners your view controller needs to implement the `TapForTapBannerAdDelegate` protocol in the header file, e.g. @interface MyViewController <TapForTapBannerAdDelegate>

```objective-c
// Be sure to import TapForTap.h
# import "TapForTap.h"

- (void) viewDidLoad
{
	[super viewDidLoad];

	// Show a banner at the bottom of this view, 320x50 points
	CGFloat y = self.view.frame.size.height - 50.0;
	TapForTapBannerAd *bannerAd = [[TapForTapAdView alloc] initWithFrame: CGRectMake(0, y, 320, 50) delegate: self];
	[self.view addSubview: adView];

	// If you do not use ARC then release the adView.
	// [adView release];
} 

##  Step 5 - Send info about your users (optional). ##

If you have information about your users that your privacy policy allows you to share with us, you can help us better target ads by passing it along. Just set the info on `TapForTap`. We accept year of birth, gender, location, and user account IDs on your system.

```objective-c
[TapForTap setGender: MALE or FEMALE];
[TapForTap setYearOfBirth: 1990];
[TapForTap setLocation: location];
[TapForTap setUserAccountId: accountId];
```

Where gender is `either` `MALE` or `FEMALE`, `age` is a positive integer, `location` is an `android.location.Location` object, and user `account ID`s are strings.

**Note:** If you are using Tap for Tap's [monetization](/doc/Monetization) program passing this information can greatly increase your revenue.