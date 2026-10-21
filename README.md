# Íslenskar raddir fyrir Autodarts (darts-caller)

Íslenskir „callerar“ fyrir [Autodarts](https://autodarts.io) svo að skor, útskot og leikjatilkynningar séu lesnar upp á íslensku. Raddirnar virka með [darts-caller](https://github.com/lbormann/darts-caller), sem er oftast keyrt í gegnum [darts-hub](https://github.com/lbormann/darts-hub).

| Mappa | Rödd |
|---|---|
| `is-IS-Gudrun-Female-v1` | Guðrún (kvenrödd) |
| `is-IS-Gunnar-Male-v1` | Gunnar (karlrödd) |

Hvor rödd er með 364 hljóðskrár (mp3): öll skor frá 0 til 180, einfalda, tvöfalda og þrefalda reiti, bull/bullseye, „game on“, „game shot“, „match shot“, „busted“, leggi og sett (1–50), auk hljóða fyrir æfingaleiki (Around the Clock, Round the World, Bermuda og Gotcha) og blindrastuðning.

---

## Það sem þarf

- Autodarts-borð og aðgang að [play.autodarts.io](https://play.autodarts.io)
- Tölvu sem keyrir **darts-hub** (Windows, Linux, t.d. Raspberry Pi, eða Mac). Þetta má vera sama tölvan og keyrir Autodarts.

Leiðbeiningarnar eru í tveimur hlutum: [Windows](#uppsetning-á-windows) og [Linux / Raspberry Pi](#uppsetning-á-linux--raspberry-pi).
- Hátalara eða heyrnartól við þá tölvu, eða síma/spjaldtölvu ef notaður er vef-callerinn (sjá neðar)

---

## Uppsetning á Windows

### 1. Settu upp darts-hub (ef þú ert ekki með það)

1. Sæktu nýjustu útgáfuna fyrir þitt stýrikerfi á <https://github.com/lbormann/darts-hub/releases/latest>
   (t.d. `darts-hub-windows-X64.zip` fyrir Windows).
2. Búðu til möppuna `darts-hub` í heimamöppunni þinni (t.d. `C:\Users\<notandi>\darts-hub`) og afþjappaðu zip-skrána þangað.
3. Tvísmelltu á `darts-hub` til að ræsa forritið.
4. Settu upp **darts-caller** inni í darts-hub og fylltu inn Autodarts-netfang, lykilorð og Board ID.

### 2. Sæktu íslensku raddirnar

**Auðveldast:** Smelltu á græna **Code**-takkann efst á þessari síðu og veldu **Download ZIP**. Afþjappaðu skrána.

**Eða með git:**

```bash
git clone https://github.com/bippi/dart-caller-isk.git
```

### 3. Settu raddirnar í „media“-möppu

darts-caller leitar að röddum í einni möppu (kölluð *media path*). Hver undirmappa þar er ein rödd.

1. Búðu til möppu, til dæmis `C:\darts-voices`
   - **Ekki** setja hana inni í darts-caller- eða darts-hub-möppunni, því hún getur yfirskrifast við uppfærslu.
2. Afritaðu möppurnar `is-IS-Gudrun-Female-v1` og `is-IS-Gunnar-Male-v1` inn í hana.

Útkoman á að líta svona út:

```
C:\darts-voices\
├── is-IS-Gudrun-Female-v1\
│   ├── 0.mp3
│   ├── 1.mp3
│   ├── ...
│   └── you_require.mp3
└── is-IS-Gunnar-Male-v1\
    ├── 0.mp3
    └── ...
```

> Mikilvægt: mp3-skrárnar eiga að vera **beint** inni í raddmöppunni, ekki í aukamöppu inni í henni (algengt eftir afþjöppun á zip-skrá).

Ef þú ert þegar með media-möppu fyrir darts-caller (t.d. með niðurhöluðum enskum röddum) geturðu einfaldlega bætt íslensku möppunum þar við.

### 4. Stilltu darts-caller

Opnaðu stillingar darts-caller í darts-hub og stilltu:

| Stilling | Gildi | Skýring |
|---|---|---|
| `-M` / `--media_path` | `C:\darts-voices` | Slóðin á möppuna úr skrefi 3 (heil slóð) |
| `-C` / `--caller` | `is-IS-Gudrun-Female-v1` eða `is-IS-Gunnar-Male-v1` | Hvaða rödd á að nota |
| `-R` / `--random_caller` | `0` | Slökkt á handahófskenndu vali raddar, svo valin rödd sé alltaf notuð |
| `-E` / `--call_every_dart` | `2` (valfrjálst) | Les upp hverja pílu fyrir sig (t.d. „þrefalt tuttugu“) |
| `-PCC` / `--possible_checkout_call` | `1` (valfrjálst) | Tilkynnir hvað leikmaður á eftir („you require“) |
| `-CBS` / `--call_blind_support` | `1` (valfrjálst) | Blindrastuðningur |

Ef þú notar enskar raddir líka og vilt að íslensku raddirnar séu valdar af handahófi, slepptu `-C` og settu `-R` á `1` (ný rödd í hverjum leik) eða `2` (ný rödd í hverjum legg).

### 5. Endurræstu og prófaðu

Endurræstu darts-caller í darts-hub. Við ræsingu birtir hann lista yfir uppsettar raddir og þar eiga íslensku raddirnar að sjást. Byrjaðu leik á Autodarts og hentu einni pílu.

---

## Uppsetning á Linux / Raspberry Pi

Þetta á við Ubuntu, Debian, Raspberry Pi OS og sambærilegar dreifingar. darts-hub styður x64, ARM og ARM64, svo það keyrir líka á Raspberry Pi.

### 1. Settu upp darts-hub (ef þú ert ekki með það)

**Auðveldast:** Keyrðu uppsetningarskriftu darts-hub. Hún sækir nýjustu útgáfuna og stillir hana til að ræsast sjálfkrafa:

```bash
sudo apt install curl
bash <(curl -sL get-add.arnes-design.de)
```

**Eða handvirkt:**

1. Sæktu zip-skrána fyrir þinn örgjörva á <https://github.com/lbormann/darts-hub/releases/latest> (ARM64 fyrir Raspberry Pi 4/5 með 64-bita stýrikerfi).
2. Afþjappaðu hana í `~/darts-hub` og gerðu skrána keyranlega:

   ```bash
   mkdir -p ~/darts-hub
   unzip darts-hub-*.zip -d ~/darts-hub
   chmod +x ~/darts-hub/darts-hub
   ~/darts-hub/darts-hub
   ```

Settu svo upp **darts-caller** inni í darts-hub og fylltu inn Autodarts-netfang, lykilorð og Board ID.

### 2. Sæktu raddirnar og settu þær í media-möppu

Með git:

```bash
sudo apt install git
git clone https://github.com/bippi/dart-caller-isk.git ~/dart-caller-isk
mkdir -p ~/darts-voices
cp -r ~/dart-caller-isk/is-IS-* ~/darts-voices/
```

Eða án git:

```bash
sudo apt install wget unzip
cd ~
wget https://github.com/bippi/dart-caller-isk/archive/refs/heads/main.zip -O dart-caller-isk.zip
unzip dart-caller-isk.zip
mkdir -p ~/darts-voices
cp -r ~/dart-caller-isk-main/is-IS-* ~/darts-voices/
```

Athugaðu að allt sé á sínum stað:

```bash
ls ~/darts-voices
# is-IS-Gudrun-Female-v1  is-IS-Gunnar-Male-v1
ls ~/darts-voices/is-IS-Gudrun-Female-v1 | wc -l
# 364
```

### 3. Stilltu darts-caller

Stillingarnar eru þær sömu og á Windows (sjá [töfluna að ofan](#4-stilltu-darts-caller)). Munurinn er slóðin í `-M`:

| Stilling | Gildi |
|---|---|
| `-M` / `--media_path` | `/home/<notandi>/darts-voices` |
| `-C` / `--caller` | `is-IS-Gudrun-Female-v1` eða `is-IS-Gunnar-Male-v1` |

Notaðu **heila slóð**, ekki `~/darts-voices`, því `~` er ekki alltaf túlkað rétt. Rétta slóð færðu með:

```bash
echo ~/darts-voices
```

### 4. Hljóð

Ef ekkert heyrist á Linux er algengast að hljóðið fari á rangt úttak.

- Prófaðu hátalarana: `speaker-test -t wav -c 2` (Ctrl+C til að stöðva)
- Stilltu hljóðstyrk og úttak: `alsamixer`, eða hljóðstillingar skjáborðsins
- **Raspberry Pi:** Veldu úttak (HDMI, heyrnartólstengi eða USB/Bluetooth) með `sudo raspi-config` → *System Options* → *Audio*, eða með því að hægrismella á hátalaratáknið efst í horninu.
- Ef Pi-inn er skjálaus (headless) og ekki tengdur við hátalara er gott að nota [vef-callerinn](#vef-caller-sími--spjaldtölva) í síma eða spjaldtölvu í staðinn.

### 5. Uppfæra raddirnar síðar

Ef þú notaðir git:

```bash
cd ~/dart-caller-isk && git pull
cp -r ~/dart-caller-isk/is-IS-* ~/darts-voices/
```

Endurræstu svo darts-caller.

> Á Linux skipta há- og lágstafir máli í skráarheitum. Skrá með nafni leikmanns verður að heita nákvæmlega eins og notandanafnið á Autodarts, með lágstöfum, t.d. `jon.mp3`, ekki `Jon.mp3`.

---

## Vef-caller (sími / spjaldtölva)

darts-caller er líka með vef-caller sem spilar hljóðin í vafra, t.d. í síma sem tengdur er við Bluetooth-hátalara. Í vef-callernum má líka skipta milli radda á meðan leikið er. Sjá leiðbeiningar í [darts-caller](https://github.com/lbormann/darts-caller).

---

## Þitt eigið nafn

darts-caller getur lesið upp nafn leikmanns þegar röðin kemur að honum og þegar leikur byrjar. Til þess þarf hljóðskrá sem heitir nákvæmlega eins og notandanafnið á Autodarts, með lágstöfum, t.d. `bippi.mp3` (sem fylgir með sem dæmi).

Til að bæta við eigin nafni:

1. Taktu upp eða búðu til mp3- eða wav-skrá þar sem nafnið er sagt.
2. Gefðu henni nafn eftir Autodarts-notandanafninu þínu, t.d. `jon.mp3`.
3. Settu hana í raddmöppuna (eða báðar).

---

## Afbrigði hljóða (`+2`, `+3`)

Sumar skrár eru til í fleiri en einni útgáfu, t.d. `gameon.mp3`, `gameon+2.mp3` og `gameon+3.mp3`. darts-caller velur þá eina þeirra af handahófi svo að upplesturinn verði ekki einhæfur. Þú getur bætt við eigin afbrigðum á sama hátt: `nafn+eitthvað.mp3`.

---

## Vandamál og lausnir

**Röddin birtist ekki í listanum**
- Athugaðu að `-M` vísi á móðurmöppuna (`C:\darts-voices`), ekki á raddmöppuna sjálfa.
- Athugaðu að mp3-skrárnar séu beint inni í raddmöppunni, ekki í aukamöppu.

**Ekkert hljóð**
- Athugaðu hljóðstyrk og að réttur hátalari sé valinn sem sjálfgefinn í stýrikerfinu.
- Prófaðu að stilla `-V` / `--caller_volume` (t.d. `1.0`).

**Sum skor eru lesin upp á ensku eða alls ekki**
- Þá vantar líklega skrá fyrir það hljóð í raddmöppunni. Hægt er að bæta henni við. Heiti skráa eru talin upp í [darts-caller](https://github.com/lbormann/darts-caller) undir *sound-file-keys*.

---

## Hvað er í pökkunum

| Flokkur | Skrár |
|---|---|
| Skor | `0.mp3` – `180.mp3`, `left`, `average` |
| Leikur | `hi`, `gameon`, `matchon`, `gameshot`, `matchshot`, `matchcancel`, `busted`, `first_to_throw`, `bulling_start`, `bulling_end` |
| Leggir og sett | `leg_1` – `leg_50`, `set_1` – `set_50` |
| Einstakar pílur | `bull`, `bullseye`, `double`, `triple`, `outside`, `d1` – `d20`, `t1` – `t20` |
| Útskot | `you_require` |
| Around the Clock | `atc_target_hit`, `atc_target_missed`, `atc_target_next` |
| Round the World | `rtw_target_hit_single`, `rtw_target_hit_double`, `rtw_target_hit_triple`, `rtw_target_missed` |
| Bermuda / Gotcha | `ber_minus`, `got_score_denied` |
| Blindrastuðningur | `bs_target_is`, `bs_any_double`, `bs_any_triple`, `bs_outside`, `bs_single_inner` |

---

## Um raddirnar og notkunarskilmála

Raddirnar eru **búnar til með gervigreind** í Microsoft Azure AI Speech (raddirnar `is-IS-GudrunNeural` og `is-IS-GunnarNeural`). Þetta eru ekki upptökur af raunverulegu fólki.

Skrárnar voru búnar til með greiddri Azure-áskrift (Standard S0), sem veitir rétt til að nota og dreifa hljóðinu. Þér er frjálst að nota þær með Autodarts og darts-caller. Ekki má nota þær til að þjálfa eða bæta aðra talgervla.

---

## Ábendingar og viðbætur

Fannstu villu í framburði, vantar hljóð, eða viltu bæta við rödd? Opnaðu [Issue](https://github.com/bippi/dart-caller-isk/issues) eða sendu Pull Request.

Góða skemmtun og góð skot! 🎯
