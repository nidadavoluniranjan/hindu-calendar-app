# Mobile Setup Guide - Flutter

## Prerequisites
- Flutter SDK 3.0+ (Download from https://flutter.dev/docs/get-started/install)
- Dart SDK (included with Flutter)
- Android Studio or Xcode (for emulators)
- For iOS: macOS with Xcode
- For Android: Android SDK

## Installation Steps

### 1. Install Flutter SDK

**macOS/Linux:**
```bash
git clone https://github.com/flutter/flutter.git -b stable
export PATH="$PATH:`pwd`/flutter/bin"
flutter doctor
```

**Windows:**
- Download Flutter SDK from https://flutter.dev/docs/get-started/install/windows
- Extract to a desired location
- Add Flutter to PATH environment variable
- Run `flutter doctor` in cmd/PowerShell

### 2. Verify Installation

```bash
flutter doctor
flutter --version
```

### 3. Create Flutter Project

```bash
cd mobile
flutter create hindu_calendar_flutter
cd hindu_calendar_flutter
```

## Project Structure

```
hindu_calendar_flutter/
├── android/              # Android native code
├── ios/                  # iOS native code
├── lib/
│   ├── models/          # Data models
│   ├── screens/         # UI screens
│   ├── widgets/         # Reusable widgets
│   ├── services/        # API services
│   ├── providers/       # State management
│   ├── utils/           # Utilities
│   └── main.dart        # Entry point
├── assets/
│   ├── images/
│   ├── icons/
│   └── translations/    # i18n JSON files
├── test/               # Unit tests
├── pubspec.yaml        # Dependencies
└── README.md
```

## Step 1: Update pubspec.yaml

```yaml
name: hindu_calendar_flutter
description: Hindu Calendar Application for iOS and Android
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  
  # HTTP & Networking
  dio: ^5.3.0
  
  # State Management
  provider: ^6.0.0
  
  # Local Storage
  hive: ^2.2.0
  hive_flutter: ^1.1.0
  
  # Date & Time
  intl: ^0.18.0
  
  # Localization
  easy_localization: ^3.0.0
  
  # UI
  flutter_bloc: ^8.1.0
  cupertino_icons: ^1.0.0
  
  # Authentication
  flutter_secure_storage: ^8.1.0
  jwt_decoder: ^2.0.1
  
  # Connectivity
  connectivity_plus: ^5.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^2.0.0
  build_runner: ^2.4.0
  hive_generator: ^2.0.0

flutter:
  uses-material-design: true
  
  assets:
    - assets/images/
    - assets/icons/
    - assets/translations/
```

## Step 2: Get Dependencies

```bash
cd hindu_calendar_flutter
flutter pub get
```

## Step 3: Generate Build Files (for Hive)

```bash
flutter pub run build_runner build
```

## Step 4: Android Setup

### Android Studio Configuration
1. Open `android/` folder in Android Studio
2. Sync Gradle files
3. Install SDK versions if needed

### Minimum SDK Version
Edit `android/app/build.gradle`:
```gradle
android {
    compileSdkVersion 34
    
    defaultConfig {
        minSdkVersion 21
        targetSdkVersion 34
    }
}
```

### Internet Permission
Edit `android/app/src/AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## Step 5: iOS Setup

### Update iOS Deployment Target
Edit `ios/Podfile`:
```ruby
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
    target.build_configurations.each do |config|
      config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
        '$(inherited)',
        'PERMISSION_LOCATION=1',
      ]
    end
  end
end
```

### Minimum iOS Version
In Xcode:
1. Open `ios/Runner.xcworkspace`
2. Select Runner
3. Build Settings → Minimum Deployments → Set to 12.0+

### Internet Security
Edit `ios/Runner/Info.plist`:
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

## Step 6: Setup Localization

### Create Translation Files

```
assets/translations/
├── en.json
├── hi.json
├── te.json
├── ta.json
├── kn.json
└── ml.json
```

### Example: en.json
```json
{
  "app_title": "Hindu Calendar",
  "calendar": "Calendar",
  "events": "Events",
  "festivals": "Festivals",
  "settings": "Settings",
  "logout": "Logout",
  "home": "Home"
}
```

### Configure Easy Localization in main.dart
```dart
import 'package:easy_localization/easy_localization.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await EasyLocalization.ensureInitialized();
  
  runApp(
    EasyLocalization(
      supportedLocales: [
        Locale('en'),
        Locale('hi'),
        Locale('te'),
        Locale('ta'),
        Locale('kn'),
        Locale('ml'),
      ],
      path: 'assets/translations',
      fallbackLocale: Locale('en'),
      child: MyApp(),
    ),
  );
}
```

## Step 7: Run on Emulator/Device

### Android
```bash
# List available emulators
flutter emulators

# Start emulator
flutter emulators --launch <emulator_name>

# Run app
flutter run
```

### iOS
```bash
# List connected devices
flutter devices

# Run on iOS simulator
flutter run -d <device_id>

# Run on physical device
flutter run
```

## Step 8: Key Directories

### lib/models/
- user.dart
- event.dart
- festival.dart
- panchang.dart
- auth_response.dart

### lib/screens/
- home_screen.dart
- calendar_screen.dart
- event_screen.dart
- festival_screen.dart
- panchang_screen.dart
- login_screen.dart
- settings_screen.dart

### lib/services/
- api_service.dart
- auth_service.dart
- calendar_service.dart
- event_service.dart
- storage_service.dart

### lib/providers/
- auth_provider.dart
- calendar_provider.dart
- event_provider.dart
- ui_provider.dart

### lib/widgets/
- calendar_widget.dart
- event_card.dart
- festival_card.dart
- panchang_card.dart
- custom_app_bar.dart

## Step 9: Build Release APK/IPA

### Android Release APK
```bash
flutter build apk --release
# Output: build/app/outputs/flutter-apk/app-release.apk
```

### Android App Bundle
```bash
flutter build appbundle --release
# Output: build/app/outputs/bundle/release/app-release.aab
```

### iOS Release
```bash
flutter build ios --release
# Then upload to App Store via Xcode or Transporter
```

## Common Commands

```bash
# Check Flutter status
flutter doctor

# Clean build
flutter clean

# Get dependencies
flutter pub get

# Run tests
flutter test

# Analyze code
flutter analyze

# Format code
dart format .

# Build runner
flutter pub run build_runner build

# Run with debug info
flutter run -v

# Build for specific device
flutter run -d <device_id>
```

## Troubleshooting

### Port Already in Use
```bash
flutter run --no-devtools
```

### Clear Cache
```bash
flutter clean
flutter pub get
```

### Gradle Issues (Android)
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
```

### Podfile Lock Issues (iOS)
```bash
cd ios
rm Podfile.lock
pod install
cd ..
flutter clean
flutter pub get
```

## Testing

### Unit Tests
```bash
flutter test test/unit_test.dart
```

### Integration Tests
```bash
flutter test integration_test/app_test.dart
```

## Deployment

### Google Play Store
1. Create signing key
2. Build app bundle
3. Create release in Play Console
4. Upload bundle

### Apple App Store
1. Create certificate in Apple Developer
2. Create app in App Store Connect
3. Build release archive
4. Upload with Transporter

## Performance Tips

- Use const constructors
- Avoid rebuilds with Provider/BLoC
- Use cached images
- Optimize list views with ListView.builder
- Profile with DevTools

## Security

- Store tokens in secure storage (flutter_secure_storage)
- Use HTTPS for API calls
- Implement certificate pinning
- Validate JWT tokens
- Never hardcode sensitive data
