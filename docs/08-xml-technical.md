# XML Technical Notes — KCD Specific

Catatan teknis tentang struktur file XML Kingdom Come: Deliverance. **Berdasarkan analisis aktual** dari 11 file XML.

---

## Struktur Dasar File XML KCD

### Format Aktual (Confirmed)

```xml
<Table>
<Row><Cell>STRING_ID</Cell><Cell>Original_English</Cell><Cell>Display_English</Cell></Row>
<Row><Cell>another_id</Cell><Cell>Another text</Cell><Cell>Another text</Cell></Row>
...
</Table>
```

**PENTING:**
- ❌ **TIDAK ADA** XML declaration (`<?xml version="1.0"?>`) di awal — langsung mulai dengan `<Table>`
- ✅ Setiap `<Row>` punya tepat **3 `<Cell>`**
- ✅ Tag `<Table>` di awal, `</Table>` di akhir file

### Tiga Cell, Tiga Peran

| Cell # | Peran | Edit? |
|--------|-------|-------|
| Cell #1 | **String ID** (unique identifier) | ❌ JANGAN UBAH |
| Cell #2 | **Original English** (internal reference) | ❌ JANGAN UBAH |
| Cell #3 | **Display text** (yang tampil di game) | ✅ **INI YANG DITERJEMAHKAN** |

**Mengapa ada 3 cell?** Warhorse menggunakan Cell #2 sebagai reference internal (kadang Cell #2 dan #3 berbeda, menunjukkan revisi historis). Game hanya menampilkan **Cell #3**.

### Contoh Real dari File

```xml
<Table>
<Row><Cell>ui_hud_drop_body</Cell><Cell>Drop body</Cell><Cell>Drop body</Cell></Row>
<Row><Cell>ui_hud_pick_up_body</Cell><Cell>Pick up body</Cell><Cell>Pick up body</Cell></Row>
</Table>
```

---

## ID Encoding (Dialog Files)

### Dialog ID Pattern

```
t[N]_s[N]_[N]_[speaker_code]_[hash]
```

Contoh:
- `t10001_s15335_0_ludmila_al_g9cK`
  - `t10001` = ?
  - `s15335` = ?
  - `0` = sequence
  - `ludmila_al` = speaker (Ludmila + alphabet variant?)
  - `g9cK` = hash unik

- `t10037_s15395_0_divis_z_ta_HHOB`
  - speaker: `divis_z_ta` = Sir Divish (z Talmberka = "dari Talmberg" di Ceko)

- `t9919_s15191_1_ui`
  - `_ui` = **Player choice option** (pilihan dialog dari sudut pandang Henry)

### Quest ID Pattern

```
chap[N|_dlc[N]]_sch[N]_[hash]_e[N]_[hash]
```

Contoh:
- `chap_dlc1_sch4_aoMw_e1_nm62` = DLC1, Scheme 4, event 1
- `chap17_t1C_sch3_JglP_e2_NFgO` = Chapter 17, scheme 3, event 2

### UI ID Pattern

```
[category]_[name]
```

Contoh:
- `ui_hud_drop_body`
- `ui_nh_add_alchemy` (NH = New Hamlet / Pribyslavitz)
- `ui_nh_structure_name_baker1`
- `buff_alcoholism`
- `game_over_died_by_poison`

**JANGAN ubah ID apapun** — bahkan kalau terlihat aneh, itu reference internal Warhorse.

---

## Encoding

- **File asli**: tidak ada deklarasi encoding (default ASCII tapi support UTF-8)
- **Save sebagai UTF-8** di editor kamu
- **Line ending**: LF (Unix) — di-handle oleh `.gitattributes`
- File mendukung karakter spesial Eropa Tengah:
  - Czech: `á é í š ř č ě ý ž ó ú ů ť ň`
  - German: `ö ü ä ß`
  - Hungarian: `ő ű`
  - Polish: `ł`

### Karakter Spesial yang Ditemukan di File

Diurutkan berdasarkan frekuensi (dari analisis aktual):

| Karakter | Jumlah Muncul | Penanganan |
|----------|---------------|------------|
| `'` (apostrophe curly) | 13,828 | Pertahankan — banyak di possessive ("Henry's") |
| `…` (ellipsis single char) | 6,584 | Pertahankan |
| `á` | 1,963 | Pertahankan (nama Czech) |
| `é` | 932 | Pertahankan |
| `í` | 685 | Pertahankan |
| `–` (en-dash) | 516 | Pertahankan |
| `š` | 500 | Pertahankan |
| `ř` | 344 | Pertahankan |
| `č` | 255 | Pertahankan |
| `ě` | 272 | Pertahankan |
| `ý` | 175 | Pertahankan |
| `ž` | 141 | Pertahankan |
| `ť ň ó ú ů ä` | <300 | Pertahankan |
| `ö` | 330 | Pertahankan |
| `ü` | 144 | Pertahankan |
| `ő` | 148 | Pertahankan |
| `ű` | 42 | Pertahankan |
| `ł` | 42 | Pertahankan |
| `"` `"` `'` `'` (smart quotes) | banyak | Pertahankan sesuai original |

