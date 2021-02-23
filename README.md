---
noteId: "531c04906b2111ebb150c5c7eebb2104"
tags: []

---

# Stytch React Native SDK

# iOS
Requirements for iOS:

The minimum deployment target needs to be at least 12.0
Required react-native version 0.60.x+

1. Adding the SDK dependency

`npm install @stytch/stytch-react-native` --save or 
`yarn add @stytch/stytch-react-native`

Update the Stytch pod with:
`cd ios`
`pod install`
`pod update`

# iOS Swift
Add this import after `import UIKit` line
`import Stytch`

Add these lines to the bottom of `AppDelegate.swift` file

func application(_ application: UIApplication, continue userActivity: NSUserActivity, restorationHandler: @escaping ([UIUserActivityRestoring]?) -> Void) -> Bool {
        return Stytch.shared.handleMagicLinkUrl(userActivity.webpageURL)
    }

func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    return Stytch.shared.handleMagicLinkUrl(url)
}

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return Stytch.shared.handleMagicLinkUrl(url)
}

# iOS Objective C
Add this import after `#import "AppDelegate.h"` line
`#import <Stytch/Stytch.h>`

Add these lines to the bottom of `AppDelegate.m` file
... TBD (translate functions from swift)

2. Configure the flow
    let projectId = "XXXXXX"
    let secretKey = "XXXXXX"

    StytchSdk.configureWithProjectId(projectId, secretKey, "schema", "https://stytch.com/v1/")
    StytchSdk.onSuccess(res => {
        console.log("onSuccess", res)
    })

    StytchSdk.onFailure(res => {
        console.log("onFailure", res)
    })

    StytchSdk.onEvent(res => {
        console.log("onEvent", res)
    })
    StytchSdk.onMagicLinkSent(res => {
        console.log("onMagicLinkSent", res)
    })

    StytchSdk.onDeepLinkHandled(res => {
        console.log("onDeepLinkHandled", res)
    })

    StytchSdk.showUI()

    // StytchSdk.closeUI() // when you want to close the default Stytch UI

3. Customizing UI (if using showUI)
    StytchSdk.showTitle(true)
    StytchSdk.showBrandLogo(false)
    StytchSdk.showSubtitle(true)
    StytchSdk.inputCornerRadius(10)
    StytchSdk.buttonCornerRadius(5)
    StytchSdk.titleStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" })
    StytchSdk.subtitleStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" })
    StytchSdk.inputTextStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" })
    StytchSdk.inputPlaceholderStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" })
    StytchSdk.buttonTextStyle({ size: 20, font: 'ArialHebrew-Bold', color: "#ffffff" })

    StytchSdk.inputBackgroundColor("#aaaaaa")
    StytchSdk.inputBorderColor("#aaaaaa")
    StytchSdk.buttonBackgroundColor("#aaaaaa")
    StytchSdk.backgroundColor("#aaaaaa")

Example repo: https://github.com/stytchauth/stytch-react-native-example
More in-depth reference of functionalities: https://github.com/stytchauth/stytch-ios-example
