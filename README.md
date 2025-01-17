
**This repository is created based on [flutter_twitter](https://pub.dev/packages/flutter_twitter) because flutter_twitter has not been updated.**

Since flutter_twitter contains UIWebView, I could not apply to the App Store, so I replaced it with WKWebView.

# flutter_twitter

[![pub package](https://img.shields.io/pub/v/flutter_twitter_login.svg)](https://pub.dartlang.org/packages/flutter_twitter_login)
 [![Build Status](https://travis-ci.org/roughike/flutter_twitter_login.svg?branch=master)](https://travis-ci.org/roughike/flutter_twitter_login)
 [![Coverage Status](https://coveralls.io/repos/github/roughike/flutter_twitter_login/badge.svg)](https://coveralls.io/github/roughike/flutter_twitter_login)

A Flutter plugin for using the native TwitterKit SDKs on Android and iOS.

This plugin uses [the new Gradle 4.1 and Android Studio 3.0 project setup](https://github.com/flutter/flutter/wiki/Updating-Flutter-projects-to-Gradle-4.1-and-Android-Studio-Gradle-plugin-3.0.1).

## Dart support

* Dart 1: 1.0.x.
* Dart 2: 1.1.0 and up.

## Before instalation

Before you begin it is important to properly configure your application at https://apps.twitter.com/

It is important to configure the callback URLs so that everything works correctly in your application.

You will have to use the following callback URLs:

Android - twittersdk: //

iOS - twitterkit-CONSUMERKEY: //

FOR MORE INFORMATION READ:
https://developer.twitter.com/en/docs/basics/developer-portal/guides/callback-urls.html

[Complete Guide on ](https://github.com/twitter/twitter-kit-ios/wiki/Installation)




### Configure Info.Plist
Twitter Kit looks for a URL scheme in the format twitterkit-<consumerKey>, where consumerKey is your application's Twitter API key, e.g. twitterkit-dwLf79lNQfsJ.

You can find your consumer key in the Twitter app dashboard.

In your app's Info.plist, add URL Schemes by adding code below after <dict>

```
// Info.plist
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>twitterkit-<consumerKey></string>
    </array>
  </dict>
</array>
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>twitter</string>
    <string>twitterauth</string>
</array>
```



## Installation

See the [installation instructions on pub](https://pub.dartlang.org/packages/flutter_twitter_login#-installing-tab-). No platform-specific configuration is needed!

## How do I use it?

Here's some sample code that should cover most of the cases. For full API reference, just [see the source code](https://github.com/roughike/flutter_twitter_login/blob/master/lib/flutter_twitter_login.dart). Everything is documented there.

```dart
var twitterLogin = new TwitterLogin(
  consumerKey: '<your consumer key>',
  consumerSecret: '<your consumer secret>',
);

final TwitterLoginResult result = await twitterLogin.authorize();

switch (result.status) {
  case TwitterLoginStatus.loggedIn:
    var session = result.session;
    _sendTokenAndSecretToServer(session.token, session.secret);
    break;
  case TwitterLoginStatus.cancelledByUser:
    _showCancelMessage();
    break;
  case TwitterLoginStatus.error:
    _showErrorMessage(result.error);
    break;
}
```
