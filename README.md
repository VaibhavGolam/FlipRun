# FLIP // RUN

One-tap gravity runner for Android, by Vaibhav Golam. Tap to flip gravity and run on the floor or the ceiling. Dodge spikes, blocks and gaps, grab coins, and survive through four zones (Neon Night, Aurora, Sunset, Ember). Sound effects and a music loop are generated in code, so there are no audio files. Both can be switched off with the buttons on the menu screen. Best score, coins and everything you buy are saved on the phone.

The runner is a small robot drawn entirely in code, and the launcher icon shows the same robot. The whole game is one file: `app/src/main/assets/index.html`. The Android app is a thin WebView wrapper around it.

## What's in the game

- **Coins and Store.** Coins you pick up are saved in a wallet. The Store (menu or crash screen) sells 6 skins (Robo, Goldie, Ninja, Alien, Ghost, Kitty), 4 trails, and boosts: longer Magnet time (3 levels), Coin x2, and Shields (one is used at the start of each run, hold up to 3). Prices are in `SKINS`, `TRAILS`, `MAGPRICE`, `X2_PRICE` and `SHIELD_PRICE`.
- **In-App tab.** Coin packs, Remove Ads and a Starter Bundle are shown as "coming soon". Nothing real can be bought yet.
- **Magnet.** A magnet pickup shows up now and then and pulls every coin on screen toward you.
- **Size changes.** Every 20 to 30 seconds you turn BIG (bigger hitbox, coins worth 10 points) or MINI (smaller hitbox) for 7 seconds.
- **Speed surge.** Every 25 to 40 seconds the game speeds up about 12 percent and the camera tilts and zooms for about 5 seconds, then settles back.
- **Watch ad to revive.** The button is on the crash screen but no ad network is connected. `Ads.showRewarded()` and `revive()` in `index.html` are the two places to wire it up later.

## Keep-playing features

- **Best marker.** A dashed line in the corridor shows where your best run ended.
- **Daily goals.** Three goals a day (coins, score, close calls, magnets, flips, runs). Each pays coins, and finishing all three pays a bonus. See `MVALS` and `MREW`.
- **Login streak.** A reward pops up on the first launch of each day and grows over 7 days (`STREAK_R`). Missing a day resets it.
- **Daily challenge.** Same obstacle seed for everyone on a given day. The first run is scored and pays 50 coins, later runs are practice.
- **Close calls.** Clear a spike or block by a hair for +10 points.
- **Levels.** XP from score and coins, with coins as the level-up reward and a shield every 5 levels.
- **Share.** The crash screen has a SHARE button that builds a score card image. Where the phone allows it, it opens the share sheet. If not, it copies the score text.
- **New hazards.** Moving saws and falling blocks. Every fifth zone is a rush zone with denser patterns and double coins. Two new zone colors (Toxic, Void).

## Get the APK (no Android Studio needed)

1. Create a new empty repository on GitHub and upload everything in this folder, including the hidden `.github` folder.
2. If `.github/workflows/build-apk.yml` did not upload, create it by hand: **Add file > Create new file**, type `.github/workflows/build-apk.yml` as the name, and paste in the contents of `BUILD_APK_WORKFLOW.yml`.
3. Open the **Actions** tab, pick **Build APK**, and press **Run workflow** (it also runs on every push).
4. After about 3 minutes, open the finished run and download **FlipRun-APK** from Artifacts. Unzip it to get `app-debug.apk`.
5. Send the APK to your phone and install it.

The package id is `com.fliprun.game`. Change it in `app/build.gradle` (and the Java folder) before your first Play upload if you want a different one, because it cannot change afterwards.

## Play it in a browser first

Open `app/src/main/assets/index.html` in Chrome. Space or Up arrow flips gravity.

## Tweaking

- Difficulty and pacing: `START` speed, the speed ramp in `worldStep()`, and the pattern list `PATS` (each pattern has a minimum play time in seconds before it can appear).
- Zone colors: the `ZONES` array. A new zone starts every 250 points.
- Events: `SIZE_DUR`, `BIGS`, `SMALLS`, `SURGE_DUR`, `SURGE_BOOST` and `runEvents()`.
- Sound: the `sfx` object for effects, `playStep()` for the music.
- App name: `android:label` in `AndroidManifest.xml`.
