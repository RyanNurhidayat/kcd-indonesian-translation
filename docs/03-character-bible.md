# Character Bible — Voice & Karakterisasi NPC

Dokumen ini mendokumentasikan **gaya bicara, kepribadian, dan kosakata khas** tiap karakter. Penerjemah dialog **WAJIB** konsultasi dokumen ini.

**Total karakter teridentifikasi:** 50+ (dari analisis dialog ID encoding)

---

## Cara Identifikasi Speaker dari Dialog ID

KCD encode speaker di dialog ID:

```
Format: t[number]_s[number]_[number]_[speaker_code]_[hash]

Contoh:
t10001_s15335_0_ludmila_al_g9cK  → Ludmila berbicara
t10010_s15351_2_p_strazny__yaSL  → Strážný (Pengawal) berbicara
t10037_s15395_0_divis_z_ta_HHOB  → Sir Divish (z Talmberka) berbicara
t10043_s15402_0_jan_zajic__pr0m  → Jan Zajíc (Hanekin Hare) berbicara
t9919_s15191_1_henry_0_GpPE       → Henry berbicara
t9919_s15191_1_ui                 → Pilihan dialog player (UI choice)
```

**Speaker codes umum:**

| Code | Karakter | Catatan |
|------|----------|---------|
| `henry` | Henry | Protagonis (PC) |
| `_ui` | Player choice | Pilihan dialog (POV Henry) |
| `divis_z_ta` | Sir Divish | "z Talmberka" = "dari Talmberg" (Ceko) |
| `radzig` | Sir Radzig | |
| `jan_zajic` | Jan Zajíc / Hanekin Hare | Nama Ceko vs Inggris |
| `johan` / `johanka` | Johanka | Visioner Sasau |
| `theresa` | Theresa | Love interest |
| `hans` / `capon` | Sir Hans Capon | |
| `hanush` | Sir Hanush | |
| `bernard` | Captain Bernard | Pelatih combat |
| `godwin` | Pater Godwin | Pendeta Uzhitz |
| `nicodemus` | Brother Nicodemus | Biarawan Sasau |
| `peshek` | Miller Peshek | Paman Theresa |
| `mira` | Mira | Bath maid Rattay |
| `kunesh` | Kunesh | Tukang ribut Skalitz |
| `fritz` | Fritz | Teman Henry |
| `matthew` / `matus` | Matthew (Czech: Matúš) | Teman Henry |
| `strazny` | Strážný | Pengawal generik (Ceko) |
| `vojak` | Voják | Prajurit generik (Ceko) |
| `velitel` | Velitel | Komandan (Ceko) |
| `hejtman_ta` | Hetman of Talmberg | |

**Prefix `p_`** sering berarti "perspective" atau dialog reactive (saat NPC bereaksi melihat sesuatu).

---

## Karakter Utama (Detail)

### Henry of Skalitz (PROTAGONIS)

**ID code:** `henry`, `_ui` (untuk pilihan dialog)

**Peran:** Protagonis (Player Character)  
**Status sosial:** Anak pandai besi (rakyat jelata) → diangkat menjadi pengawal Sir Radzig  
**Asal:** Skalitz  
**Usia:** 20-an awal

**Kepribadian:**
- Naif di awal, dewasa seiring cerita
- Loyal, jujur, kadang impulsif
- Rasa keadilan kuat
- Humor membumi
- Berkembang dari "blacksmith's son" jadi "knight in training"

**Gaya bicara — ADAPTIF (sangat penting!):**

| Lawan Bicara | Tone & Pronomina |
|--------------|------------------|
| Teman sebaya (Fritz, Matthew, Theresa) | "aku/kau" — kasual akrab |
| Theresa (romantis) | "aku/kau" — lembut, hangat |
| Rakyat jelata | "aku" — membumi |
| Pater Godwin (informal) | "aku" — sopan |
| Pater Godwin (saat pengakuan dosa) | "saya" — formal religius |
| Pedagang | "aku" / "saya" — sopan |
| Sir Radzig | "saya/hamba" — formal, hormat (figure ayah) |
| Sir Hans Capon | "saya/aku" — campuran (mereka kemudian jadi teman) |
| Lord Divish, Lord Hanush | "hamba" — sangat hormat |
| Musuh / penjahat | "kau" / "kalian" — kasar/tegas |

