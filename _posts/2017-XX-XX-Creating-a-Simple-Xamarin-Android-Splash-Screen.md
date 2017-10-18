---
published: false
layout: post
title: Creating a Simple Xamarin.Android Splash Screen
date: 2017-01-21 12:23
comments: true
tags: [Xamarin, Xamarin.Android, Android]
---
Creating a splash screen for your app is not usually priority number 1, but at some point you or your client during the development phase is going to get sick of seeing a blank screen upon app launch.  Creating a splash screen for your Xamarin.Android app is quite different from how it's done on your Xamarin.iOS application.  In this post I am going to review how I create a simple splash screen on my Xamarin.Android applications.  

First is coming up with an idea of what you want displayed on the splash screen.  Keep in mind that the splash screen is only shown for a matter of seconds, this means don't put paragraphs of text or very detailed artwork.  Typically I will show only a couple assets, such as an app/brand icon and the app title.  This artwork is static and will be shipped with the application bundle to the store.  Don't plan on including any dynamic text or images from a web service, because this screen is shown prior to any of your app's code actually executing, and as soon as the app is ready the splash screen is removed and your app's first screen is displayed.