---

## Karakter Escape XML

XML butuh escape untuk karakter tertentu:

| Karakter | Escape XML | Catatan |
|----------|-----------|---------|
| `&` | `&amp;` | **Selalu** escape |
| `<` | `&lt;` | **Selalu** escape |
| `>` | `&gt;` | Direkomendasikan escape |
| `"` | `&quot;` | Escape dalam atribut |
| `'` | `&apos;` | Escape dalam atribut |

### Contoh:

```xml
<!-- SALAH -->
<Cell>Bread & butter</Cell>

<!-- BENAR -->
<Cell>Bread &amp; butter</Cell>
```

---

## ⚠️ DUA TINGKAT ESCAPE (Critical!)

KCD pakai **dua tingkat escape** tergantung konteks:

### Single Escape (Most Common)

Digunakan untuk **markup yang di-render game sebagai HTML**:

```
&lt;br/&gt;          → di-render sebagai <br/> (line break)
&amp;nbsp;           → di-render sebagai &nbsp; (non-breaking space)
&lt;font color='#XXX'&gt; → di-render sebagai <font color='#XXX'> (warna teks)
```

### Double Escape (Less Common, Tapi Ada!)

Digunakan saat markup HARUS tampil sebagai literal text atau di-encode sekali lagi:

```
&amp;lt;br/&amp;gt;          → di-render sebagai &lt;br/&gt; (literal teks)
&amp;lt;img src='...'&amp;gt; → di-render sebagai &lt;img src='...'&gt;
```

### Cara Membedakan

**Lihat di file asli:**
- Kalau aslinya `&lt;br/&gt;` → tetap `&lt;br/&gt;`
- Kalau aslinya `&amp;lt;br/&amp;gt;` → tetap `&amp;lt;br/&amp;gt;`

**JANGAN konversi antar keduanya!**

---

## Placeholder & Variabel Game

### 1. Format String Placeholders

| Placeholder | Arti | Contoh Inggris | Indonesia |
|-------------|------|----------------|-----------|
| `%s` | String generic | "Picked up %s" | "Mengambil %s" |
| `%d`, `%i` | Integer | "%d arrows left" | "%d anak panah tersisa" |
| `%f` | Float | jarang | jarang |

### 2. Positional Placeholders

| Placeholder | Arti | Contoh Inggris | Indonesia |
|-------------|------|----------------|-----------|
| `{0}`, `{1}` | Slot positional | "Take {0} {1}" | "Ambil {0} {1}" atau "Ambil {1} {0}" (sesuai grammar) |

**Indonesia tip**: Indonesia kadang butuh swap urutan. Misal:
- "5 arrows" → "{0} arrows" → "{0} anak panah" (urutan sama)
- "the red sword" → "the {0} {1}" → "{1} {0}" karena "{1}" (red) jadi modifier setelah noun "{0}" (sword)

### 3. Keybinding Placeholders (`$keyname;`)

**Format**: `$variable;` dengan **semicolon di akhir** (critical!)

**Daftar lengkap yang ditemukan di tutorials.xml:**

```
$alch_use_bag;          alchemy bag key
$attack1;               serangan tipe 1
$attack1_mouse;         serangan tipe 1 (mouse)
$attack2;               serangan tipe 2
$attack3;               serangan tipe 3
$attack_abort;          batal serangan
$attack_abort_mouse;    batal serangan (mouse)
$block;                 tangkis/blok
$call_horse;            panggil kuda
$font_color;            warna font (markup)
$font_end;              akhir warna font
$h;                     header (markup)
$h_end;                 akhir header
$horse_sprint;          sprint kuda
$jump;                  lompat
$lock_dir_fwd;          arah lockpicking forward
$moveback;              gerak mundur
$moveforward;           gerak maju
$moveleft;              gerak kiri
$moveright;             gerak kanan
$p;                     paragraph
$read_select;           pilih saat baca
$read_toggle;           toggle baca
$sitting_sleep;         duduk/tidur
$sprint;                lari
$surrender;             menyerah
$surrender_xi_activate; aktifkan menyerah (Xbox)
$surrender_xi_modifier; modifier menyerah (Xbox)
$toggle_crouch;         toggle jongkok
$toggle_run;            toggle lari
```

