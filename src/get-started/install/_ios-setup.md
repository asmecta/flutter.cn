## iOS setup

## 设置 iOS 开发环境

### Install Xcode

### 安装 Xcode

To develop Flutter apps for iOS, you need a Mac with Xcode installed.

开发 iOS 平台上的 Flutter 应用，你需要一个安装了 Xcode 的 Mac 设备。

 1. Install the latest stable version of Xcode
    (using [web download][] or the [Mac App Store][]).

    通过 [直接下载][web download] 或者通过 [Mac App Store][]
    来安装最新稳定版 Xcode；

 1. To configure the Xcode command-line tools to use the
    installed version, run the following commands.

    配置 Xcode 命令行工具以使用新安装的 Xcode 版本。
    从命令行中运行以下命令：

    ```terminal
    $ sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
    $ sudo xcodebuild -runFirstLaunch
    ```

    To use the latest version of Xcode, use this path.
    If you need to use a different version, specify that path instead.

    当你安装了最新版本的 Xcode，大部分情况下，上面的路径都是一样的。
    但如果你安装了不同版本的 Xcode，你可能要更改一下上述命令中的路径。

 1. Sign the Xcode license agreement.
    To sign the SLA, either:

    同意 Xcode 的许可协议：

    {: type="a"}
    1. Open Xcode and confirm.

       运行一次 Xcode。

    1. Open the Terminal and run:

       在终端输入命令并运行：

       ```terminal
       $ sudo xcodebuild -license
       ```

Versions older than the latest stable version might still work,
but are not recommended for Flutter development.

旧版本可能也能够正常工作，但是不建议在 Flutter 开发环境中使用。
旧版本的 Xcode 不支持定位代码，还可能无法正常工作。

With Xcode, you can run Flutter apps on an iOS device or on the simulator.

安装了 Xcode 之后，你就可以在 iOS 真机或者模拟器上运行 Flutter 应用了。

### Set up the iOS simulator

### 配置 iOS 模拟器

To prepare to run and test your Flutter app on the iOS simulator,
follow this procedure.