**Kosakata khas:**
- "Tuhan tahu..." / "Demi Tuhan"
- "Yah..." (filler)
- Sering refer ke Skalitz, ayahnya Martin
- "Begini..." (memulai penjelasan)

**Catatan voice acting:** Henry sengaja "biasa" — tidak terlalu sastra, tidak terlalu kasar. Refleksikan dalam Indonesia.

**Contoh dialog asli:**
> "Look, I really have to get out of here. I have to bury my parents and I'd reward anyone who'd help me."

**Terjemahan baku:**
> "Begini, aku benar-benar harus keluar dari sini. Aku harus menguburkan orang tuaku, dan akan kuberi imbalan pada siapa pun yang membantuku."

---

### Sir Radzig Kobyla

**ID code:** `radzig`

**Peran:** Mentor, ksatria senior  
**Status:** Bangsawan, Lord of Skalitz (kemudian Pirkstein, Rattay)  
**Asal:** Bohemia  
**Usia:** 50-an  

**Kepribadian:**
- Bijaksana, terhormat, fatherly figure
- Disiplin militer
- Loyalis Raja Wenceslas IV

**Gaya bicara:**
- Formal, terstruktur, kalimat lengkap
- Ke Henry: "kau / engkau" (familiar tapi tegas, fatherly)
- Sering bicara soal kehormatan, tugas, loyalitas
- TIDAK vulgar

**Kosakata khas:**
- "Anakku" (ke Henry, sangat dekat)
- "Demi kehormatan..."
- "Tugas kita..."
- "Loyalitas pada Raja..."

---

### Sir Hans Capon

**ID code:** `hans`, `capon`

**Peran:** Bangsawan muda, partner banyak quest  
**Status:** Bangsawan, calon penerus Town of Rattay  
**Asal:** Rattay  
**Usia:** Awal 20-an  

**Kepribadian:**
- Bermulut besar, sombong di awal
- Womanizer (sering ke bathhouse)
- Berkembang jadi teman dekat Henry
- Suka berburu, berkuda, combat
- Buruk di catur & dadu

**Gaya bicara:**
- Formal-snobby awalnya, lebih akrab kemudian
- Ke Henry: "kau" (atasan ke bawahan awalnya), lalu setara
- Banyak referensi noble pursuits

**Kosakata khas:**
- "Henry, my friend..."
- Drama atas hal sepele
- Banyak bicara perempuan

---

### Captain Bernard

**ID code:** `bernard`

**Peran:** Pelatih combat Henry  
**Status:** Kapten militer  
**Asal:** Veteran perang  
**Usia:** 40-an  

**Kepribadian:**
- Veteran tough, tidak banyak basa-basi
- Peduli tapi ekspresinya kasar
- Hidup militer

**Gaya bicara:**
- Pendek, langsung, militeristik
- Banyak metafora pertempuran
- Boleh kasar tapi tidak vulgar berlebihan
- Ke Henry: "kau" (atasan ke bawahan)

**Kosakata khas:**
- "Dengar baik-baik..."
- "Demi setan..."
- Istilah teknis combat

---

### Pater Godwin

**ID code:** `godwin`

**Peran:** Pendeta Uzhitz, partner side-quest  
**Status:** Pendeta Katolik  
**Usia:** 40-an  

**Kepribadian:**
- Religius TAPI alkoholik
- Filosofis saat mabuk
- Hangat ke Henry
- Kontras: kotbah suci vs mabuk-mabukan

**Gaya bicara — DUA MODE:**

**Mode 1 (sober/formal):**
- Religius, Latin sesekali
- "Saudaraku", "anakku"
- Kutip Alkitab

**Mode 2 (mabuk):**
- Kacau, filosofis nyeleneh
- Kadang vulgar
- Cuping kata

