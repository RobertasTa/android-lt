# Android LT: a Lithuanian voice and ears for Android phones

![A robotic hand holds a gift box labelled "android-lt" under a glowing globe; next to it: "Android LT, Ingutė on your Android phone" (illustration created with AI)](docs/banner.png)

Ingutė, a Lithuanian synthetic voice, on your Android phone, offline. The phone uses it wherever
it can read aloud: the text-to-speech settings, the screen reader, book and article readers.

Since 1.1.0 there are **ears** too: speak Lithuanian to the phone and the text appears in any text
field, also offline (see [Ears](#ears-lithuanian-dictation-parakeetype)).

*Page: https://robertasta.github.io/android-lt/en/ · Lietuviškai: [README.md](README.md)*

## What is here

- **Ingutė** in sherpa-onnx format (`lt_LT-ingute-medium.onnx`, 63 MB) and a **`tokens.txt`** with
  an "s" fix. eSpeak NG writes Lithuanian /s/ as `ʂ` in many positions, a symbol the voice
  hardly learned, so without the fix many s sounds disappear ("pasiimk skėtį" comes out as
  "paimk kėtį").
- **`lt_dict`**: the Lithuanian eSpeak NG dictionary with the stressed syllable for 189,000 word
  forms. Without it the stress is guessed by rules and is wrong in about half of the
  multi-syllable words.
- **Ears** (`parakeet-lt-kmynas-int8.zip`, 955 MB): a Lithuanian speech recognition model for
  the Parakeetype voice keyboard.

The voice is played by **SherpaTTS**, a free open-source Android TTS engine. It is not part of
this package; install it separately (step 1).

## Installing (about 10 minutes)

1. **Install SherpaTTS from F-Droid.** It is not on Google Play; searching there shows other,
   ad-supported apps.
   File: https://f-droid.org/repo/org.woheller69.ttsengine_34.apk (version 3.4, 91 MB).
   The right app is called **SherpaTTS**, package `org.woheller69.ttsengine`, no ads.
2. **Download to the phone** from the
   [release](https://github.com/RobertasTa/android-lt/releases/latest):
   `lt_LT-ingute-medium.onnx` and `tokens.txt`.
3. **SherpaTTS** → "INSTALL PIPER MODEL FROM SD": language code `lit`, name `Ingute`,
   model `lt_LT-ingute-medium.onnx`, tokens `tokens.txt` → OK.
4. **Phone settings** → "Text-to-speech output" → engine **SherpaTTS**, language
   **Lithuanian** → "Listen to an example".

Ingutė speaks now. Stress is still placed by eSpeak NG; step 5 fixes that.

### 5. Stress (needs a computer)

Recent Android versions (tested on 15) do not let file managers write into another app's
folder, so `lt_dict` goes in through `adb` from a computer
([Google platform-tools](https://developer.android.com/tools/releases/platform-tools)).

1. On the phone: Settings → About phone → tap the build number 7 times (developer mode; the
   phone asks for its unlock code) → in developer options turn on **USB debugging** → connect
   the cable and allow it on the phone.
2. On the computer, in the folder with the downloaded `lt_dict`:

```
adb shell md5sum /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict
```

It must print `5426503daf0a29836d0f168d38b38581` (the dictionary of SherpaTTS 3.4). **If it is
different, stop**: your SherpaTTS version differs and this `lt_dict` was built for 3.4.

```
adb shell cp /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict_orig
adb push lt_dict /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict
adb shell am force-stop org.woheller69.ttsengine
```

Open SherpaTTS and listen to "Dabar labai gera diena, nes Lietuvos rinktinė laimėjo."
You can switch USB debugging off afterwards. To undo, rename `lt_dict_orig` back to `lt_dict`.
Reinstalling SherpaTTS or clearing its data undoes step 5.

## Measurements

A Lithuanian speech recognition model listened to 12 everyday sentences (no numbers):

| | word errors |
|---|---|
| Ingutė in SherpaTTS, no fixes | 7.7 % |
| + "s" fix (`tokens.txt`) | 4.4 % |
| + stress (`lt_dict`) | 1.1 % |

Stressed syllable compared with the stress dictionary on LIEPA texts (19,943 multi-syllable
words): eSpeak NG alone 53.4 %, with this dictionary 99.3 %. Tested on a Xiaomi 12T Pro,
Android 15, SherpaTTS 3.4.

## Limits

- Numbers and abbreviations are read by eSpeak NG itself ("15:25 val." may sound odd).
- Only the stressed syllable is set, not the Lithuanian pitch accent.
- About 9 % of words are not in the dictionary; eSpeak NG guesses those.
- `lt_dict` was built for SherpaTTS 3.4 (sherpa-onnx 1.13); check the md5 first on other versions.
- It is a synthetic voice: natural, but not a person.

## Ears: Lithuanian dictation (Parakeetype)

[Parakeetype](https://github.com/theScrabi/Parakeetype) is an open-source voice keyboard for
Android (F-Droid). It recognises speech on the phone and never goes online. Its default model
hears Lithuanian poorly; `parakeet-lt-kmynas-int8.zip` gives it Lithuanian ears.

| word error rate | FLEURS (986 utterances) | short commands (127) |
|---|---|---|
| Parakeetype's default model (Parakeet Ultra) | 27.1 % | 80.4 % |
| with these ears | 10.6 % | 17.0 % |

Measured on a PC with a script that follows Parakeetype's recognition path exactly; tested live on
Robertas's phone (Xiaomi 12T Pro, Android 15).

**Status (2026-10-29).** For Parakeetype from F-Droid to accept this archive, its author has to
merge our proposal [theScrabi/Parakeetype#1](https://github.com/theScrabi/Parakeetype/pull/1).
Until then you can build the app with the Lithuanian model yourself ("Build it yourself" below).

### Installing

1. **Parakeetype**: from F-Droid once the proposal is merged, or built yourself.
2. **Download to the phone** `parakeet-lt-kmynas-int8.zip` (955 MB) from the
   [release](https://github.com/RobertasTa/android-lt/releases/latest).
3. On Parakeetype's main screen enable the keyboard and allow the microphone. Next to "Model not
   installed" tap "Install", scroll down to the **Parakeet Lithuanian** card → "Import model
   file" → the archive. The app checks every file's hash; you can delete the archive afterwards.
4. On the same card: "Set as Active".
5. **Dictate**: open any text field (notes, for example) and switch the keyboard to Parakeetype.
   In Gboard, long-press the 🌐 globe and pick "Parakeetype Voice Input". Hold the big microphone
   button and speak. The first time, the model takes a few seconds to load.
6. **Back to your usual keyboard**: the small keyboard icon on the right, above the Enter key.

| | | |
|---|---|---|
| ![Parakeet Lithuanian as the active model](docs/parakeetype_model.jpg) | ![Switching keyboards: Parakeetype voice input](docs/parakeetype_switch.jpg) | ![Dictated: "Labas testas yra. Tikrinam, kaip ausys veikia."](docs/parakeetype_dictation.jpg) |

### Build it yourself (until the proposal is merged)

You need a computer with Java 17 or newer and the Android SDK: [Android Studio](https://developer.android.com/studio)
or Google's command-line tools (`android sdk install "platforms;android-37.0" "build-tools;37.0.0"`).
The first build downloads about 1 GB.

```
git clone -b add-lithuanian-model https://github.com/RobertasTa/Parakeetype.git
cd Parakeetype
./gradlew assembleDebug
```

On Windows: `gradlew assembleDebug`. Point to the Android SDK with `sdk.dir=...` in
`local.properties` or the `ANDROID_HOME` variable. Copy the resulting
`app/build/outputs/apk/debug/app-debug.apk` to the phone's Download folder and tap it in a file
manager (Xiaomi phones refuse `adb install` without a Mi account). If you already have
Parakeetype from F-Droid, uninstall it first: apps signed with different keys cannot update each
other. Once the proposal is merged, uninstall your build and install the F-Droid one.

### Limits of the ears

- Lithuanian only. For other languages pick the default model (one model is active at a time).
- About 910 MB on the phone; Parakeetype needs Android 12 or newer.
- On short commands it gets roughly one word in six wrong.

## Licences

- **Voice** (`lt_LT-ingute-medium.onnx`, `tokens.txt`): NewGenLTU Open RAIL-D 1.0. Free of
  charge, commercial use is not prohibited, use restrictions apply; when passing it on, include
  [LICENSE-VOICE](LICENSE-VOICE) and state the origin. Ingutė was grown from the Reginutė model
  with the authors' own Python tools.
- **`lt_dict`** and its sources (`espeak-ng-lt/`): GPL-3.0 (eSpeak NG data). The stress
  positions come from two CC BY 4.0 works; see [THIRD_PARTY.md](THIRD_PARTY.md).
- **Ears** (`parakeet-lt-kmynas-int8.zip`): CC BY 4.0. NVIDIA Parakeet TDT 0.6B v3, fine-tuned for
  Lithuanian by Kristijonas Jakubsonas ("kmynas v4", LIEPA-3). Our changes are listed in the
  archive's `NOTICE.txt`. The Silero VAD inside the archive is MIT. Parakeetype is a separate
  app (GPL-3.0).
- Texts in this repository: GPL-3.0 ([LICENSE](LICENSE)).

## Thanks

[SherpaTTS](https://github.com/woheller69/ttsengine) (woheller69),
[sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) (k2-fsa),
[eSpeak NG](https://github.com/espeak-ng/espeak-ng), [Piper](https://github.com/OHF-Voice/piper1-gpl)
and Michael Hansen; the creators of the **LIEPA** corpus (Vilnius University) and
**Arūnas Smaliukas** for `g2p-lt-lexicon`; [Parakeetype](https://github.com/theScrabi/Parakeetype)
(theScrabi), **Kristijonas Jakubsonas** for the Lithuanian Parakeet ("kmynas") and NVIDIA for
Parakeet.

## Stuck?

Paste into any AI chat: `Read https://raw.githubusercontent.com/RobertasTa/android-lt/main/AI_CONSULTANT_BRIEF.md and help me with Android LT.`
Questions and feedback: [Issues](https://github.com/RobertasTa/android-lt/issues).

---

Made with AI: Claude (Anthropic) prepared and measured the package together with Robertas;
tested on Robertas's phone; the banner was made with AI. Our other gifts: [Skaityklė](https://github.com/RobertasTa/skaitykle)
(text to MP3), [Diktuoklė](https://github.com/RobertasTa/diktuokle) (voice dictation),
[all of them](https://github.com/RobertasTa).
