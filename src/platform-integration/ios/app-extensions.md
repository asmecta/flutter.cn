---
title: Adding iOS app extensions
description: Learn how to add app extensions to your Flutter apps
---

iOS App extensions allow you to expand functionality
outside your app. Your app could appear as a home screen widget,
or you can make portions of your app available within other apps.

To learn more about app extensions, check out
[Apple's documentation][].

## How do you add an app extension to your Flutter app?
To add an app extension to your Flutter app,
add the extension point *target* to your Xcode project.

1. Open the default Xcode workspace in your project by running
   `open ios/Runner.xcworkspace` in a terminal window from your
   Flutter project directory.
1. In Xcode, select **File -> New -> Target** from the menu bar. 

    <figure class="site-figure {{include.class}}">
    <div class="site-figure-container">
        <img src='/assets/images/docs/development/platform-integration/app-extensions/xcode-new-target.png'
        height='300'>
    </div>
    </figure>
1. Select the app extension you intend to add.
   This selection generates extension-specific code 
   within a new folder in your project.
   To learn more about the generated code and the SDKs for each
   extension point, check out the resources in
   [Apple's documentation][].

To learn how to add a home screen widget to your iOS device,
check out the [Adding a Home Screen widget to your Flutter App] codelab.

[Adding a Home Screen widget to your Flutter App]: https://codelabs.developers.google.com/flutter-home-screen-widgets#0

## How do Flutter apps interact with App Extensions? 
Flutter apps interact with app extensions using the same
techniques as UIKit or SwiftUI apps.
The containing app and the app extension don't communicate directly.
The containing app might not be running while the device user interacts with the extension.
The app and your extension can read and write to shared resources or
use higher-level APIs to communicate with each other.

### Using higher-level APIs
Some extensions have APIs. For example, 
the [Core Spotlight][] framework indexes your app 
allowing users to search from Spotlight and Safari. The
[WidgetKit][] framework can trigger an update of your home screen
widget.

To simplify how your app communicates with extensions,
Flutter plugins wrap these APIs.
To find plugins that wrap extension APIs,
check out [Leveraging Apple's System APIs and Frameworks][] or
search [pub.dev][].

### Sharing resources
To share resources between your Flutter app and your app extension, put
the `Runner` app target and the extension target in the same
[App Group][].

{{site.alert.note}}
  You must be signed in to your Apple Developer account.
{{site.alert.end}}

To add a target to an App Group:

1. Open the target settings in Xcode.
1. Navigate to the **Signing & Capabilities** tab.
1. Select **+ Capability** then **App Groups**.
1. Choose which App Group you want to add the target from one of two options:
    1. Select an App Group from the list.
    1. Click **+** to add a new App Group.

{% include docs/app-figure.md
image="development/platform-integration/app-extensions/xcode-app-groups.png" %}

When two targets belong to the same App Group, they can read and write
data to the same source. Choose one of the following sources for your data.

- **Key/value:** Use the [`shared_preference_app_group`][]
  plugin to read or write to `UserDefaults` within the same App Group.
- **File:** Use the App Group container path from the
  [`path_provider`][] plugin to [read and write files][].
- **Database:** Use the App Group container path from
  the [`path_provider`][] plugin to create a database with the
  [`sqflite`][] plugin.

### Background updates

Background tasks provide a means to update your extension through code
regardless of the status of your app.

To schedule background work from your Flutter app, use the
[`workmanager`][] plugin.

### Deep linking
You might want to direct users from an app extension to a
specific page in your Flutter app.
To have a URL open a specified route in your app, you can use
[Deep Linking][].

## Creating app extension UIs with Flutter

Some app extensions display a user interface.

For example, share extensions allow users to conveniently
share content with other apps,
such as sharing a picture to create a new post on a social media app.

<figure class="site-figure {{include.class}}">
    <div class="site-figure-container">
        <img src='/assets/images/docs/development/platform-integration/app-extensions/share-extension.png'
        height='300'>
    </div>
</figure>

Starting from version 3.16, Flutter supports
building Flutter UI for app extensions.
To create the UI for
an app extension using Flutter, you must use an extension-safe
`Flutter.xcframework` and embed the `FlutterViewController`
as described in the following section.

{{site.alert.note}}
  Due to the memory limitations of app extensions,
  it is only recommended to use Flutter to build app extension UI
  for extension types that have memory limits larger than 100MB.
  For example, share extensions which have a 120MB memory limit.

  In addition, Flutter uses extra memory in debug mode.
  Therefore, Flutter does not fully support running app extensions in
  debug mode on physical devices when used to build extension UI.
  As an alternative, use an iOS simulator to test your extension in debug mode.
{{site.alert.end}}

1. Locate the extension-safe `Flutter.xcframework` file,
   at `<path_to_flutter_sdk>/bin/cache/artifacts/engine/ios/extension_safe/Flutter.xcframework`.
   
    * If you would like to build for release or profile mode, find the
      framework file under the `ios-profile` or `ios-release` folder.

1. Drag and drop the `Flutter.xcframework` file into your
   share extension's frameworks and libraries list.
   Make sure the embed column says "Embed & Sign".

   <figure class="site-figure {{include.class}}">
       <div class="site-figure-container">
           <img src='/assets/images/docs/development/platform-integration/app-extensions/embed-framework.png'
           height='300'>
       </div>
   </figure>

1. Open the Flutter app project settings in Xcode to share build
   configurations. 

   1. Navigate to the **Info** tab.
   1. Expand the **Configurations** group. 
   1. Expand the **Debug**, **Profile**, and **Release** entries.
   1. For each of these configurations, make sure the value in the
      **Based on configuration file** drop-down menu for your
      extension matches the one selected for the normal app target.

    <figure class="site-figure {{include.class}}">
        <div class="site-figure-container">
            <img src='/assets/images/docs/development/platform-integration/app-extensions/xcode-configurations.png'
            height='300'>
        </div>
    </figure>

1. (Optional) Replace any storyboard files with an extension class if needed.
   
    1. In the `Info.plist` file,
       delete the **NSExtensionMainStoryboard** property.
    1. Add the **NSExtensionPrincipalClass** property.
    1. Set the value for this property to the entry point of the extension.
       For example, for share extensions, it is usually
       `<YourShareExtensionTargetName>.ShareViewController`.
       If you use Objective-C to implement the extension,
       you should omit the `<YourShareExtensionTargetName>.` portion.<br>

    <figure class="site-figure {{include.class}}">
        <div class="site-figure-container">
            <img src='/assets/images/docs/development/platform-integration/app-extensions/share-extension-info.png'
            height='300'>
        </div>
    </figure>


1. Embed the `FlutterViewController` as described in
   [Adding a Flutter Screen][]. For example, you can display a
   specific route in your Flutter app within a share extension.

    ```swift
    import UIKit
    import Flutter

    class ShareViewController: UIViewController {
        override func viewDidLoad() {
            super.viewDidLoad()
            showFlutter()
        }

        func showFlutter() {
            let flutterViewController = FlutterViewController(project: nil, nibName: nil, bundle: nil)
            addChild(flutterViewController)
            view.addSubview(flutterViewController.view)
            flutterViewController.view.frame = view.bounds
        }
    }
    ```

## Test extensions

Testing extensions on simulators and physical devices
have slightly different procedures.

{% comment %}
The different procedures are necessary due to bugs(which bugs?) in Xcode.
Revisit these docs after future Xcode releases to see if they are fixed.
{% endcomment -%}

### Test on a simulator

1. Build and run the main application target.
1. After the app is launched on the simulator,
   press <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>H</kbd> to minimize the app,
   which switches to the home screen.
1. Launch an app that supports Share Extension,
   such as the Photos app.
1. Select a photo, tap the share button, then tap
   on the share extension icon of your app.

### Test on a physical device

You can use the following procedure or the
[Testing on simulators](#test-on-a-simulator) instructions
to test on physical devices.

1. Launch the Share Extension target.
1. In the popup window that says “Choose an app to run”,
   select an app that can be used to test Share Extension,
   such as the Photos app.
1. Select a photo, tap the share button,
   then tap on the Share Extension icon of your app.

{% comment %}
## Tutorials

For step-by-step instruction for using app extensions with your
Flutter iOS app, check out the
[Adding Home Screen Widgets and Live Activities to your Flutter app][] codelab.
{% endcomment %}

[Apple's documentation]: https://developer.apple.com/app-extensions/
[Core Spotlight]: https://developer.apple.com/documentation/corespotlight
[WidgetKit]: https://developer.apple.com/documentation/widgetkit
[Leveraging Apple's System APIs and Frameworks]: {{site.url}}/platform-integration/ios/apple-frameworks
[pub.dev]: {{site.pub-pkg}}
[App Group]: https://developer.apple.com/documentation/xcode/configuring-app-groups
[Adding a Flutter Screen]: {{site.url}}/add-to-app/ios/add-flutter-screen?tab=vc-uikit-swift-tab#alternatively---create-a-flutterviewcontroller-with-an-implicit-flutterengine
[`shared_preference_app_group`]: {{site.pub-pkg}}/shared_preference_app_group
[Compiling the Engine]: https://github.com/flutter/flutter/wiki/Compiling-the-engine
[`path_provider`]: {{site.pub-pkg}}/path_provider
[`sqflite`]: {{site.pub-pkg}}/sqflite
[`workmanager`]: {{site.pub-pkg}}/workmanager
[read and write files]: {{site.url}}/cookbook/persistence/reading-writing-files
[example from the community on GitHub]: {{site.github}}/flutter/engine/pull/39941
[Deep Linking]:{{site.url}}/ui/navigation/deep-linking
[Adding Home Screen Widgets to your Flutter app]: {{site.codelabs}}/flutter-home-screen-widgets#0