**Kosakata khas:**
- "Dominus vobiscum" / "Damai sertamu"
- "Anakku..."
- "Begini, Henry..."
- Saat mabuk: makian ringan, filosofi nyeleneh

---

### Theresa

**ID code:** `theresa`

**Peran:** Love interest Henry, dari Skalitz  
**Status:** Anak tukang giling (Peshek's niece)  
**Asal:** Skalitz → Rattay Mill  
**Usia:** 20-an awal  

**Kepribadian:**
- Cerdas, mandiri, kuat
- Hangat, peduli
- Trauma dari penyerangan Skalitz
- A Woman's Lot DLC: tampil sebagai PC

**Gaya bicara:**
- Hangat, semi-formal
- Ke Henry: "kau" (akrab)
- Sopan tapi tidak kaku

**Kosakata khas:**
- Lembut, deskriptif
- Sering bicara soal Skalitz, masa lalu

---

### Johanka

**ID code:** `johan`, `johanka`

**Peran:** Visioner, calon biarawati  
**Status:** Anak yatim, kemudian di biara Sasau  
**Asal:** Skalitz (refugee)  

**Kepribadian:**
- Punya visi/wahyu (mirip Joan of Arc)
- Religius mendalam
- Kemudian dianggap penyihir oleh Gereja
- Tragic figure

**Gaya bicara:**
- Religius, sering bicara dengan istilah Katolik
- Lembut tapi mantap
- Saat visi: trance-like

---

### Sir Divish of Talmberg

**ID code:** `divis_z_ta`

**Peran:** Lord Talmberg, host Henry setelah Skalitz hancur  
**Status:** Lord  
**Asal:** Talmberg  

**Variant ejaan di file asli:** Lord Divis, Lord Divisch (gunakan **Lord Divish**)

**Gaya bicara:**
- Formal, terstruktur
- Sering bicara hukum, keadilan
- Ke pendakwa: "engkau" (tegas)

**Contoh:**
> "I hope you realize Sir Henry of Leipa never repealed his sentence against you."

→ "Saya harap engkau sadar, Sir Henry dari Leipa tidak pernah mencabut hukumannya atasmu."

---

### Lady Stephanie of Talmberg

**ID code:** `stephanie`

**Peran:** Istri Sir Divish, mengurus Henry saat sakit  
**Status:** Lady  

**Gaya bicara:**
- Halus, ibu-ibu noble
- Ke Henry: hangat, "kau"

---

### Sir Hanush of Leipa

**ID code:** `hanush`

**Peran:** Lord of Leipa, paman Sir Hans Capon, Lord of Rattay  
**Status:** Senior noble  

**Gaya bicara:**
- Sangat formal
- Berwibawa, otoritatif
- Frustasi dengan keponakannya yang naughty (Sir Hans)

---

### Brother Nicodemus

**ID code:** `nicodemus`

**Variants di file:** Nikodem, Nocodemus (gunakan **Brother Nicodemus**)

**Peran:** Biarawan Sasau, helpful figure  
**Status:** Monk  

**Gaya bicara:**
- Religius, helpful
- Diksi Latin sesekali

---

### Father Simon

**ID code:** `simon`

**Peran:** Pendeta Rattay  
**Status:** Priest  

**Gaya bicara:**
- Religius formal
- Mature, fatherly

---

### Miller Peshek

**ID code:** `peshek`

**Peran:** Paman Theresa, pemilik Rattay Mill  
**Status:** Penggiling (semi-illegal — millers di abad pertengahan dianggap kurang terhormat)  

**Gaya bicara:**
- Rakyat tapi cukup terdidik
- Punya bisnis sampingan (curi-curi)

---

### Kunesh

**ID code:** `kunesh`

**Peran:** Tukang bangun bermasalah (early game)  
**Status:** Rakyat/peminum  
**Asal:** Skalitz  

**Kepribadian:**
- Kasar, suka berkelahi
- Selalu marah
- Pemabuk

**Gaya bicara:**
- Vulgar, makian
- "Brengsek", "anjing", "bedebah"
- Ke Henry: "kau" kasar

---

### Mira

**ID code:** `mira`

**Peran:** Bath maid di Rattay  
**Status:** Pelayan pemandian  

**Gaya bicara:**
- Genit, akrab
- Ke pelanggan: "Tuanku"

---

### Captain Robard

**ID code:** `robard`

**Variant ejaan:** Robrad (gunakan **Captain Robard**)

**Peran:** Kapten pengawal Talmberg  

**Gaya bicara:**
- Militeristik, tegas
- Otoritatif

---

### Jan Zajíc / Hanekin Hare

**ID code:** `jan_zajic`

**Peran:** Side quest character (Master Huntsman story)  
**Catatan:** Nama Ceko `Jan Zajíc` = "John Hare". Versi Inggris pakai "Hanekin Hare". Dua-duanya merujuk karakter yang sama.

**Gaya bicara:**
- Religius, "It is the will of God..."
- Formal, terhormat

---

## Karakter Pendukung (Singkat)

Karakter ini akan diperkaya saat kita masuk ke dialog mereka:

### Skalitz Refugees
- **Martin** — Ayah Henry (mati di awal game)
- **Bianca** — Ibu Henry (mati di awal game)
- **Fritz** — Teman masa kecil
- **Matthew (Matúš)** — Teman masa kecil

### Sasau Monastery
- **Brother Cellarius** — Biarawan cellarman
- **Brother Cyril** — Scribe
- **Brother Elias** — Cook
- **Brother Eustice** — Helpful
- **Brother Gregor / Gregorius** — Senior
- **Brother Infirmarius** — Heal-master
- **Brother Librarian** — Library
- **Brother Overseer** — In charge
- **Brother Porter** — Gatekeeper
- **Brother Siskin** — Music

### Tradesmen at Pribyslavitz (DLC From the Ashes)
- **Innkeeper Adam**
- **Butcher Kochwurst** (Master Butcher)
- **Butcher Brisket** (Czech: Špejlík)
- **Trader Kornelius**
- **Woodcutter Kunesh**
- **Woodcutter Raspberry (Malina)**
- **Tavern maid Mirka**
- **Armoursmith Ota / Zach**
- **Armourer Fink** (Czech: Zvest)
- **Baker Silvester**
- **Groom Mark / Vashek**

### Royal/Historical
- **Raja Wenceslaus IV** (Wenceslas "the Idle")
- **Raja Sigismund** (Hungary, half-brother)
- **Emperor Charles IV** (late, father of Wenceslas)
- **Sir Markvart von Aulitz** — Bandit leader / antagonist
- **Sir Istvan Toth** — Antagonis utama

### Lainnya
- **Lord Henry of Leipa** — Different from Henry-PC; senior noble
- **Sir Vincent of Wartenberg** — Velish Castle
- **Master Huntsman Nicholas** — Antagonist in side quest
- **Wolflin of Kamberk** — Robber Baron (Raubritter)
- **Zmola, Zbyshek** — Bandits

---

## Karakter Generik (Tipe NPC)

### Guard (Pengawal Kota)
- **ID code:** `strazny`, `straznik`, dll
- Formal, otoritatif
- "Hentikan!" / "Berhenti di sana!"
- "Engkau" ke siapa saja

### Soldier (Prajurit)
- **ID code:** `vojak`
- Militeristik
- Pendek, langsung

### Commander (Komandan)
- **ID code:** `velitel`
- Tegas, perintah singkat

### Merchant (Pedagang)
- Sopan, praktis
- "Selamat datang, Tuan/Nona"
- Fokus transaksi

### Peasant (Petani)
- Membumi, kasual
- Bisa sopan ke Henry
- "Halo, kawan"

### Drunk (Pemabuk)
- Kacau, repetitif
- Makian ringan
- Kalimat tidak lengkap
- "Hik..."

---

## Update Character Bible

Saat menerjemahkan dialog, jika kamu identifikasi karakter baru:

1. **Tambahkan entry** dengan format standar
2. **Tulis voice/style** berdasarkan dialog yang sudah ada
3. **Commit** dengan tipe `docs(character-bible)`
4. **Update CHANGELOG.md** kalau karakter penting
