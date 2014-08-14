<h1>Cocos2dx Google Play Game Services</h1>

Mit License - http://opensource.org/

================================

V.1.0.0

- Android Google Play Game Services with Cocos2d-x Support for Achievements and Leaderboards.

================================

v.1.0.1

Bugs fixed by vivekporwal - https://github.com/vivekporwal

1. Submit score to play services was not working properly before because of call to bad function signature in JNIHelper.cpp which is corrected now.
2. 'long score' was taking garbage value as not converted to jlong is also fixed.
3. incrementAchievement : function call done for Boolean instead of Integer is corrected now.

Version for Cocos2d-x v3.0 by howlryu - https://github.com/howlryu

	https://github.com/howlryu/Cocos2dX_GooglePlayGamesServices

================================

V.1.0.2

1. IOS Leaderboards, Achievements and Little demo implemented.
2. Merge android project and IOS project to manage some platforms with the same code.
3. On Android Side modify the "gamehelper_ids" xml to update the app id and on the IOS side update the "PlayGameConstants.h" to make changes.
4. Leaderboards ID's and Achievements ID's are in the "PlayGameConstants.h" file
5. Created "PlayGameSingleton.h" for IOS side.
6. Check IOS folder to watch the files.

================================

v.1.0.3

1. Android Screen Blinking (Flickering) fixed thanks to - https://github.com/cocos2d/cocos2d-x/pull/5320
2. IOS files updated to support version lower to IOS7 because "animated" on "Google Play Game Services" IOS has issues on ipod version (just tested on iPad mini and iPod Touch)
3. Android and IOS AdMob integration.
4. JNIHelper added to Xcode project and with pragma validation just for Android to use the same code on both versions.
5. Some bugs fixed.

================================

v.1.0.4

1. Added AdMob interstitial support. Now you can preload interstitial ads and show whenever you want. 

================================

v.1.0.5

1. Admob intestitial support by hydex86 - https://github.com/hydex86 ; https://github.com/cpinan/Cocos2dX_GooglePlayGamesServices/pull/6

================================

v.1.0.6

1. Lot of issues fixed.
2. Removed some features for unknown bugs.
3. Change the ID for Google Play Services work.

Special thanks to:
- Hyunho.
- Iam Ks.
- Patinya Janluechai.
- Tahir Slezovic.
- Alberto González.
- Evgeniy Fedoseev.
- Hori from China.
- Francis Free.
- Pietro Vieria.

Thanks for your collaboration to fix this issues with the merge.

================================

Don't forget add google-play-services_lib library. The version used for this template is: 5089000

Android Support with cocos2d-x for Google Play Games Services.

This is the first version for the Cocos2d-x Template to use Google Play Games Services with Android.

Package created: com.carlospinan.utils

- ConfigUtils.java : Contains some global constants to identify if the services is available.
- NativeUtils.java : Allow communication with C++
- UtilActivity.java : This is the Class to extends from BaseGameActivity and implements some methods.

This sources in the future will support Google Play Games Services for IOS and Ouya support (Just android)

I will add Facebook SDK, Twitter SDK and some support for IAB (In App Billing) but maybe I will work with the Paypal SDK.

Important C++ Clases:

JNIHelpers: Allows communication from C++ to Java.
NativeUtils: Have some methods to communicate with Google Play Games Services.

Currently just work Achievements and Leaderboards.

Android notes:

Modify the file build_native.sh and change the NDK_ROOT for your NDK PATH and find COCOS2DX_ROOT and change for your 
COCOS2DX PATH

After this changes put in your terminal (or Cygwin):

./build_native.sh in the proj.android directory.

Note: I recommend use first: "./build_native.sh clean" without quotes to clean the previous obj

If you want to implement this use: NativeUtils.h in your C++ class and with your Game Logic call the methods.

In this version the current methods are:

	static bool isSignedIn();
	static void signIn();
	static void signOut();
	static void submitScore(const char* leaderboardID, long score);
	static void unlockAchievement(const char* achievementID);
	static void incrementAchievement(const char* achievementID, int numSteps);
	static void showAchievements();
	static void showLeaderboards();
	static void showLeaderboard(const char* leaderboardID);
	
In the next version I will add the multiplayer support and I'm working on the Ouya integration and IOS support 
for Google Play Game Services.

========================================================================================
IOS Side explanation V 1.0.2:

You must include "NativeUtils.h" and work with that methods.

If you want to change the notification achievement bar position you should modify the "AppController.mm" and change the line:

	[GPGManager sharedInstance].achievementUnlockedToastPlacement = kGPGToastPlacementTop;
	
The
    
    if(!PlayGameSingleton::sharedInstance().isSignedIn())
    {
        PlayGameSingleton::sharedInstance().trySilentAuthentication();
        [NSThread detachNewThreadSelector:@selector(playServicesAuthenticate) toTarget:self withObject:nil];
    }
    
Try to authenticate if the user is not signed in and run in background.

Play with the methods and modify the code if you need.



========================================================================================
AdMob interstitial integration V 1.0.4:

Just call to preloadIntestitialAd() before showing the ad. Then call to showIntestitialAd() to show an ad. Notice these methods require to be runned on main UI Thread. 

To avoid reconnect to Google Game Play Services on each intestitial shown I commented BaseGameActivity.onStop() method. 
========================================================================================

If you have some problem just contact me to:

carlos.pinan@gmail.com
