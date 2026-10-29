# Android LT — lietuviškas balsas Android telefonui

Ingutė, lietuviškas sintetinis balsas, tavo Android telefone. Veikia be interneto. Telefonas ją
naudoja visur, kur moka skaityti garsiai: „Teksto į kalbą“ nustatymuose, ekrano skaitytuve,
knygų ir straipsnių skaityklėse.

*In English: [README_EN.md](README_EN.md)*

## Kas čia yra

- **Ingutės balsas** sherpa-onnx formatu (`lt_LT-ingute-medium.onnx`, 63 MB) ir **`tokens.txt`**
  su „s“ pataisa: be jos telefone dingsta daug „s“ garsų („pasiimk skėtį“ skamba kaip „paimk kėtį“).
- **`lt_dict`** — lietuvių eSpeak NG žodynas su kirčio vieta 189 tūkst. žodžių formų. Be jo
  telefonas kirtį spėja ir maždaug pusėje daugiaskiemenių žodžių suklysta: *dãbar, lãbai, Lietùvos*
  vietoje *dabar̃, labaĩ, Lietuvõs*.

Balsą groja nemokama atviro kodo programa **SherpaTTS**. Jos šis paketas neturi — ją reikia
įsidiegti atskirai (žr. 1 žingsnį).

## Kaip įdiegti (apie 10 min.)

1. **Įsidiek SherpaTTS iš F-Droid** — Google Play'uje jos **nėra** (paieška ten rodo kitas,
   reklamines programas).
   Failas: https://f-droid.org/repo/org.woheller69.ttsengine_34.apk (versija 3.4, 91 MB).
   Tikroji programa vadinasi **SherpaTTS**, paketas `org.woheller69.ttsengine`, jokių reklamų.
