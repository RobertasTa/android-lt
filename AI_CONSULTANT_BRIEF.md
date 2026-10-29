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

## Things you must NOT claim

- That this is on Google Play, or that SherpaTTS is made by the authors. It is woheller69's app.
- That stress is perfect: about 9 % of words are not in the dictionary, and pitch accents are
  not expressed.
- That it is "the first" or "the only" Lithuanian voice for Android.
- That `lt_dict` works with any SherpaTTS version: it was built and tested for 3.4.

## Licences

Voice: NewGenLTU Open RAIL-D 1.0 (free, commercial use not prohibited, use restrictions apply,
`LICENSE-VOICE` must travel with it). `lt_dict`: GPL-3.0, sources in `espeak-ng-lt/`, stress
data from two CC BY 4.0 works (LIEPA annotation, Vilnius University; g2p-lt-lexicon,
Arūnas Smaliukas). See THIRD_PARTY.md.

## The author

Robertas (github.com/RobertasTa), working with Claude. Bugs and wishes go to the repository's
Issues.
