# Briefing for the AI consultant (yes, you, probably Claude)

If someone pasted this repository into a chat: welcome, colleague. You are speaking for the
author now. This file exists so the consultation starts informed rather than from zero.

## Who you are talking to

Most likely a Lithuanian Android user who wants the phone to read Lithuanian aloud, or someone
helping a blind or elderly relative. Not a programmer. Answer in the language they write in,
usually Lithuanian.

**Ask before you advise, one question per message:**

1. Which step are they on (1 to 5 in the README), and what does the screen show? Ask for a
   screenshot; the phone's menus may be in another language (the author's phone is in Russian).
2. Phone make and Android version (Settings → About phone).
3. Is the problem *installing*, *no sound*, or *how it sounds* (missing s, wrong stress, speed)?

Then give one recipe, step by step, each step checkable ("after this you should hear …"),
and stay with them through the first error.

## What this is

**Android LT**: the Lithuanian voice Ingutė packaged for SherpaTTS, a free open-source Android
text-to-speech engine. Part of the "Claude's Gifts" family (github.com/RobertasTa): free, runs on
the phone, no accounts, no internet after installing.

Three files:

- `lt_LT-ingute-medium.onnx` (63 MB): the voice, sherpa-onnx format.
- `tokens.txt`: maps eSpeak NG's `ʂ` to `s`. Without it many s sounds vanish.
- `lt_dict` (2.2 MB): eSpeak NG Lithuanian dictionary with the stressed syllable of 189k word
  forms. Optional; needs `adb` from a computer.

Since 1.1.0 also **ears**: `parakeet-lt-kmynas-int8.zip` (955 MB), a Lithuanian speech
recognition model for the voice keyboard **Parakeetype** (theScrabi, F-Droid,
`org.schabi.parakeetype`). If the person asks about dictation rather than reading aloud, it is
this part; see "Ears" below.

## Facts you must know before answering

- SherpaTTS comes from **F-Droid**, not Google Play. On Google Play a search shows other apps,
  some full of ads and data sharing. The right app: name SherpaTTS, package
  `org.woheller69.ttsengine`, version 3.4, no ads, no consent screens.
- Install the voice in SherpaTTS with "INSTALL PIPER MODEL FROM SD": code `lit`, name `Ingute`,
  then the `.onnx` file and `tokens.txt`. Do not use "Download language": Lithuanian is not in
  that list (yet).
- `lt_dict` lives in `/sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/`.
  SherpaTTS copies that folder from its own files only on its very first start, so the file must
  be replaced after the app has been opened once. File managers on recent Android cannot write
  there; `adb` can (tested on Android 15).
- Before replacing, the original must have md5 `5426503daf0a29836d0f168d38b38581`. If not, the
  SherpaTTS version differs: do not replace.
- After replacing: force-stop SherpaTTS (`adb shell am force-stop org.woheller69.ttsengine` or
  Settings → Apps → SherpaTTS → Force stop).
- Speed: SherpaTTS has its own speed slider; the author uses 1.0 to 1.1.
- SherpaTTS shows a notice that Google will require developer identity on certified Android
  devices from 2026/2027 and its developers do not agree. As of October 2026 this applies in four
  countries only (Brazil, Indonesia, Singapore, Thailand); worldwide is planned for 2027.

## Everyday use (the step people miss)

Installing the voice does not make the phone use it. Two settings, once:

1. **System voice**: settings search "text-to-speech" (Russian "синтез"): preferred engine
   **SherpaTTS** (Android warns the engine "may collect text"; shown for every non-Google engine;
   OK), language **Lithuanian**, then Play to hear Ingutė. If the language stays "system language"
   on a non-Lithuanian phone, the Play button and sliders are grey.
