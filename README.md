# react-native-speak

A wonderful TTS (text-to-speech) library for [React Native](https://github.com/facebook/react-native).

## TOC

* [Installation](#installation)
* [Linking](#linking)
* [Usage](#usage)
* [API](#api)

## Installation

Using npm:

```shell
npm install --save react-native-speak
```

or using yarn:

```shell
yarn add react-native-speak
```

## Linking

### Automatic

```shell
react-native link react-native-speak
```

*For iOS users using Pods:*
You need to run `pod install` after running the above link command inside your `ios` folder.

### Manual

<details>
    <summary>iOS (via CocoaPods)</summary>

Add the following line to your build targets in your `Podfile`

`pod 'RNSpeak', :path => '../node_modules/react-native-speak'`

Then run `pod install`

</details>

<details>
    <summary>iOS (without CocoaPods)</summary>

In XCode, in the project navigator:

* Right click _Libraries_
* Add Files to _[your project's name]_
* Go to `node_modules/react-native-speak`
* Add the `.xcodeproj` file

In XCode, in the project navigator, select your project.

* Add the `libRNSpeak.a` from the _RNSpeak_ project to your project's _Build Phases ➜ Link Binary With Libraries_
* Click `.xcodeproj` file you added before in the project navigator and go the _Build Settings_ tab. Make sure _All_ is toggled on (instead of _Basic_).
* Look for _Header Search Paths_ and make sure it contains both `$(SRCROOT)/../react-native/React` and `$(SRCROOT)/../../React`
* Mark both as recursive (should be OK by default).

Run your project (Cmd+R)

</details>

<details>
    <summary>Android</summary>

* **_optional_** in `android/build.gradle`:

```gradle
...
  ext {
    // dependency versions
    googlePlayServicesVersion = "<Your play services version>" // default: "+"
    compileSdkVersion = "<Your compile SDK version>" // default: 23
    buildToolsVersion = "<Your build tools version>" // default: "25.0.2"
    targetSdkVersion = "<Your target SDK version>" // default: 22
  }
...
```

* in `android/app/build.gradle`:

```diff
dependencies {
    ...
    implementation "com.facebook.react:react-native:+"  // From node_modules
+   implementation project(':react-native-speak')
}
```

* in `android/settings.gradle`:

```diff
...
include ':app'
+ include ':react-native-speak'
+ project(':react-native-speak').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-speak/android')
```

* in `MainApplication.java`:

```diff
+ import com.truckmap.RNSpeak.RNSpeak;

  public class MainApplication extends Application implements ReactApplication {
    //......

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
+         new RNSpeak(),
          new MainReactPackage()
      );
    }

    ......
  }
```

NOTE: If you faced with this error: `Could not resolve all files for configuration ':react-native-speak:debugCompileClasspath'.`, in `build.gradle` put `google()` in the first line (according to https://stackoverflow.com/a/50748249)

* in `android/build.gradle`:

```diff
allprojects {
    repositories {
+       google()
        ...
    }
}
```
</details>

## Usage

```js
import Speech from 'react-native-speak';
```

## API

| Method                                                            | Return Type         |  iOS | Android |
| ----------------------------------------------------------------- | ------------------- | :--: | :-----: |
| [speak()](#speak)                                     | `Promise<any>`            |  ✅  |   ✅    |

---

### speak()

```
speak(text: string)
```

Speaks a phrase.

**Examples**

```js
Speech.speak("hello world!"); // speaks the given phrase.
```
---

## Events

### onSpeechStart

Fired when speech has started.

**Examples**

```js
import { NativeEventEmitter, NativeModules } from 'react-native'
const speechEventEmitter = new NativeEventEmitter(NativeModules.RNSpeak)

speechEventEmitter.addListener('onSpeechStart', () => {
  // callback when finished
});
```

---

### onSpeechEnd

Fired when speech has ended.

**Examples**

```js
import { NativeEventEmitter, NativeModules } from 'react-native'
const speechEventEmitter = new NativeEventEmitter(NativeModules.RNSpeak)

speechEventEmitter.addListener('onSpeechEnd', () => {
  // callback when finished
});
```

---

### onSpeechError

Fired when an error is found in the speech pipeline. (TBD)

**Examples**

```js
import { NativeEventEmitter, NativeModules } from 'react-native'
const speechEventEmitter = new NativeEventEmitter(NativeModules.RNSpeak)

speechEventEmitter.addListener('onSpeechError', error => {
  console.error(error);
});
```

---

## Release Notes

See the [CHANGELOG.md](/CHANGELOG.md).

## Contributing

Please see the [`contributing guide`](/CONTRIBUTING.md).
