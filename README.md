# flutter_siren_2

This fork of [flutter_siren](https://pub.dev/packages/flutter_siren/example) fixes a few problems with `Android API 33` and has `up-to-date` dependencies (28 Nov. 2023). 

I created the fork mainly because I couldn't compile flutter_siren with a current flutter installation with (Android) because the dependencies were out-of-date and additionally some customization was needed to target API 33 from Android. Unfortunately, the original repo has been archived and is no longer maintained.

## Install

```sh
$ flutter pub add flutter_siren_2
```

[New Pub Dev Page](https://pub.dev/packages/flutter_siren_2)

# 🚨 flutter_siren (Original Readme)



The Flutter port of the popular [Siren](https://github.com/ArtSabintsev/Siren), one way to notify users when a new version of your app is available and prompt them to upgrade.

🚀 Supports iOS, Android and MacOS.

## Requirements
Your package must follow the [Semantic Versioning](https://semver.org/)

## Install
Add this to your package's pubspec.yaml file:

```yaml
dependencies:
  flutter_siren_2: <latest-version>
```

And install the packages from the command line:

```sh
$ flutter pub get
```

## Usage

```dart
import 'package:flutter/material.dart';
import 'package:flutter_siren_2/flutter_siren_2.dart';

// Check update on button press with AlertDialog.

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Builder(
          builder: (context) {
            return Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  FlatButton(
                    child: Text('Check Update'),
                    onPressed: () {
                      final siren = Siren();
                      siren.promptUpdate(context);
                    },
                  )
                ],
              ),
            );
          }
        )
      ),
    );
  }
}

```

## Customizing the prompt update. 

| value             | Description             | default |
| -------------     |-------------            | -----|
|title              | Alert title             | Update Available |
|message            | Alert Message           | There is an updated version available on the App Store. Would you like to upgrade? |
|buttonUpgradeText  | Upgrade Button Text     | Upgrade |
|buttonCancelText   | Cancel Button Text      | Cancel |
|forceUpgrade       | Hide Cancel Button      | false |

```dart
// Passing custom options.
siren.promptUpdate(context, 
  title: "My alert title", 
  message: "Bro, update my app", 
  buttonUpgradeText: "Download",  
  buttonCancelText: "Nop",
  forceUpgrade: true
);
```

## Building your own prompt update.

Your can use the `updateIsAvailable` method to create your own way to alert the user about new updates. This method returns a boolean and you do your magic!  
```dart 
final siren = Siren();

FutureBuilder<bool>(
  future: siren.updateIsAvailable(),
  builder: (context, AsyncSnapshot<bool> snapshot){ 
    if (snapshot.hasData) {
      return AlertDialog(
        title: Text(title),
        content: Text(message),
        actions: <Widget>[],
      );
    }
  }
);
```

## Accessing store and local versions

Your can use the `localVersion` or `storeVersion` getters to access the current version status of your app!  
```dart 
final siren = Siren();

final local = siren.localVersion;
final store = siren.storeVersion;
```

## Inspiration
These awesome packages: [Siren](https://github.com/ArtSabintsev/Siren) and [react-native-siren](https://github.com/GantMan/react-native-siren)