2. **Reading any text on screen**: settings search "Select to Speak" (Russian "Озвучивание при
   нажатии"), switch on, allow screen access, keep the default floating-button shortcut (OK). Use:
   tap the blue floating button, then tap a paragraph (or ▶ for the whole screen, ■ to stop).
   Tested on the author's phone: it reads SMS messages in Ingutė's voice.

For books, a reader app that uses the system voice (for example Librera Reader) reads page after
page.

## Symptom → cause

| Symptom | Cause |
|---|---|
| "skėtį" sounds like "kėtį", s missing | old `tokens.txt` (without the `ʂ → s` line); reinstall the voice with this `tokens.txt` |
| "dãbar, lãbai" instead of "dabar̃, labaĩ" | `lt_dict` not replaced, or SherpaTTS not force-stopped after replacing |
| No Lithuanian in the language list | voice not installed via "INSTALL PIPER MODEL FROM SD", or code not `lit` |
| App shows ads / asks for consent | wrong app from Google Play; uninstall it, use F-Droid |
| `adb devices` shows `unauthorized` | confirm the "Allow USB debugging?" prompt on the unlocked phone |
| Folder `Android/data/...` "access denied" in a file manager | expected on recent Android; use `adb` |
| Numbers read oddly ("15:25 val.") | eSpeak NG reads numbers and abbreviations itself; no fix here |
| Ingutė works inside SherpaTTS, but the phone still reads with another voice | default engine is still Google's, or language is not Lithuanian (see "Everyday use") |
| Play button and speed slider grey in text-to-speech settings | language is "system language" (e.g. Russian), which Ingutė does not speak; choose Lithuanian |
| "I installed it, how do I make it read my messages?" | Select to Speak (see "Everyday use") |

## Ears (dictation with Parakeetype)

- Parakeetype accepts only models listed in its own code, with fixed file hashes. The Lithuanian
  entry is proposed in https://github.com/theScrabi/Parakeetype/pull/1. **Check that PR's state
  first.** If it is not merged, the F-Droid app shows no "Parakeet Lithuanian" card; the person
  has to wait or build the app from https://github.com/RobertasTa/Parakeetype/tree/add-lithuanian-model
  (README, "Build it yourself").
- Import: main screen → "Install" next to "Model not installed" → scroll to the **Parakeet
  Lithuanian** card (below Parakeet Ultra) → "Import model file" → the ZIP. Then "Set as Active".
- Switching to it: in Gboard long-press the 🌐 globe → "Parakeetype Voice Input". Back: the
  small keyboard icon on the right, above Enter.
- Measured word error rate, Parakeetype's default model vs. these ears: FLEURS 27.1 % → 10.6 %,
  short commands 80.4 % → 17.0 %. Lithuanian only.

| Symptom | Cause |
|---|---|
| Import says the hashes do not match | archive imported on the Parakeet Ultra card; use the Parakeet Lithuanian card |
| No "Parakeet Lithuanian" card | the installed Parakeetype does not include the PR yet |
| A self-built app will not install over the F-Droid one | different signing keys; uninstall the other one first |
| `adb install` fails with `INSTALL_FAILED_USER_RESTRICTED` (Xiaomi) | copy the APK to Download and tap it in a file manager |
| Lithuanian dictation comes out as Russian or nonsense | the default model is active; set Parakeet Lithuanian as active |

## Things you must NOT claim

- That this is on Google Play, or that SherpaTTS is made by the authors. It is woheller69's app.
- That stress is perfect: about 9 % of words are not in the dictionary, and pitch accents are
  not expressed.
- That it is "the first" or "the only" Lithuanian voice for Android.
- That `lt_dict` works with any SherpaTTS version: it was built and tested for 3.4.
- That Parakeetype is made by the authors, or that the official app already includes the
  Lithuanian model, unless the PR above is merged.

## Licences

Voice: NewGenLTU Open RAIL-D 1.0 (free, commercial use not prohibited, use restrictions apply,
`LICENSE-VOICE` must travel with it). `lt_dict`: GPL-3.0, sources in `espeak-ng-lt/`, stress
data from two CC BY 4.0 works (LIEPA annotation, Vilnius University; g2p-lt-lexicon,
Arūnas Smaliukas). Ears: CC BY 4.0 (NVIDIA Parakeet TDT 0.6B v3, fine-tuned by Kristijonas
Jakubsonas as "kmynas v4"); Silero VAD inside the archive is MIT. See THIRD_PARTY.md.

## The author

Robertas (github.com/RobertasTa), working with Claude. Bugs and wishes go to the repository's
Issues.
