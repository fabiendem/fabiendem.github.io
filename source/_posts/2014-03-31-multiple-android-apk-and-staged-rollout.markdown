---
layout: post
title: "Multiple Android APK and staged rollout"
date: 2014-03-31 16:06:40 +0100
comments: true
categories: 
- Android
---

In some conditions, you may need to publish different APKs for your application that are each targeted to different device configuration. Even if it's not really recommended, it is possible thanks to the [Multiple APK support][1].

Another cool feature from the Android distribution system is the staged-rollout, recently introduced by Google. The feature is [well described on the distribution support website][2] and [also on the Android developer website][3].  
Basically it allows to distribute your app to a percentage of users in order to gather possible critical bug reports and reviews before all your user based gets the update pushed on their device, you can slowly increase the percentage of users getting the update when you are more confident with your modifications.

Despite of the detailed documentation, a question raised while working on a Android app didn't find its answer from the documentation:

> If you have 2 APKs, let's say one for 2 APIs level ranges (eg: API >=17 and < 17). You want to publish an update for the users having a device running on Android API >= 17, and you select a stage rollout distribution for 20% of your user.  
On which users group will the percentage be based? All the users having your app (API < 17 and API >= 17) or only the users who have a compatible device (API >= 17)?

<!-- more -->

We haven't found the answer in the documentation, but the Google Play developer support team came up with this answer which may help you:
> If you select 20% for your staged rollout of the APK that is set for API 17+ then you should expect the 20% to be taken from users that have devices compatible with that API version, instead of all users eligible for the application.  
<cite>Google Play developer support</cite>

Now the answer is clear!

[1]: http://developer.android.com/google/play/publishing/multiple-apks.html
[2]: https://support.google.com/googleplay/android-developer/answer/3131213
[3]: http://developer.android.com/distribute/googleplay/about/distribution.html