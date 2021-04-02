# Stytch React Native SDK

## Table of contents

* [Overview](#overview)
* [Requirements](#requirements)
* [Installation](#installation)
* [Getting Started](#getting-started)
  * [Configuration](#configuration)
  * [Starting UI Flow](#starting-ui-flow)
  * [Starting Custom Flow](#starting-custom-flow)

## Overview

Stytch's SDKs make it simple to seamlessly onboard, authenticate, and engage users. Improve security and user experience with passwordless authentication.

## Requirements

## iOS

The minimum deployment target needs to be at least 12.0
Required react-native version 0.60.x+

##Android

The SDK supports API level 21 and above ([distribution stats](https://developer.android.com/about/dashboards/index.html)).

- minSdkVersion = 21
- Android Gradle Plugin 4.1.1
- AndroidX

## Installation

1. Adding the SDK dependency

`npm install @stytch/stytch-react-native` --save or 
`yarn add @stytch/stytch-react-native`

Install or Update the Stytch pod for iOS with:
`cd ios`
`pod install`
`pod update`

## Getting Started

### Configuration

Pick a unique URL scheme for redirecting the user back to your app.
For this example, we'll use YOUR_APP_NAME://.
To start using Stytch, you must configure it:

```
	let projectId = "XXXXXX"
    let secretKey = "XXXXXX"

    StytchSdk.configureWithProjectId(
		projectId, 
		secretKey, 
		"schema", 
		"https://stytch.com/v1/"
	)
```

#### Handle UI Callbacks

StytchSdk provides callbacks methods
- `onEvent` - called after user found or created
- `onSuccess` - calls after successful user authorization
- `onFailure` - called when invalid configuration

```
	StytchSdk.onSuccess(res => {
        console.log("onSuccess", res)
    })

    StytchSdk.onFailure(res => {
        console.log("onFailure", res)
    })

    StytchSdk.onEvent(res => {
        console.log("onEvent", res)
        StytchSdk.closeUI()
    })
```

You can specify Stytch environment `test` or `live`:

```
    StytchSdk.setEnvironment(StytchSdk.environments.test)
```

You can specify Stytch loginMethod `LoginOrSignUp` (default) or `LoginOrInvite`:
`loginOrSignUp`  - Send either a login or sign up magic link to the user based on if the email is associated with a user already. 
`loginOrInvite` - Send either a login or invite magic link to the user based on if the email is associated with a user already. If an invite is sent a user is not created until the token is authenticated. 

```
	StytchSdk.setLoginMethod(StytchSdk.loginMethods.loginOrInvite)
```


### Starting UI Flow

#### Show UI

```
	StytchSdk.showUI()
```

#### UI Customization

```
	StytchSdk.showTitle(true) - Show/hide title
    StytchSdk.showBrandLogo(false) - Show/hide brand logo
    StytchSdk.showSubtitle(true) - Show/hide subtitle
    StytchSdk.inputCornerRadius(10) - Input corner radius, size in pixels
    StytchSdk.buttonCornerRadius(5) - Action button corner radius, size in pixels
    // fontWeight is Android only param

    StytchSdk.titleStyle({ size: 30, font: 'Monospace', color: "#6E471F", fontWeight: StytchSdk.fontWeights.NORMAL }) - Title text style
    StytchSdk.subtitleStyle({ size: 20, color: "#6E471F" }) - Subtitle text style
    StytchSdk.inputTextStyle({ size: 20, color: "#6E471F" }) - Input text style
    StytchSdk.inputPlaceholderStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#8A5A28" }) - Input placeholder text style
    StytchSdk.buttonTextStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" }) - Action button text style

    StytchSdk.inputBackgroundColor("#E8BD90") - Input background color code
    StytchSdk.inputBorderColor("#aaaaaa") - Input border color code
    StytchSdk.buttonBackgroundColor("#6E471F") - Input background color code
    StytchSdk.backgroundColor("#F5D4B0") - Window background color
```