**Contoh penggunaan:**

```xml
<Cell>Press $attack1; to perform a basic attack.</Cell>
```

**Terjemahan BENAR:**
```xml
<Cell>Tekan $attack1; untuk melakukan serangan dasar.</Cell>
```

**Terjemahan SALAH (placeholder hilang):**
```xml
<Cell>Tekan tombol serang untuk melakukan serangan dasar.</Cell>
```

### 4. State/Action Tags (`[tag]`)

Format: `[name]` dalam kurung siku biasa.

**Yang ditemukan di analisis:**

```
[muttering]      bisikan/gumaman
[riposte]        balas serang
[feint]          tipuan
[dodge]          mengelak
[warn]           peringatan
[combo]          kombo
[arrest]         penangkapan
[hangover]       hangover
[hunger]         lapar
[tiredness]      lelah
[overeating]     kekenyangan
[alcoholism]     alkoholisme
[inebriation]   mabuk
[explain]        penjelasan
[cz]             Czech (language tag?)
```

**Aturan:** Pertahankan sebagai-adanya, JANGAN diterjemahkan ke Indonesia.

### 5. Game Variable (Sangat Jarang)

| Placeholder | Arti |
|-------------|------|
| `[player_name]` | Nama player (biasanya "Henry") |
| `\n` | Newline |
| `\t` | Tab |
| `\\` | Backslash literal |

---

## Markup Tags (Markup Aktual di File)

### Yang Paling Sering (Berdasarkan Analisis)

| Tag | Jumlah | Fungsi |
|-----|--------|--------|
| `&lt;br/&gt;` / `&amp;lt;br/&amp;gt;` | 2,285+ | Line break |
| `&amp;lt;p align='center'&amp;gt;` | 266 | Paragraph center |
| `&amp;lt;font color='#512D00'&amp;gt;` | 202 | Coklat (teks lama) |
| `&amp;lt;p align='left'&amp;gt;` | 100 | Paragraph kiri |
| `&amp;lt;font size='25'&amp;gt;` | 86 | Font size 25 |
| `&amp;lt;p&amp;gt;` | 54 | Paragraph default |
| `&amp;lt;font color='#ffffff'&amp;gt;` | 46 | Putih |
| `&amp;lt;font color='#B8AE7E'&amp;gt;` | 46 | **Emas (highlight quest)** |
| `&amp;lt;font color='#990000'&amp;gt;` | 18 | Merah (peringatan) |
| `&amp;lt;font size='32'/'40'&amp;gt;` | 24+8 | Font besar |

### Image Embeds

```xml
&amp;lt;img src='img://Libs/UI/Textures/Dynamic/dice_one.dds' width='22' height='22'&amp;gt;
&amp;lt;img src="img://Libs/UI/Textures/Dynamic/ccursor1.dds" width="70" height="60"&amp;gt;
```

**Aturan**: JANGAN ubah `src=`, `width=`, `height=`. Pertahankan apa adanya.

### Custom KCD Tags (Jarang)

```
[K]actionname[/K]              keybinding action (teks dalam jangan diterjemahkan!)
[COLOR=#XXXXXX]text[/COLOR]    warna teks (boleh terjemahkan text dalam tag)
```

---

## Common Patterns & Edge Cases

### 1. Trailing Spaces (Bug Asli Warhorse)

Beberapa Cell punya trailing space di akhir text:
```xml
<Cell>Charcoal </Cell>
```

**Tetap pertahankan** trailing space — itu kadang sengaja (untuk formatting).

### 2. Cell Kosong

```xml
<Cell></Cell>
```

Jarang ada Cell kosong, tapi kalau ada → biarkan kosong di terjemahan juga.

### 3. Cell Hanya Whitespace

```xml
<Cell>   </Cell>
```

Biarkan whitespace-only sesuai original.

### 4. Multi-line Text (di Dialog/Quest)

```xml
<Cell>Line 1.

Line 2.</Cell>
```

Newline di dalam Cell dipertahankan.

### 5. Mixed Markup

```xml
<Cell>You have unlocked the perk &amp;lt;font color='#B8AE7E'&amp;gt;First Aid II&amp;lt;/font&amp;gt;.&amp;lt;br/&amp;gt;Using bandages is now more effective.</Cell>
```

Terjemahkan:
```xml
<Cell>Engkau telah membuka perk &amp;lt;font color='#B8AE7E'&amp;gt;First Aid II&amp;lt;/font&amp;gt;.&amp;lt;br/&amp;gt;Penggunaan perban kini lebih efektif.</Cell>
```

**Catatan**: nama perk "First Aid II" tetap (atau cek glossary [perks-buffs.md](../glossaries/perks-buffs.md) untuk terjemahan).

