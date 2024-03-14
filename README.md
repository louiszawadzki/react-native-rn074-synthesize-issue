# react-native-rn074-synthesize-issue

Demo for issue on RN 0.74.

This module contains a very simple code logging the bridge value:

```obj-c
@implementation Rn074SynthesizeIssue

@synthesize bridge = _bridge;
RCT_EXPORT_MODULE()

// Example method
// See // https://reactnative.dev/docs/native-modules-ios
RCT_EXPORT_METHOD(multiply:(double)a
                  b:(double)b
                  resolve:(RCTPromiseResolveBlock)resolve
                  reject:(RCTPromiseRejectBlock)reject)
{
    NSNumber *result = @(a * b);
    NSLog(@"Bridge is: %@", _bridge.description);

    resolve(result);
}
@end
```

When bridgeless mode is on, the bridge is null.

## Setup

```sh
yarn
cd example
yarn
(cd ios && RCT_NEW_ARCH_ENABLED=1 pod install)
```

## Reproducing the issue

Open the app on Xcode `(cd example/ && xed ios)`, then run the app.

When the app launches, in the Xcode logs you should see:

```
Bridgeless mode is enabled
Running "example
Bridge is: (null)
```

When you turn bridgeless mode off by uncommenting the code in `AppDelegate.mm`, you get as expected:

```
Running "example
Bridge is: <RCTCxxBridge: 0x10540cb00>
```

---

Made with [create-react-native-library](https://github.com/callstack/react-native-builder-bob)
