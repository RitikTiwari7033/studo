# 📚 Studo — Flutter Study App

<p align="center">
  <img src="assets/images/logo.png" alt="Studo Logo" width="120"/>
</p>

<p align="center">
  <a href="https://flutter.dev"><img src="https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter" alt="Flutter"/></a>
  <a href="https://dart.dev"><img src="https://img.shields.io/badge/Dart-3.x-0175C2?logo=dart" alt="Dart"/></a>
  <img src="https://img.shields.io/badge/Platform-Android%20%7C%20iOS-green" alt="Platform"/>
  <img src="https://img.shields.io/badge/License-MIT-blue" alt="License"/>
</p>

---

## 📖 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Running the App](#-running-the-app)
- [Asset Documentation](#-asset-documentation)
- [pubspec.yaml Reference](#-pubspecyaml-reference)
- [Environment Configuration](#-environment-configuration)
- [Build & Release](#-build--release)
- [Testing](#-testing)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📌 About

**Studo** is a Flutter-based mobile application designed to help students manage their study sessions, track progress, organize notes, and stay on top of assignments — all from one clean, minimal interface.

---

## ✨ Features

- 🗂️ Subject & topic organizer
- ⏱️ Study timer with Pomodoro support
- 📝 Notes with rich text editing
- 📅 Assignment & deadline tracker
- 📊 Progress analytics dashboard
- 🔔 Push notifications for reminders
- 🌙 Dark / Light mode support
- 🔐 Authentication (Email + Google Sign-In)

---

## 📱 Screenshots

| Home | Notes | Timer | Analytics |
|------|-------|-------|-----------|
| ![Home](assets/screenshots/home.png) | ![Notes](assets/screenshots/notes.png) | ![Timer](assets/screenshots/timer.png) | ![Analytics](assets/screenshots/analytics.png) |

> Add actual screenshots to `assets/screenshots/` and update the table above.

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| UI Framework | Flutter 3.x |
| Language | Dart 3.x |
| State Management | Riverpod / Provider |
| Local Database | Hive / SQLite (via `sqflite`) |
| Remote Backend | Firebase (Firestore, Auth, Storage) |
| Navigation | GoRouter |
| Notifications | `flutter_local_notifications` |
| Dependency Injection | `get_it` |
| HTTP Client | `dio` |
| Animations | `flutter_animate` |

---

## 🗂 Project Structure

```
studo/
├── android/                    # Android native project
├── ios/                        # iOS native project
├── assets/
│   ├── fonts/                  # Custom fonts
│   ├── icons/                  # App icons (SVG/PNG)
│   ├── images/                 # General images & illustrations
│   ├── lottie/                 # Lottie animation files (.json)
│   └── screenshots/            # App store / README screenshots
├── lib/
│   ├── main.dart               # Entry point
│   ├── app.dart                # Root widget, theme setup
│   ├── core/
│   │   ├── constants/          # App-wide constants (colors, sizes, strings)
│   │   ├── errors/             # Error handling classes
│   │   ├── extensions/         # Dart extensions
│   │   ├── router/             # GoRouter configuration
│   │   ├── theme/              # Light & dark theme definitions
│   │   └── utils/              # Utility functions & helpers
│   ├── data/
│   │   ├── datasources/        # Remote (Firebase) and local (Hive/SQLite) sources
│   │   ├── models/             # Data models (JSON serializable)
│   │   └── repositories/       # Repository implementations
│   ├── domain/
│   │   ├── entities/           # Business logic entities
│   │   ├── repositories/       # Abstract repository contracts
│   │   └── usecases/           # Use case classes
│   ├── presentation/
│   │   ├── pages/              # Full-screen page widgets
│   │   ├── widgets/            # Reusable UI components
│   │   └── providers/          # State management (Riverpod/Provider)
│   └── services/
│       ├── auth_service.dart
│       ├── notification_service.dart
│       └── storage_service.dart
├── test/
│   ├── unit/                   # Unit tests
│   ├── widget/                 # Widget tests
│   └── integration/            # Integration tests
├── pubspec.yaml
└── README.md
```

---

## ✅ Prerequisites

Before you begin, make sure you have the following installed:

| Tool | Version | Install Link |
|------|---------|-------------|
| Flutter SDK | ≥ 3.10.0 | [flutter.dev](https://flutter.dev/docs/get-started/install) |
| Dart SDK | ≥ 3.0.0 | Bundled with Flutter |
| Android Studio | Latest | [developer.android.com](https://developer.android.com/studio) |
| Xcode (macOS only) | ≥ 14.x | Mac App Store |
| CocoaPods (macOS only) | Latest | `sudo gem install cocoapods` |
| Git | Latest | [git-scm.com](https://git-scm.com) |
| VS Code (optional) | Latest | [code.visualstudio.com](https://code.visualstudio.com) |

### Verify Flutter Installation

```bash
flutter doctor -v
```

All items should show a ✅. Resolve any issues shown before continuing.

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/RitikTiwari7033/studo.git
cd studo
```

### 2. Install Flutter Dependencies

```bash
flutter pub get
```

### 3. Firebase Setup

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project named `studo`.
2. Add an **Android** app:
   - Package name: `com.yourdomain.studo`
   - Download `google-services.json` → place it in `android/app/`
3. Add an **iOS** app:
   - Bundle ID: `com.yourdomain.studo`
   - Download `GoogleService-Info.plist` → place it in `ios/Runner/`
4. Enable **Authentication** (Email/Password + Google Sign-In)
5. Enable **Firestore Database** (start in test mode for development)
6. Enable **Firebase Storage**

### 4. Android Configuration

Open `android/app/build.gradle` and update:

```gradle
android {
    compileSdkVersion 34

    defaultConfig {
        applicationId "com.yourdomain.studo"
        minSdkVersion 21
        targetSdkVersion 34
        versionCode 1
        versionName "1.0.0"
    }
}
```

Open `android/build.gradle` and ensure the `classpath` for Google Services is present:

```gradle
dependencies {
    classpath 'com.google.gms:google-services:4.4.0'
}
```

### 5. iOS Configuration

```bash
cd ios
pod install
cd ..
```

Open `ios/Runner/Info.plist` and add your Google Sign-In URL scheme (from `GoogleService-Info.plist`):

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>YOUR_REVERSED_CLIENT_ID</string>
    </array>
  </dict>
</array>
```

### 6. Environment Variables

Create a `.env` file in the root (never commit this):

```env
FIREBASE_API_KEY=your_api_key
FIREBASE_PROJECT_ID=studo-xxxxx
FIREBASE_APP_ID=1:xxxxx:android:xxxxx
```

Install `flutter_dotenv`:

```yaml
# pubspec.yaml
dependencies:
  flutter_dotenv: ^5.1.0
```

Load in `main.dart`:

```dart
import 'package:flutter_dotenv/flutter_dotenv.dart';

void main() async {
  await dotenv.load(fileName: ".env");
  runApp(const App());
}
```

---

## ▶️ Running the App

### Development

```bash
# List available devices
flutter devices

# Run on a specific device
flutter run -d <device_id>

# Run on all connected devices
flutter run -d all

# Run with verbose logging
flutter run -v
```

### Hot Reload vs Hot Restart

| Command | What it does |
|---------|-------------|
| `r` (in terminal) | Hot Reload — injects changed code, preserves state |
| `R` (in terminal) | Hot Restart — full restart, clears state |
| `q` | Quit the app |

### Run Flavors (if configured)

```bash
# Development
flutter run --flavor dev -t lib/main_dev.dart

# Production
flutter run --flavor prod -t lib/main_prod.dart
```

---

## 🎨 Asset Documentation

All assets live under the `assets/` directory and must be declared in `pubspec.yaml`.

### Directory Overview

```
assets/
├── fonts/
│   ├── Poppins-Regular.ttf
│   ├── Poppins-Medium.ttf
│   ├── Poppins-SemiBold.ttf
│   └── Poppins-Bold.ttf
│
├── icons/
│   ├── app_icon.png            # 1024×1024 app icon source
│   ├── ic_home.svg
│   ├── ic_notes.svg
│   ├── ic_timer.svg
│   ├── ic_analytics.svg
│   └── ic_settings.svg
│
├── images/
│   ├── logo.png                # App logo (512×512 recommended)
│   ├── onboarding_1.png
│   ├── onboarding_2.png
│   ├── onboarding_3.png
│   ├── empty_notes.png         # Empty state illustration
│   ├── empty_tasks.png
│   └── bg_gradient.png         # Background gradient image
│
├── lottie/
│   ├── loading.json            # Loading spinner animation
│   ├── success.json            # Success checkmark animation
│   └── empty.json              # Empty state animation
│
└── screenshots/
    ├── home.png
    ├── notes.png
    ├── timer.png
    └── analytics.png
```

### Asset Naming Conventions

| Type | Convention | Example |
|------|-----------|---------|
| Icons | `ic_<name>.svg` | `ic_home.svg` |
| Images | `<context>_<name>.png` | `onboarding_1.png` |
| Lottie | `<action>.json` | `loading.json` |
| Fonts | `<Family>-<Weight>.ttf` | `Poppins-Bold.ttf` |

### Using Assets in Code

```dart
// Image
Image.asset('assets/images/logo.png')

// Icon (SVG with flutter_svg)
SvgPicture.asset('assets/icons/ic_home.svg', width: 24, height: 24)

// Lottie animation
Lottie.asset('assets/lottie/loading.json', width: 200)

// Font (applied via ThemeData)
TextStyle(fontFamily: 'Poppins', fontWeight: FontWeight.w600)
```

### App Icon Generation

Install `flutter_launcher_icons`:

```yaml
dev_dependencies:
  flutter_launcher_icons: ^0.13.1

flutter_launcher_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/icons/app_icon.png"
  min_sdk_android: 21
  adaptive_icon_background: "#FFFFFF"
  adaptive_icon_foreground: "assets/icons/app_icon_foreground.png"
```

Run:

```bash
dart run flutter_launcher_icons
```

### Splash Screen Generation

Install `flutter_native_splash`:

```yaml
dev_dependencies:
  flutter_native_splash: ^2.3.9

flutter_native_splash:
  color: "#FFFFFF"
  image: assets/images/logo.png
  android_12:
    icon_background_color: "#FFFFFF"
    image: assets/images/logo.png
  ios: true
```

Run:

```bash
dart run flutter_native_splash:create
```

---

## 📦 pubspec.yaml Reference

```yaml
name: studo
description: A Flutter study companion app.
version: 1.0.0+1

environment:
  sdk: ">=3.0.0 <4.0.0"

dependencies:
  flutter:
    sdk: flutter

  # State Management
  flutter_riverpod: ^2.4.9
  riverpod_annotation: ^2.3.3

  # Navigation
  go_router: ^13.2.0

  # Firebase
  firebase_core: ^2.27.0
  firebase_auth: ^4.17.0
  cloud_firestore: ^4.15.0
  firebase_storage: ^11.6.0
  google_sign_in: ^6.2.1

  # Local Storage
  hive: ^2.2.3
  hive_flutter: ^1.1.0
  sqflite: ^2.3.2
  path_provider: ^2.1.2

  # Networking
  dio: ^5.4.1
  connectivity_plus: ^5.0.2

  # UI & Theming
  flutter_svg: ^2.0.9
  lottie: ^3.1.0
  cached_network_image: ^3.3.1
  shimmer: ^3.0.0
  flutter_animate: ^4.5.0

  # Notifications
  flutter_local_notifications: ^17.1.1
  firebase_messaging: ^14.7.20

  # Utils
  intl: ^0.19.0
  uuid: ^4.3.3
  flutter_dotenv: ^5.1.0
  permission_handler: ^11.3.0
  url_launcher: ^6.2.5
  share_plus: ^7.2.2

  # Fonts
  google_fonts: ^6.2.1

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  build_runner: ^2.4.8
  riverpod_generator: ^2.3.9
  hive_generator: ^2.0.1
  flutter_launcher_icons: ^0.13.1
  flutter_native_splash: ^2.3.9
  mockito: ^5.4.4

flutter:
  uses-material-design: true

  assets:
    - assets/images/
    - assets/icons/
    - assets/lottie/
    - assets/screenshots/
    - .env

  fonts:
    - family: Poppins
      fonts:
        - asset: assets/fonts/Poppins-Regular.ttf
          weight: 400
        - asset: assets/fonts/Poppins-Medium.ttf
          weight: 500
        - asset: assets/fonts/Poppins-SemiBold.ttf
          weight: 600
        - asset: assets/fonts/Poppins-Bold.ttf
          weight: 700
```

---

## ⚙️ Environment Configuration

### Android Permissions

In `android/app/src/main/AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<uses-permission android:name="android.permission.VIBRATE"/>
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
<uses-permission android:name="android.permission.USE_EXACT_ALARM"/>
```

### iOS Permissions

In `ios/Runner/Info.plist`:

```xml
<key>NSCameraUsageDescription</key>
<string>Used to scan documents and attach photos to notes.</string>

<key>NSPhotoLibraryUsageDescription</key>
<string>Used to attach images to your notes.</string>

<key>NSUserNotificationsUsageDescription</key>
<string>Used to send study reminders.</string>
```

---

## 📦 Build & Release

### Android

```bash
# Debug APK
flutter build apk --debug

# Release APK
flutter build apk --release

# App Bundle (for Play Store)
flutter build appbundle --release
```

The release AAB is generated at `build/app/outputs/bundle/release/app-release.aab`.

**Signing the release build:**

Create `android/key.properties`:

```
storePassword=<your_store_password>
keyPassword=<your_key_password>
keyAlias=<your_key_alias>
storeFile=<path_to_keystore.jks>
```

Update `android/app/build.gradle`:

```gradle
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
keystoreProperties.load(new FileInputStream(keystorePropertiesFile))

android {
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```

### iOS

```bash
# Debug build
flutter build ios --debug

# Release build
flutter build ios --release
```

Then open Xcode and archive for App Store submission.

---

## 🧪 Testing

```bash
# Run all tests
flutter test

# Run only unit tests
flutter test test/unit/

# Run widget tests
flutter test test/widget/

# Run with coverage report
flutter test --coverage
genhtml coverage/lcov.info -o coverage/html
open coverage/html/index.html

# Integration tests (on device)
flutter test integration_test/
```

### Linting

```bash
# Analyze code
flutter analyze

# Format code
dart format lib/ test/
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/my-new-feature`
3. Commit your changes: `git commit -m 'feat: add some feature'`
4. Push the branch: `git push origin feature/my-new-feature`
5. Open a Pull Request

### Commit Message Convention

Use [Conventional Commits](https://www.conventionalcommits.org/):

| Prefix | Purpose |
|--------|---------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation update |
| `style:` | Code style / formatting |
| `refactor:` | Code refactoring |
| `test:` | Tests |
| `chore:` | Maintenance / tooling |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ using Flutter</p>
