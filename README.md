# Android LT — lietuviškas balsas ir ausys Android telefonui

![Robotinė ranka laiko dovanų dėžutę su užrašu „android-lt“, virš jos šviečia Žemės rutulys; šalia užrašas „Android LT — Ingutė speaks, your phone listens“ (iliustracija sukurta naudojant DI)](docs/banner.png)

Ingutė, lietuviškas sintetinis balsas, tavo Android telefone. Veikia be interneto. Telefonas ją
naudoja visur, kur moka skaityti garsiai: „Teksto į kalbą“ nustatymuose, ekrano skaitytuve,
knygų ir straipsnių skaityklėse.

Ir **ausys**: kalbi į telefoną lietuviškai, o tekstas atsiranda bet kuriame teksto lauke —
SMS, užrašuose, ChatGPT, Claude ar Gemini programoje. Irgi be interneto (skyrius
[„Ausys“](#ausys-diktavimas-lietuviškai-parakeetype)).

**Nuo 1.2.0 — dvi paruoštos programos:** parsisiunti, įdiegi, ir veikia. Nereikia nei F-Droid,
nei laido, nei kompiuterio → [Kaip įdiegti](#kaip-įdiegti-apie-5-min)

**Jau įdiegei, bet nežinai, ką toliau?** → [Kaip naudotis kasdien](#kaip-naudotis-kasdien)

*Puslapis: https://robertasta.github.io/android-lt/ · In English: [README_EN.md](README_EN.md)*

## Kas čia yra

- **`Ingute-1.0.apk`** (151 MB) — programa „Ingutė“: lietuviškas telefono balsas. Viduje jau yra
  Ingutės balsas, „s“ pataisa ir kirčių žodynas; įdiegta ji pati tampa telefono balsu. Tai
  [SherpaTTS](https://github.com/woheller69/ttsEngine) 3.4 (woheller69) su mūsų lietuviškais priedais
  ([kodas](https://github.com/RobertasTa/ttsEngine/tree/ingute)).
- **`Parakeetype-LT-0.5.0-lt2.apk`** (59 MB) — balso klaviatūra „Parakeetype LT“: lietuviškas diktavimas.
  Tai [Parakeetype](https://github.com/theScrabi/Parakeetype) (theScrabi), kurioje lietuviškas modelis
  yra pirmas ir numatytasis ([kodas](https://github.com/RobertasTa/Parakeetype/tree/lt-build)).
  Interneto leidimo neturi.
- **Ausys** (`parakeet-lt-kmynas-int8.zip`, 955 MB) — lietuviškas kalbos atpažinimo modelis šiai
  klaviatūrai; programa pati parodo, kur jį atsisiųsti.
- Pažengusiems, atskirai: **Ingutės balsas** sherpa-onnx formatu (`lt_LT-ingute-medium.onnx`, 63 MB),
  **`tokens.txt`** su „s“ pataisa (be jos „pasiimk skėtį“ skamba kaip „paimk kėtį“) ir **`lt_dict`** —
  eSpeak NG žodynas su kirčio vieta 189 tūkst. žodžių formų (be jo telefonas suklysta maždaug pusėje
  daugiaskiemenių žodžių: *dãbar, lãbai, Lietùvos* vietoje *dabar̃, labaĩ, Lietuvõs*).

Abi programos pasirašytos mūsų raktu, sertifikato SHA-256
`8679aa5fbfd9f9f96d53ba761e72c9b0f7a361ffdc8493e33bb905e077afaf7f`; failų sumos — `SHA256SUMS.txt` leidime.

## Kaip įdiegti (apie 5 min.)

Reikia Android 10 ar naujesnio (ausims — Android 12). Abu failai — [leidime](https://github.com/RobertasTa/android-lt/releases/latest).

### Balsas — „Ingutė“

1. **Parsisiųsk į telefoną** `Ingute-1.0.apk` ir paspausk jį (naršyklėje arba failų tvarkyklėje,
   aplanke „Download“). Telefonas paklaus, ar leisti diegti programas iš šio šaltinio — **leisk**.
2. **„Įdiegti“.** Atidaryti programos nereikia: Ingutė įsidiegia pati.
3. **Telefono nustatymuose** → „Teksto į kalbą išvestis“ → variklis **Ingutė**, kalba **lietuvių** →
   „Klausyti pavyzdžio“. Ingutė prabyla — jau su kirčiais.

### Ausys — „Parakeetype LT“

1. **Parsisiųsk ir įdiek** `Parakeetype-LT-0.5.0-lt2.apk`. Jei „Google Play Protect“ pasiūlys programą
   patikrinti, spausk **„Patikrinti“**, po to **„Įdiegti“** (mums atsakė: „Atrodo, kad programa saugi“).
2. **Atidaryk** ją, leisk mikrofoną, prie „Modelis neįdiegtas“ spausk **„Įdiegti“**.
3. Kortelėje **„Parakeet Lithuanian (Default)“** — **„Atsisiųsti naršyklėje“** (955 MB, geriau per Wi-Fi).
   Kai atsisiųs — **„Importuoti modelio failą“** → `parakeet-lt-kmynas-int8.zip`. Po minutės kortelė
   rodo **„Aktyvus modelis“**; archyvą galima ištrinti.
4. Pradžios ekrane prie „Klaviatūra neįgalinta“ → **„Atidaryti nustatymus“** → įjunk Parakeetype.
   Android įspės, kad klaviatūra „gali rinkti viską, ką įvedate“: tai rodoma kiekvienai klaviatūrai,
   o ši interneto leidimo neturi, tad tekstas iš telefono niekur neišeina → **OK**.
5. **Diktuok**: bet kuriame teksto lauke Gboard'e ilgai laikyk 🌐 → **„Parakeetype balso įvestis“**,
   laikyk didelį mikrofono mygtuką ir kalbėk.

| | | | |
|---|---|---|---|
| ![Nustatymai: variklis Ingutė, kalba lietuvių](docs/apk_ingute_nustatymai.jpg) | ![Parakeet Lithuanian — pirmas ir numatytasis](docs/apk_modelis.jpg) | ![Po importo: „Aktyvus modelis“](docs/apk_aktyvus.jpg) | ![Padiktuota: „Labas, tai yra lietuviškos ausys Android telefonui“](docs/apk_padiktuota.jpg) |

Programos ekranuose — lietuviškai, sistemos languose — rusiškai (tokia telefono kalba).

<details>
<summary><b>Pažengusiems: balsas per SherpaTTS iš F-Droid</b> (be mūsų programos, apie 10 min.)</summary>

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

</details>

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

## Ausys: diktavimas lietuviškai (Parakeetype)

[Parakeetype](https://github.com/theScrabi/Parakeetype) yra atviro kodo balso klaviatūra
Android telefonui (F-Droid). Kalbą ji atpažįsta pačiame telefone ir prie interneto
nesijungia. Jos numatytasis modelis lietuviškai girdi prastai, o `parakeet-lt-kmynas-int8.zip`
duoda jai lietuviškas ausis.

| žodžių klaidų dalis | FLEURS (986 sakiniai) | trumpos komandos (127) |
|---|---|---|
| Parakeetype numatytasis modelis (Parakeet Ultra) | 27,1 % | 80,4 % |
| su šiomis ausimis | 10,6 % | 17,0 % |

Matuota kompiuteryje, tiksliai atkartojant Parakeetype atpažinimo kelią; Roberto telefone
(Xiaomi 12T Pro, Android 15) išbandyta gyvai.

**Kaip įdiegti** — žr. [„Ausys — Parakeetype LT“](#ausys--parakeetype-lt) aukščiau: mūsų paruošta
programa. Kai Parakeetype autorius sujungs mūsų pasiūlymą
[theScrabi/Parakeetype#1](https://github.com/theScrabi/Parakeetype/pull/1), lietuvišką modelį siūlys
ir F-Droid Parakeetype.

### Pasidaryk pats

Reikia kompiuterio su Java 17 ar naujesne ir Android SDK: [Android Studio](https://developer.android.com/studio)
arba Google command-line tools (`android sdk install "platforms;android-37.0" "build-tools;37.0.0"`).
Pirmas kompiliavimas parsisiunčia apie 1 GB.

```
git clone -b lt-build https://github.com/RobertasTa/Parakeetype.git
cd Parakeetype
./gradlew assembleDebug
```

Windows'e — `gradlew assembleDebug`. Android SDK vietą nurodyk `local.properties` faile
(`sdk.dir=...`) arba `ANDROID_HOME` kintamuoju. Gautą `app/build/outputs/apk/debug/app-debug.apk`
nukopijuok į telefono „Download“ ir paspausk failų tvarkyklėje (Xiaomi be Mi paskyros neleidžia
diegti per `adb install`). Jei jau turi „Parakeetype LT“ iš mūsų leidimo, pirma ją pašalink:
skirtingai pasirašytos programos viena kitos neatnaujina. Balso programos kodas — šaka
[`ingute`](https://github.com/RobertasTa/ttsEngine/tree/ingute), kompiliuojama taip pat.

### Ausų ribos

- Tik lietuvių kalba. Kitoms kalboms rinkis numatytąjį modelį (vienu metu veikia vienas).
- Telefone užima apie 910 MB; Parakeetype reikia Android 12 ar naujesnio.
- Trumpose komandose klysta maždaug kas šeštą žodį.

## Kaip naudotis kasdien

Įdiegti dar nereiškia, kad telefonas pats pradės kalbėti ar klausyti. Čia — ką padaryti vieną
kartą ir kaip paskui naudotis. Meniu pavadinimai skirtinguose telefonuose šiek tiek skiriasi,
todėl paprasčiausia juos rasti **telefono nustatymų paieškoje** (didinamasis stiklas viršuje).
Ekranai — iš Xiaomi telefono rusiška kalba.

### Kad telefonas skaitytų Ingutės balsu

**1. Padaryk Ingutę telefono balsu** (vieną kartą)

Nustatymų paieškoje įrašyk „teksto į kalbą“ (rusiškai „синтез“, angliškai „text-to-speech“).

- **Numatytasis variklis** (rusiškai „Синтезатор речи по умолчанию“) → pasirink **Ingutė**
  (jei diegei pažengusiųjų keliu — **SherpaTTS**). Android parodys perspėjimą, kad variklis „gali
  rinkti tekstą“: jį rodo kiekvienam ne Google balsui. Ingutė tekstą apdoroja pačiame telefone →
  spausk **OK**.
- **Kalba** („Язык“) → **lietuvių**. Jei čia lieka „sistemos kalba“, o telefonas ne lietuviškas,
  mygtukai pilki ir niekas nekalba.
- **Klausyti pavyzdžio** („Воспроизвести“) — turi prabilti Ingutė. Greitį keisk čia pat.

**2. Kad perskaitytų bet kokį tekstą ekrane: SMS, laišką, straipsnį** (vieną kartą)

Nustatymų paieškoje įrašyk „Select to Speak“ (rusiškame telefone „озвуч“ →
„Озвучивание при нажатии“). Tai Google funkcija, ji yra daugumoje telefonų su Google Play.

- Įjunk jungiklį. Android paprašys leidimo matyti ekraną — be jo funkcija negalėtų perskaityti
  teksto → **Leisti** („Разрешить“).
- Ekrano krašte atsiras mažas mėlynas mygtukas. Jei klaus, kaip jį nustatyti, — nieko nekeisk,
  spausk **OK**.

**Kasdien:** atsidaryk tekstą → paspausk mėlyną mygtuką → **paliesk pastraipą**, ir Ingutė ją
perskaitys (arba ▶ — skaitys visą ekraną iš eilės, ■ — sustabdo). Mygtuką galima nutempti pirštu
kitur, jei trukdo.

| | | |
|---|---|---|
| ![Nustatymai „Синтез речи“: variklis SherpaTTS, kalba lietuvių](docs/tts_settings.jpg) | ![„Озвучивание при нажатии“ (Select to Speak) su įjungimo jungikliu](docs/select_to_speak.jpg) | ![Po įjungimo ekrano dešinėje atsiranda mėlynas mygtukas](docs/select_to_speak_button.jpg) |

### Kad telefonas rašytų, ką sakai (ausys)

Kai Parakeetype su lietuvišku modeliu jau įdiegta (skyrius „Ausys“ aukščiau):

1. Atsidaryk vietą, kur rašai: SMS, užrašus, paiešką.
2. **Perjunk klaviatūrą į Parakeetype.** Gboard'e ilgai laikyk 🌐 gaubliuką → „Parakeetype balso
   įvestis“. Kitose klaviatūrose ieškok mažo klaviatūros ženkliuko ekrano apačioje.
3. **Laikyk didelį mikrofono mygtuką ir kalbėk.** Atleidus tekstas atsiranda; taškus, kablelius ir
   didžiąsias raides programa sudeda pati.
4. **Atgal į įprastą klaviatūrą** — mažas klaviatūros ženkliukas dešinėje, virš Enter mygtuko.

### Nesiseka? Nebijok klausti

Pasiklydai ar telefonas rodo ne tai, kas čia parašyta? Atsidaryk bet kurį DI pokalbį (ChatGPT,
Claude, Gemini) ir įklijuok:

`Perskaityk https://raw.githubusercontent.com/RobertasTa/android-lt/main/AI_CONSULTANT_BRIEF.md ir padėk man su Android LT.`

Tada parašyk, kas neišeina, ir pridėk ekrano nuotrauką. Tas DI žino visus šiuos žingsnius ir
dažniausias klaidas, o kalbėsis su tavimi lietuviškai.

## Licencijos

- **Programos** — GPL-3.0, kaip ir jų originalai: „Ingutė“ — SherpaTTS (woheller69) su mūsų
  pakeitimais ([kodas](https://github.com/RobertasTa/ttsEngine/tree/ingute)); „Parakeetype LT“ —
  Parakeetype (theScrabi) su mūsų pakeitimais ([kodas](https://github.com/RobertasTa/Parakeetype/tree/lt-build)).
  Programoje „Ingutė“ esantis balsas ir žodynas — pagal žemiau nurodytas licencijas.
- **Balsas** (`lt_LT-ingute-medium.onnx`, `tokens.txt`) — NewGenLTU Open RAIL-D 1.0:
  naudoti galima laisvai ir nemokamai, komercinio naudojimo nedraudžia, galioja naudojimo
  apribojimai; perduodant toliau kartu perduoti [LICENSE-VOICE](LICENSE-VOICE) ir nurodyti kilmę.
  Ingutė išaugo iš Reginutės modelio, mūsų Python įrankiais.
- **`lt_dict`** ir jo šaltiniai (`espeak-ng-lt/`) — GPL-3.0 (eSpeak NG duomenys). Kirčių vietos
  sudarytos iš dviejų CC BY 4.0 darbų — žr. [THIRD_PARTY.md](THIRD_PARTY.md).
- **Ausys** (`parakeet-lt-kmynas-int8.zip`) — CC BY 4.0: NVIDIA Parakeet TDT 0.6B v3, lietuviškai
  apmokytas Kristijono Jakubsono („kmynas v4“, LIEPA-3). Mūsų pakeitimai surašyti archyvo
  `NOTICE.txt`. Archyve esantis Silero VAD — MIT. Parakeetype — atskira programa (GPL-3.0).
- Šio repozitorijos tekstai — GPL-3.0 ([LICENSE](LICENSE)).

## Ačiū

[SherpaTTS](https://github.com/woheller69/ttsengine) (woheller69), [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)
(k2-fsa), [eSpeak NG](https://github.com/espeak-ng/espeak-ng), [Piper](https://github.com/OHF-Voice/piper1-gpl)
ir Michaelui Hansenui; **LIEPA** garsyno kūrėjams (Vilniaus universitetas) ir **Arūnui Smaliukui**
už `g2p-lt-lexicon`; [Parakeetype](https://github.com/theScrabi/Parakeetype) (theScrabi),
**Kristijonui Jakubsonui** už lietuvišką Parakeet („kmynas“) ir NVIDIA už Parakeet.

## Nesiseka?

Įklijuok į bet kurį DI pokalbį: `Perskaityk https://raw.githubusercontent.com/RobertasTa/android-lt/main/AI_CONSULTANT_BRIEF.md ir padėk man su Android LT.`
Klausimai ir pastebėjimai — [Issues](https://github.com/RobertasTa/android-lt/issues).

---

Sukurta naudojant DI: paketą ruošė ir matavo Claude (Anthropic) kartu su Robertu; išbandyta
Roberto telefone; baneris sukurtas naudojant DI. Kitos mūsų dovanos: [Skaityklė](https://github.com/RobertasTa/skaitykle) (tekstas
į mp3), [Diktuoklė](https://github.com/RobertasTa/diktuokle) (diktavimas balsu) —
[visos](https://github.com/RobertasTa).
