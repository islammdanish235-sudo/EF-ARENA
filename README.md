# EF ARENA — Flutter + Firebase starter

This is a starter scaffold for an Android eFootball Mobile tournament app.

## Included
- Dark black/gold EF ARENA theme
- Phone number + OTP authentication UI
- Home, tournament list, matches, ranking, profile screens
- Tournament join request
- In-app Admin Panel entry (shown only for configured admin UID)
- Basic tournament creation
- Starter Firestore security rules

## Important setup

1. Install Flutter and Android Studio.
2. Create a Firebase project at https://console.firebase.google.com/
3. Add an Android app to Firebase using your Android application ID.
4. Enable **Authentication → Phone**.
5. Create a Cloud Firestore database.
6. Install FlutterFire CLI and run:
   ```bash
   dart pub global activate flutterfire_cli
   flutterfire configure
   ```
7. Update `main.dart` to initialize Firebase with the generated options:
   ```dart
   import 'firebase_options.dart';
   await Firebase.initializeApp(
     options: DefaultFirebaseOptions.currentPlatform,
   );
   ```
8. Set your admin UID at build time:
   ```bash
   flutter run --dart-define=EF_ARENA_ADMIN_UID=YOUR_FIREBASE_AUTH_UID
   ```
9. Replace `REPLACE_WITH_YOUR_ADMIN_UID` in `firebase/firestore.rules` with the same UID, then publish the rules.
10. Run:
   ```bash
   flutter pub get
   flutter run
   ```

## Production security notes

- Do not rely only on hiding the Admin screen in the app. Firestore rules/server-side authorization are essential.
- For production, use Firebase Auth custom claims set by a trusted server or Cloud Function to identify admins. Never allow a client to grant itself admin privileges.
- Add App Check, rate limits, input validation, duplicate-registration prevention, and audit logs.
- The current join flow is a starter only. It does not verify payments, enforce tournament capacity, or prevent duplicate registrations.
- Paid entry should be integrated only after you define a compliant payment provider and refund/dispute rules. Never store card or mobile-wallet PINs.
- OTP SMS may incur Firebase billing and requires correct Firebase/Play integrity configuration.
- The project has not been built or tested against your Firebase project yet; configuration is required before it can run.

## Suggested next development tasks
1. Player profile form (display name and eFootball User ID)
2. Admin registration approval/rejection
3. Tournament capacity and duplicate-registration checks (server-side)
4. Match fixture generation and result evidence upload
5. Leaderboard aggregation
6. Bengali/English localization using Flutter `gen-l10n`