2. **Parsisiųsk į telefoną** iš [Release](https://github.com/RobertasTa/android-lt/releases/latest)
   du failus: `lt_LT-ingute-medium.onnx` ir `tokens.txt`.
3. **SherpaTTS** → „INSTALL PIPER MODEL FROM SD“:
   kalbos kodas `lit`, pavadinimas `Ingute`, modelis — `lt_LT-ingute-medium.onnx`,
   tokens — `tokens.txt` → OK.
4. **Telefono nustatymuose** → „Teksto į kalbą išvestis“ → variklis **SherpaTTS**, kalba
   **lietuvių** → „Klausyti pavyzdžio“.

Čia Ingutė jau kalba. Kirčius kol kas dėlioja eSpeak NG — 5 žingsnis juos sutvarko.

| | |
|---|---|
| ![Įkėlimo langelis](docs/sherpatts_install.jpg) | ![Pagrindinis langas](docs/sherpatts_main.jpg) |

### 5. Kirčiai (per kompiuterį)

Naujesni Android'ai (išbandyta su 15) neleidžia failų tvarkyklei rašyti į kitų programų aplankus,
todėl `lt_dict` dedamas per kompiuterį su `adb`
([Google platform-tools](https://developer.android.com/tools/releases/platform-tools)).

1. Telefone: Nustatymai → Apie telefoną → 7 kartus paspausk „Versijos numerį“ (Xiaomi — „OS
   versija“; paklaus telefono atrakinimo kodo) → kūrėjo režimas →
   kūrėjo nustatymuose įjunk **„USB derinimas“** → prijunk laidu ir patvirtink leidimą telefone.
2. Kompiuteryje (aplanke, kur yra parsisiųstas `lt_dict` ir `adb`):

```
adb shell md5sum /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict
```

Turi būti `5426503daf0a29836d0f168d38b38581` (originalus SherpaTTS 3.4 žodynas). **Jei kitoks —
nekeisk**: tavo SherpaTTS versija kita, o šis `lt_dict` sudarytas jos 3.4 versijai.

```
adb shell cp /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict_orig
adb push lt_dict /sdcard/Android/data/org.woheller69.ttsengine/files/espeak-ng-data/lt_dict
adb shell am force-stop org.woheller69.ttsengine
```

Atidaryk SherpaTTS ir paklausyk: „Dabar labai gera diena, nes Lietuvos rinktinė laimėjo.“
Po to USB derinimą gali išjungti. Grąžinti: tą patį aplanką, `lt_dict_orig` → `lt_dict`.
Iš naujo įdiegus SherpaTTS ar išvalius jos duomenis, 5 žingsnį reikia kartoti.

## Ką rodo matavimai

Lietuviškas kalbos atpažinimo modelis klausė 12 kasdienių sakinių (be skaičių):

| | žodžių klaidų |
|---|---|
| Ingutė per SherpaTTS be pataisų | 7,7 % |
| + „s“ pataisa (`tokens.txt`) | 4,4 % |
| + kirčiai (`lt_dict`) | 1,1 % |

Kirčio vieta, palyginus su kirčių žodynu (LIEPA tekstai, 19 943 daugiaskiemeniai žodžiai):
eSpeak NG be šio žodyno — 53,4 %, su juo — 99,3 %. Išbandyta Xiaomi 12T Pro, Android 15,
SherpaTTS 3.4.

## Ribos

- Skaičius ir santrumpas skaito eSpeak NG pats („15:25 val.“ gali skambėti keistai).
- Perduodama tik kirčio vieta, ne priegaidė (tvirtapradė / tvirtagalė).
- Apie 9 % žodžių žodyne nėra — jiems kirtį spėja eSpeak NG.
- `lt_dict` sudarytas SherpaTTS 3.4 (sherpa-onnx 1.13) — kitai versijai pirmiau patikrink md5.
- Tai sintetinis balsas: natūralus, bet ne žmogus.

## Licencijos

- **Balsas** (`lt_LT-ingute-medium.onnx`, `tokens.txt`) — NewGenLTU Open RAIL-D 1.0:
  naudoti galima laisvai ir nemokamai, komercinio naudojimo nedraudžia, galioja naudojimo
  apribojimai; perduodant toliau kartu perduoti [LICENSE-VOICE](LICENSE-VOICE) ir nurodyti kilmę.
  Ingutė išaugo iš Reginutės modelio, mūsų Python įrankiais.
- **`lt_dict`** ir jo šaltiniai (`espeak-ng-lt/`) — GPL-3.0 (eSpeak NG duomenys). Kirčių vietos
  sudarytos iš dviejų CC BY 4.0 darbų — žr. [THIRD_PARTY.md](THIRD_PARTY.md).
- Šio repozitorijos tekstai — GPL-3.0 ([LICENSE](LICENSE)).

## Ačiū

[SherpaTTS](https://github.com/woheller69/ttsengine) (woheller69), [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)
(k2-fsa), [eSpeak NG](https://github.com/espeak-ng/espeak-ng), [Piper](https://github.com/OHF-Voice/piper1-gpl)
ir Michaelui Hansenui; **LIEPA** garsyno kūrėjams (Vilniaus universitetas) ir **Arūnui Smaliukui**
už `g2p-lt-lexicon`.

## Nesiseka?

Įklijuok į bet kurį DI pokalbį: `Perskaityk https://raw.githubusercontent.com/RobertasTa/android-lt/main/AI_CONSULTANT_BRIEF.md ir padėk man su Android LT.`
Klausimai ir pastebėjimai — [Issues](https://github.com/RobertasTa/android-lt/issues).

---

Sukurta naudojant DI: paketą ruošė ir matavo Claude (Anthropic) kartu su Robertu; išbandyta
Roberto telefone. Kitos mūsų dovanos: [Skaityklė](https://github.com/RobertasTa/skaitykle) (tekstas
į mp3), [Diktuoklė](https://github.com/RobertasTa/diktuokle) (diktavimas balsu) —
[visos](https://github.com/RobertasTa).