如果想要在 iOS 模拟器中运行和测试 Flutter 应用，按照以下步骤即可：

 1. If using Xcode 15 or greater, download and install the iOS Simulator 
    by running the following command:

    如果使用 Xcode 15 或更高的版本，
    请运行以下指令下载并安装 iOS 模拟器：

    ```terminal
    $ xcodebuild -downloadPlatform iOS
    ```

    If you want to use a different method of downloading and installing the 
    iOS Simulator, check out 
    [Apple's documentation on installing Simulators][] for more options.

    如果你想使用其他方式下载和安装 iOS 模拟器，请查阅 
    [Apple 文档中的安装模拟器][Apple's documentation on installing Simulators] 
    了解更多方案。

 1. To start the Simulator, run the following command:

    运行以下指令启动模拟器：

    ```terminal
    $ open -a Simulator
    ```

 1. Set your Simulator to use a 64-bit device (iPhone 5s or later).

    将模拟器设置使用为 64 位设备（iPhone 5s 或更新的设备）。

    - From Xcode, choose a simulator device type. Go to
      **Product** <span aria-label="and then">></span>
      **Destination** <span aria-label="and then">></span>
      Choose your target device.

      通过 Xcode 选择模拟器设备类型。
      打开 **Product** <span aria-label="and then">></span>
      **Destination** <span aria-label="and then">></span> 
      选择目标设备。

    - From the Simulator app, go to
      **File** <span aria-label="and then">></span>
      **Open Simulator** <span aria-label="and then">></span>
      Choose your target iOS device

      通过 Simulator app 选择模拟器设备。
      打开 **File** <span aria-label="and then">></span>
      **Open Simulator** <span aria-label="and then">></span> 
      选择目标设备。

    - To check the device version in the Simulator,
      open the **Settings** app <span aria-label="and then">></span>
      **General** <span aria-label="and then">></span>
      **About**.

      在模拟器中检查设备版本。
      打开 **Settings** app <span aria-label="and then">></span>
      **General** <span aria-label="and then">></span>
      **About**。

 1. The simulated high-screen density iOS devices might overflow your screen.
    If that appears true on your Mac, change the presented size in the
    Simulator app

    模拟的高分辨率 iOS 设备可能会溢出你的屏幕。
    如果在 Mac 上出现这种情况，
    请在 Simulator app 中更改显示大小。

    - To display the Simulator at a small size, go to
      **Window** <span aria-label="and then">></span>
      **Physical Size** or<br>press <kbd>Cmd</kbd> + <kbd>1</kbd>.

      以小尺寸显示模拟器，
      设置 **Window** <span aria-label="and then">></span>
      **Physical Size** 或者<br>快捷键 <kbd>Cmd</kbd> + <kbd>1</kbd>。

    - To display the Simulator at a moderate size, go to
      **Window** <span aria-label="and then">></span>
      **Point Accurate** or<br>press <kbd>Cmd</kbd> + <kbd>2</kbd>.

      以中尺寸显示模拟器，
      设置 **Window** <span aria-label="and then">></span>
      **Point Accurate** 或者<br>快捷键 <kbd>Cmd</kbd> + <kbd>2</kbd>。

    - To display the Simulator at an HD representation, go to
      **Window** <span aria-label="and then">></span>
      **Pixel Accurate** or<br>press <kbd>Cmd</kbd> + <kbd>3</kbd>.
      _The Simulator defaults to this size._

      以 HD 高清显示模拟器，
      设置 **Window** <span aria-label="and then">></span>
      **Pixel Accurate** 或者<br>快捷键 <kbd>Cmd</kbd> + <kbd>3</kbd>。

    - The Simulator defaults to **Fit Screen**.
      If you need to return to that size, go to
      **Window** <span aria-label="and then">></span>
      **Fit Screen** or press <kbd>Cmd</kbd> + <kbd>4</kbd>.

      模拟器默认为 **Fit Screen（适应屏幕）**。
      如果你需要恢复到该尺寸的设置，
      设置 **Window** <span aria-label="and then">></span>
      **Fit Screen** 或者<br>快捷键 <kbd>Cmd</kbd> + <kbd>4</kbd>。

### Deploy to physical iOS devices

### 部署到 iOS 真机

To deploy your Flutter app to a physical iPhone or iPad,
you need to do the following:

你需要执行以下操作，
将 Flutter 应用程序部署到 iPhone 或 iPad 真机上：

- Create an [Apple Developer][] account.

  创建 [Apple Developer][] 账户。

- Set up physical device deployment in Xcode.

  在 Xcode 中设置真机设备部署。

- Create a development provisioning profile to self-sign certificates.

  创建开发配置文件 (Provisioning Profile)，
  并自行签署证书 (Signing Certificate)。

- Install the third-party CocoaPods dependency manager
  if your app uses Flutter plugins.

  如果你的应用程序使用 Flutter 插件，
  请安装第三方 CocoaPods 依赖管理器。

#### Create your Apple ID and Apple Developer account

#### 创建 Apple ID 和 Apple Developer 账户

To test deploying to a physical iOS device, you need an Apple ID.

测试部署到 iOS 真机，你需要一个 Apple ID。

To distribute your app to the App Store,
you must enroll in the Apple Developer Program.

要在 App Store 发布你的应用程序，
你必须注册 Apple Developer Program。

If you only need to test deploying your app,
complete the first step and move on to the next section.

如果你只需要测试部署应用程序，
请完成第 1 步后继续下一节。

1. If you don't have an [Apple ID][], create one.

   如果你没有 [Apple ID][]，请创建一个。

1. If you haven't enrolled in the [Apple Developer][] program, enroll now.

   如果你未注册 [Apple Developer][] program，请立即注册。

   To learn more about membership types,
   check out [Choosing a Membership][].

   了解有关会员类型的更多信息，
   请查阅 [选择会员资格][Choosing a Membership]。

[Apple ID]: https://support.apple.com/en-us/HT204316

#### Attach your physical iOS device to your Mac {#attach}

#### 将 iOS 真机连接到 Mac {#attach}

Configure your physical iOS device to connect to Xcode.

配置你的 iOS 真机连接到 Xcode。

1. Attach your iOS device to the USB port on your Mac.

   将 iOS 设备连接到 Mac 的 USB 端口。

1. On first connecting your iOS device to your Mac,
   your iOS device displays the **Trust this computer?** dialog.

   首次将 iOS 设备连接到 Mac 时，
   你的 iOS 设备会显示 **信任这台电脑吗？** 的对话框。

1. Click **Trust**.

   点击 **信任**。

   ![Trust Mac][]{:.mw-100}

1. When prompted, unlock your iOS device.

   出现提示时，解锁你的 iOS 设备。

#### Enable Developer Mode on iOS 16 or later
{:.no_toc}

#### 在 iOS 16 或更高版本上启用开发者模式
{:.no_toc}

Starting with iOS 16, Apple requires you to enable **[Developer Mode][]**
to protect against malicious software.
Enable Developer Mode before deploying to a device running iOS 16 or later.

从 iOS 16 开始，Apple 要求你启用 **[开发者模式][Developer Mode]**，
以防止恶意软件。
在部署到 iOS 16 或更高版本的设备之前，请启用开发者模式。

1. Tap on **Settings** <span aria-label="and then">></span>
   **Privacy & Security** <span aria-label="and then">></span>
   **Developer Mode**.

   点击 **设置** <span aria-label="and then">></span>
   **隐私与安全性** <span aria-label="and then">></span>
   **开发者模式**。

1. Tap to toggle **Developer Mode** to **On**.

   将 **开发者模式** 切换为 **打开**。

1. Tap **Restart**.

   点击 **重新启动**。

1. After the iOS device restarts, unlock your iOS device.

   重新启动 iOS 设备后，解锁 iOS 设备。

1. When the **Turn on Developer Mode?** dialog appears, tap **Turn On**.

   当出现 **打开开发者模式吗？** 对话框时，点击 **打开**。

   The dialog explains that Developer Mode requires reducing the security
   of the iOS device.

   对话框会提示开发者模式会降低 iOS 设备的安全性。
   
1. Unlock your iOS device.

   解锁你的 iOS 设备。

#### Enable developer code signing certificates

#### 启用开发者代码签名证书 (signing certificates)

To deploy to a physical iOS device, you need to establish trust with your
Mac and the iOS device.
This requires you to load signed developer certificates to your iOS device.
To sign an app in Xcode,
you need to create a development provisioning profile.

在部署到 iOS 真机前，你需要在 Mac 与 iOS 设备之间建立信任。
这需要将签名的开发者证书加载到 iOS 设备上。
在 Xcode 中签署应用程序，
你需要创建一个开发者配置文件 (Provisioning Profile)。

Follow the Xcode signing flow to provision your project.

请按照 Xcode 签名流程配置你的项目。

1. Open Xcode.

   打开 Xcode。

1. Sign in to Xcode with your Apple ID.

   使用 Apple ID 登录 Xcode。

   {: type="a"}
   1. Go to **Xcode** <span aria-label="and then">></span>
      **Settings...*

      选择 **Xcode** <span aria-label="and then">></span>
      **Settings...*

   1. Click **Accounts**.

      点击 **Accounts**。

   1. Click **+**.

      点击 **+**。

   1. Select **Apple ID** and click **Continue**.

      选择 **Apple ID** 并点击 **Continue**。

   1. When prompted, enter your **Apple ID** and **Password**.

      出现提示时，请输入你的 **Apple ID** 和 **Password**。

   1. Close the **Settings** dialog.

      关闭 **Settings** 对话框。

   Development and testing supports any Apple ID.

   开发和测试支持任意 Apple ID。

1. Go to **File** <span aria-label="and then">></span> **Open...**

   打开 **File** <span aria-label="and then">></span> **Open...**

   You can also press <kbd>Cmd</kbd> + <kbd>O</kbd>.

   你还可以使用快捷键 <kbd>Cmd</kbd> + <kbd>O</kbd>。

1. Navigate to your Flutter project directory.

   导航至 Flutter 项目目录。

1. Open the default Xcode workspace in your project: `ios/Runner.xcworkspace`.

   打开项目中默认的 Xcode workspace：`ios/Runner.xcworkspace`。

1. Select the physical iOS device you intend to deploy to in the device
   drop-down menu to the right of the run button.

   在运行按钮右侧的设备下拉菜单中选择你要部署的 iOS 真机。

   It should appear under the **iOS devices** heading.

   它应该出现在 **iOS devices** 标题下方。

1. In the left navigation panel under **Targets**, select **Runner**.

   在左侧导航面板的 **Targets** 下，选择 **Runner**。

1. In the **Runner** settings pane, click **Signing & Capabilities**.

   在 **Runner** 设置窗内，点击 **Signing & Capabilities**。

1. Select **All** at the top.

   选择顶部的 **All**。

1. Select **Automatically manage signing**.

   选择 **Automatically manage signing**。

1. Select a team from the **Team** dropdown menu.

   从 **Team** 下拉菜单中选择一个团队。

   Teams are created in the **App Store Connect** section of your
   [Apple Developer Account][] page.
   If you have not created a team, you can choose a _personal team_.

   团队是在 [Apple Developer Account][] 页面的 **App Store Connect** 创建的。
   如果你尚未创建团队，可以选择 _个人团队 (personal team)_。

   The **Team** dropdown displays that option as **Your Name (Personal Team)**.

   **Team** 下拉菜单中会显示名为 **你的名称 (Personal Team)** 的选项。

   ![Xcode account add][]{:.mw-100}

   After you select a team, Xcode performs the following tasks:

   选择团队后，Xcode 会执行以下工作。

   {: type="a"}
   1. Creates and downloads a Development Certificate

      创建并下载开发证书

   1. Registers your device with your account,

      将设备注册到你的账户

   1. Creates and downloads a provisioning profile if needed

      根据需要创建并下载配置文件 (Provisioning Profile)

If automatic signing fails in Xcode, verify that the project's
**General** <span aria-label="and then">></span>
**Identity** <span aria-label="and then">></span>
**Bundle Identifier** value is unique.

如果在 Xcode 中自动签名失败，请检查项目的 **General** <span aria-label="and then">></span>
**Identity** <span aria-label="and then">></span>
**Bundle Identifier** 值是否唯一。

![Check the app's Bundle ID][]{:.mw-100}

#### Enable trust of your Mac and iOS device {#trust}

#### 启用 Mac 和 iOS 设备之间的信任 {#trust}

When you attach your physical iOS device for the first time,
enable trust for both your Mac and the Development Certificate
on the iOS device.

首次连接 iOS 真机时，
为你的 Mac 和 iOS 设备上的开发证书启用信任。

##### Agree to trust your Mac

##### 同意信任你的 Mac

You should enabled trust of your Mac on your iOS device when
you [attached the device to your Mac](#attach).

将你的设备连接到 Mac 时，需要 [启用 iOS 设备对 Mac 的信任](#attach)。

##### Enable developer certificate for your iOS devices

##### 为 iOS 设备启用开发者证书

Enabling certificates varies in different versions of iOS.

在不同版本的 iOS 中，启用证书的方式也不尽相同。

{% comment %} Nav tabs {% endcomment -%}
<ul class="nav nav-tabs" id="ios-versions" role="tablist">
    <li class="nav-item">
        <a class="nav-link" id="ios14-tab" href="#ios14" role="tab" aria-controls="ios14" aria-selected="true">iOS 14</a>
    </li>
    <li class="nav-item">
        <a class="nav-link" id="ios15-tab" href="#ios15" role="tab" aria-controls="ios15" aria-selected="false">iOS 15</a>
    </li>
    <li class="nav-item">
        <a class="nav-link active" id="ios16-tab" href="#ios16" role="tab" aria-controls="ios16" aria-selected="false">iOS 16 or later</a>
    </li>
</ul>

{% comment %} Tab panes {% endcomment -%}
<div class="tab-content">

<div class="tab-pane" id="ios14" role="tabpanel" aria-labelledby="ios14-tab" markdown="1">

1. Open the **Settings** app on the iOS device.

   打开 iOS 设备上的 **设置**。

1. Tap on **General** <span aria-label="and then">></span>
   **Profiles & Device Management**.

   点击 **通用** <span aria-label="and then">></span>
   **设备管理**。

1. Tap to toggle your Certificate to **Enable**

   点击你的证书切换为 **启用**。

</div>

<div class="tab-pane" id="ios15" role="tabpanel" aria-labelledby="ios15-tab" markdown="1">

1. Open the **Settings** app on the iOS device.

   打开 iOS 设备上的 **设置**。

1. Tap on **General** <span aria-label="and then">></span>
    **VPN & Device Management**.

   点击 **通用** <span aria-label="and then">></span>
   **VPN 与 设备管理**。

1. Tap to toggle your Certificate to **Enable**.

   点击你的证书切换为 **启用**。

</div>

<div class="tab-pane active" id="ios16" role="tabpanel" aria-labelledby="ios16-tab" markdown="1">

1. Open the **Settings** app on the iOS device.

   打开 iOS 设备上的 **设置**。

1. Tap on **General** <span aria-label="and then">></span>
    **VPN & Device Management**.

   点击 **通用** <span aria-label="and then">></span>
   **VPN 与 设备管理**。

1. Under the **Developer App** heading, you should find your certificate.

   在 **开发者应用** 标题下，你需要找到你的证书。

1. Tap your Certificate.

   点击你的证书。

1. Tap **Trust "\<certificate\>"**.

   点击 **信任 "\<certificate\>"**。

1. When the dialog displays, tap **Trust**.

   显示对话框时，点击 **信任**。

</div>
</div>{% comment %} End: Tab panes. {% endcomment -%}

If prompted, enter your Mac password into the
**codesign wants to access key...** dialog and tap **Always Allow**.

如果出现提示，请在 **codesign 想要访问密钥...** 的对话框中输入 Mac 密码，
然后点击 **始终允许**。

#### Optional deployment procedures

#### 可选的部署步骤

You can skip these procedures. They enable additional debugging features.

你可以跳过这些步骤。
它们可以启用更多调试功能。

##### Set up wireless debugging on your iOS device

##### 在 iOS 设备上设置无线调试

Follow this procedure to debug your device using a Wi-Fi connection.

按照以下步骤使用 Wi-Fi 连接调试设备。

To use wireless debugging:

使用无线调试：

- Connect your iOS device to the same network as your macOS device.

  将 iOS 设备连接到与 macOS 设备相同的网络。

- Set a passcode for your iOS device.

  为 iOS 设备设置密码。

After you connect your iOS device to your Mac:

将 iOS 设备连接到 Mac 后：

1. Open **Xcode**.

   打开 **Xcode**。

1. Go to **Window** <span aria-label="and then">></span>
   **Devices and Simulators**.

   选择 **Window** <span aria-label="and then">></span>
   **Devices and Simulators**。

   You can also press <kbd>Shift</kbd> + <kbd>Cmd</kbd> + <kbd>2</kbd>.

   你还可以使用快捷键 <kbd>Shift</kbd> + <kbd>Cmd</kbd> + <kbd>2</kbd>。

1. Select your iOS device.

   选择你的 iOS 设备。

1. Select **Connect via Network**.

   选择 **Connect via Network**。

1. Once the network icon appears next to the device name,
   unplug your iOS device from your Mac.

   一旦设备名称旁边出现网络图标，
   请将 iOS 设备从 Mac 拔下。

If you don't see your device listed when using `flutter run`,
extend the timeout. The timeout defaults to 10 seconds.
To extend the timeout, change the value to an integer greater than 10.

如果在使用 `flutter run` 时没有看到设备列表，请延长超时时间。
超时默认为 10 秒。
要延长超时时间，请将值改为大于 10 的整数。

```terminal
flutter run --device-timeout 60
```

###### Learn more about wireless debugging

###### 进一步了解无线调试

- To learn more, check out
  [Apple's documentation on pairing a wireless device with Xcode][].

  了解更多信息，请查阅 
  [Apple 文档中的 pairing a wireless device with Xcode][Apple's documentation on pairing a wireless device with Xcode]。

- To troubleshoot, check out [Apple's Developer Forums][].

  要排除故障，请访问 [Apple's Developer Forums][]。

- To learn how to configure wireless debugging with `flutter attach`,
  check out [Debugging your add-to-app module][].

  要了解如何使用 `flutter attach` 配置无线调试，
  请查阅 [在混合开发模式下进行调试][Debugging your add-to-app module]。


##### Install CocoaPods

##### 安装 CocoaPods

Follow this procedure if your apps depend on [Flutter plugins][]
with native iOS code.

如果你的应用程序依赖于带有原生 iOS 代码的 [Flutter 插件][Flutter plugins]，
请遵循此步骤。

To [Install and set up CocoaPods][], run the following commands:

请运行以下指令，[安装并设置 CocoaPods][Install and set up CocoaPods]：

```terminal
$ sudo gem install cocoapods
```

{{site.alert.note}}

  The default version of Ruby requires `sudo` to install the CocoaPods gem.
  If you are using a Ruby Version manager, you might need to run without `sudo`.

  Ruby 的默认版本需要 root 权限 `sudo` 来安装 CocoaPods gem，
  如果你使用的是 Ruby Version 管理器，可能就无需 root 权限。

  Additionally, if you are installing on an [Apple Silicon Mac][],
  run the command:

  除此之外，如果你是在 Apple 芯片的 Mac 上安装，则需要运行下面的命令：

  ```terminal
  $ sudo gem uninstall ffi && sudo gem install ffi -- --enable-libffi-alloc
  ```

{{site.alert.end}}

[Check the app's Bundle ID]: {{site.url}}/assets/images/docs/setup/xcode-unique-bundle-id.png
[Choosing a Membership]: {{site.apple-dev}}/support/compare-memberships
[Mac App Store]: https://itunes.apple.com/us/app/xcode/id497799835
[Flutter plugins]: {{site.url}}/packages-and-plugins/developing-packages#types
[Install and set up CocoaPods]: https://guides.cocoapods.org/using/getting-started.html#installation
[Trust Mac]: {{site.url}}/assets/images/docs/setup/trust-computer.png
[web download]: {{site.apple-dev}}/xcode/
[Xcode account add]: {{site.url}}/assets/images/docs/setup/xcode-account.png
[Apple Silicon Mac]: https://support.apple.com/en-us/HT211814
[Developer Mode]: {{site.apple-dev}}/documentation/xcode/enabling-developer-mode-on-a-device
[Apple's Developer Forums]: {{site.apple-dev}}/forums/
[Debugging your add-to-app module]: {{site.url}}/add-to-app/debugging/#wireless-debugging
[Apple's documentation on pairing a wireless device with Xcode]: https://help.apple.com/xcode/mac/9.0/index.html?localePath=en.lproj#/devbc48d1bad
[Apple Developer]: {{site.apple-dev}}/programs/
[Apple Developer Account]: {{site.apple-dev}}/account
[Apple's documentation on installing Simulators]: {{site.apple-dev}}/documentation/xcode/installing-additional-simulator-runtimes