---

## Re-Pack ke .pak (untuk Install ke Game)

Setelah terjemahan selesai, untuk pakai in-game perlu di-pack ke `.pak`:

### Cara Manual (7-Zip)

1. Pastikan struktur folder:
   ```
   Indonesian_xml/
     Libs/
       Localization/
         Indonesian_xml/
           text_ui_HUD.xml
           text_ui_dialog.xml
           ... (semua file)
   ```

2. Pilih folder `Libs/`
3. Klik kanan → 7-Zip → **Add to archive...**
4. Settings:
   - Archive name: `Indonesian_xml.zip`
   - Archive format: **zip** (BUKAN 7z!)
   - Compression level: **Store** (no compression)
5. Klik OK
6. Rename `Indonesian_xml.zip` → `Indonesian_xml.pak`

### Install ke Game

**Cara 1: Replace English**
1. Backup `Localization/English_xml.pak` (rename ke `.bak`)
2. Rename `Indonesian_xml.pak` → `English_xml.pak`
3. Place di `[KCD]/Localization/`
4. Launch game (akan tampil terjemahan Indonesia di "English")

**Cara 2: Sebagai Mod**

Buat struktur mod:
```
Mods/
  IndonesianTranslation/
    mod.manifest
    Localization/
      Indonesian_xml.pak
```

Isi `mod.manifest`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<kcd_mod>
    <info>
        <name>Indonesian Translation</name>
        <description>Terjemahan Bahasa Indonesia untuk KCD</description>
        <author>Ryan Nurhidayat</author>
        <version>1.0.0</version>
        <created_on>2026-05-27</created_on>
    </info>
</kcd_mod>
```

---

## Validation Tools

### Cek XML Valid

**Online**: https://www.xmlvalidation.com/

**VS Code**: dengan extension XML Tools — auto-validate saat save.

**Command line (Linux/Mac)**:
```bash
xmllint --noout translation/indonesian/text_ui_HUD.xml
```

### Cek Placeholder Tidak Hilang

```bash
# Hitung placeholder di original vs translation
grep -oE '%s|\{[0-9]\}|\$[a-z_]+;' source/english/text_ui_HUD.xml | wc -l
grep -oE '%s|\{[0-9]\}|\$[a-z_]+;' translation/indonesian/text_ui_HUD.xml | wc -l
```

Hasil harus **sama**.

### Cek Row Count Sama

```bash
grep -c '<Row>' source/english/text_ui_HUD.xml
grep -c '<Row>' translation/indonesian/text_ui_HUD.xml
```

Harus **sama** persis.

---

## Common Errors & Solutions

### Error 1: Game Crash Setelah Install Translation

**Penyebab umum:**
1. Struktur XML rusak (tag tidak balance)
2. Karakter spesial tidak di-escape
3. Encoding salah
4. ID string berubah/duplikat

**Solusi:**
1. Validasi XML di VS Code (lihat error)
2. Cek encoding: harus UTF-8
3. Bandingkan dengan file asli, cari perbedaan struktur
4. Compare ID count dengan original

### Error 2: Teks Tampil sebagai `?????` atau Kotak

**Penyebab:** Karakter Unicode tidak di-render font game.

**Solusi:**
- Hindari karakter khusus yang tidak ada di font default KCD
- Cek dengan test in-game
- Karakter Indonesia standar (a-z, A-Z, 0-9, tanda baca) seharusnya aman

### Error 3: String Tidak Ter-translate, Masih English

**Penyebab:**
1. ID string diubah → game tidak temukan
2. File tidak ter-load (cek nama file, lokasi)
3. Cache game (restart total game)
4. Cell #3 sama dengan Cell #2 (lupa terjemahkan)

### Error 4: Placeholder Aneh di Game (`%s` muncul literal)

**Penyebab:** Placeholder diganti dengan teks Indonesia.

**Solusi:** Restore placeholder, jangan hapus.

### Error 5: Format Markup Berantakan

**Penyebab:** Tag HTML di-escape salah level.

**Solusi:** Cek apakah aslinya single (`&lt;`) atau double escape (`&amp;lt;`), restore.

---

## Tools yang Direkomendasikan

### VS Code Extensions

```
XML Tools           Josh Johnson — wajib (validate, format)
XML Language       Red Hat — alternatif
GitLens            git insights
Markdown All in One MD editing
```

### Command-Line Tools

```bash
xmllint            cek XML valid
diff               compare file before/after
grep               cari pattern, count placeholders
wc                 hitung baris/karakter
```

### 7-Zip

Untuk pack/unpack `.pak`:
- Windows: https://www.7-zip.org/
- Linux/Mac: `p7zip-full`
