# VerifyKit

VerifyKit is a framework to easily integrate phone number validation flow to your mobile application.

## Requirements

This framework requires the latest version of Xcode.

## Installation

You can install framework via CocoaPods.

```bash
pod 'VerifyKit', :git => 'https://github.com/vfk-test/PhonableDist.git'
```

## Manual Installation

Or you can [click here](http://www.google.com) to download the framework and add the files via drag and drop.

If you choose to use the SDK manually, after you added the files to your project, you need to add both frameworks to ```Frameworks, Libraries, and Embedded Content``` panel in your Project's general settings, then set ```Embed``` option as ```Embed & Sign```.

## Configure Info.plist

To successfully use the framework, you need to add ```VerifyKitKey``` and ```VerifyKitSecret``` to your plist file. This step is mandatory.

After user chooses to validate the phone number with a third party messaging app, the SDK needs to return to main app.
To successfully complete this flow, you need to add ```vfk{your-verifykit-key}``` as URL Scheme to your plist file.

Open your Info.plist as source code and insert the following XML snippet into the body of your file just before the final </dict> element.

```
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>vfk{your-verifykit-key}</string>
    </array>
  </dict>
</array>
<key>VerifyKitKey</key>
<string>{your-verifykit-key}</string>
<key>VerifyKitSecret</key>
<string>{your-verifykit-secret-key}</string>
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>whatsapp</string>
  <string>tg</string>
  <string>viber</string>
</array>
```

## Usage

```swift
import VerifyKit


let kit = VerifyKit()
let viewController = kit.viewControllerForLogin()
self.present(viewController, animated: true, completion: nil)
```

You can get the result via ```VerifyKitDelegate``` protocol.

```swift

viewController.kitDelegate = self

extension ViewController: VerifyKitDelegate {

    func didSuccess(with sessionCode: String) {
        print("VerifyKitDelegate didCompleteLogin sessionCode:\(sessionCode)")
    }

    func didFail(with error: VerifyKitError) {
        print("VerifyKitDelegate didFail error:\(error)")
    }
}
```

## Configuration

```swift
let options = VerifyKitOptions(logActive: true)
let kit = VerifyKit(options: options)
```


## VerifyKitOptions Struct

You can change the settings declared in ```VerifyKitOptions``` struct.

```swift
public struct VerifyKitOptions {
    var environment: VerifyKitEnvironment = .debug // default
    var logActive: Bool = true // default
    var theme: VerifyKitTheme = VerifyKitTheme()
}

public enum VerifyKitEnvironment {

    /// Stage environment for debug
    case debug

    /// Production environment for distribution
    case prod
}

public struct VerifyKitTheme {
    public var appName: String = "VerifyKit" // default
    public var statusBarColor: UIStatusBarStyle = .lightContent // default
    public var navigationBarBackgroundColor: UIColor = .blue // default
    public var navigationBarForegroundColor: UIColor = .white // default
}
```

## Dependencies

VerifyKit uses the CryptoSwift for network traffic encryption.

## Notes

Before your app release, please change the VerifyKitEnvironment to 'prod' instead of 'debug'.
