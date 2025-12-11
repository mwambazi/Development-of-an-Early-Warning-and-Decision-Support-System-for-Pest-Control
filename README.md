# FAMEWS Android Scouting App (Offline-first)

This is an Android app skeleton for a FAMEWS-style Fall Armyworm scouting client.

## Features

- Kotlin + AndroidX
- Scouting form UI (crop stage, larvae count, damage level, plants sampled, notes)
- Offline queue of observations using Room
- Retrofit + OkHttp with bearer token auth
- Repository with `queueObservation()` and `syncPending()`

## How to use

1. Open this folder (`android_app`) in **Android Studio** as a project.
2. Set your backend URL in `ScoutingActivity.createObservationRepository()`:
   ```kotlin
   baseUrl = "https://your-api.example.com/"
   ```
3. Ensure your backend exposes:
   - `POST /auth/login` returning `{ "access_token": "...", "token_type": "bearer" }`
   - `POST /observations` accepting the `ObservationCreateDto` JSON
4. Replace the placeholder FAW pest UUID in `ScoutingViewModel` with the real one from your backend.

For offline sync, call `ObservationRepository.syncPending()` from a background worker (e.g. WorkManager)
when network becomes available.
