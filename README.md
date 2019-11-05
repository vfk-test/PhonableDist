# VerifyKit

VerifyKit is a framework to easily integrate phone number validation flow to your mobile application.

## Installation

You can install framework via CocoaPods.

```bash
pod 'VerifyKit', :git => 'https://github.com/vfk-test/PhonableDist.git'
```

Or you can [click here](http://www.google.com) to download the framework and add the files via drag and drop.

After you added the files to your project, you need to add both frameworks to ```Frameworks, Libraries, and Embedded Content``` panel in your Project's general settings, then set ```Embed``` option as ```Embed & Sign```.

## Basic Usage

To successfully use the framework, you need to add ```VerifyKitKey``` and ```VerifyKitSecret``` to your plist file. This step is mandantory.

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
    
    func didCompleteLogin(with sessionCode: String) {
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


## Options Struct

You can change the settings declared in ```VerifyKitOptions``` struct.

```swift
public struct VerifyKitOptions {
    var environment: VerifyKitEnvironment
    var logActive: Bool
    var theme: VerifyKitTheme
}


public enum VerifyKitEnvironment {
    
    /// Stage environment for debug
    case debug
    
    /// Production environment for distribution
    case prod
}

public struct VerifyKitTheme {
    public var navigationBarBackgroundColor: UIColor
    public var statusBarColor: UIStatusBarStyle
}
```
