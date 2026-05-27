# Claude Code Prompts — Template Siap-Pakai

Koleksi prompt yang sudah di-tune untuk dipakai langsung di **Claude Code Max di VS Code**. CLAUDE.md di root sudah memberikan foundation, prompt di sini fokus ke task spesifik.

---

## 🎯 Cara Pakai

1. Buka VS Code dengan folder repo `kcd-indonesian-translation/`
2. Buka Claude Code Max sidebar
3. **Copy prompt dari section yang relevan**
4. Paste ke Claude Code, tweak {variable} sesuai konteks
5. Submit → Claude Code execute task

---

## 📋 Master Pre-Flight Check (Untuk Awal Session)

Pakai ini di **setiap session baru** sebelum mulai translation task. Memastikan Claude Code sudah load semua konteks.

```
Saya akan mulai sesi terjemahan KCD ke Bahasa Indonesia. 

Sebelum kita mulai, tolong baca file-file berikut secara berurutan untuk memuat konteks proyek:

1. CLAUDE.md (di root) — instruksi proyek
2. docs/01-style-guide.md — pedoman gaya
3. docs/02-glossary-master.md — glossary master
4. docs/08-xml-technical.md — teknis XML

Setelah baca, konfirmasi:
- Kamu paham peran sebagai penerjemah game profesional
- Kamu paham aturan teknis XML (Cell #1 & #2 tidak diubah, hanya Cell #3)
- Kamu paham placeholder yang harus dipertahankan ($keyname;, %s, {0}, [tag])
- Kamu siap untuk task spesifik selanjutnya

Setelah konfirmasi, tunggu instruksi file mana yang akan diterjemahkan.
```

---

## 🚀 PILOT — File Pertama (text_ui_HUD.xml)

Pakai prompt ini untuk **file paling kecil**, sebagai pilot/kalibrasi.

```
Pilot translation: text_ui_HUD.xml

File ini cuma 2 string — sempurna untuk kalibrasi gaya.

Tugas:
1. Baca source/english/text_ui_HUD.xml
2. Konsultasi glossaries/ui-terms.md untuk istilah UI
3. Copy file ke translation/indonesian/text_ui_HUD.xml
4. Terjemahkan Cell #3 saja

Konteks:
- "Drop body" muncul di HUD saat Henry sedang membawa jasad NPC (e.g., setelah stealth kill, untuk menyembunyikan korban)
- "Pick up body" muncul saat Henry dekat dengan jasad

Style:
- Formal sastra (sesuai style guide)
- Pakai "jasad" bukan "mayat" (lebih sastra & netral)

Output yang saya harapkan:
1. Tampilkan diff translation file
2. Konfirmasi struktur XML valid
3. Suggest commit message dengan format standar
4. JANGAN auto-commit — tunggu approval saya

Mulai.
```

---

## 📁 Template: Terjemahkan File Kecil (<200 rows)

Untuk file kecil seperti `text_rich_presence.xml`, `text_ui_minigames.xml`, `text_ui_misc.xml`, `text_ui_tutorials.xml`.

```
Translation task: {NAMA_FILE}.xml

Tugas:
1. Baca source/english/{NAMA_FILE}.xml — laporkan jumlah rows
2. Pre-read seluruh file untuk identifikasi:
   - Karakter yang muncul (jika dialog)
   - Istilah berulang (perlu konsistensi)
   - Placeholder/markup khusus
   - Konten istimewa (book, religious, dll)
3. Konsultasi:
   - docs/01-style-guide.md untuk gaya
   - glossaries/ yang relevan
   - docs/03-character-bible.md jika ada karakter
   - docs/04-religious-terms.md jika ada konten religius
4. Copy source ke translation/indonesian/{NAMA_FILE}.xml
5. Terjemahkan Cell #3 untuk SEMUA rows
6. Validate XML structure
7. Update glossary kalau ada istilah baru
8. Update progress.md (set status ke selesai, isi nama & tanggal)
9. Show diff & suggest commit message

Catatan khusus untuk file ini:
- {SPECIFIC_NOTES_IF_ANY}

Setelah selesai:
- Tampilkan ringkasan: jumlah string ter-translate, istilah baru di glossary
- Flag hal yang perlu perhatian saya
- JANGAN commit — tunggu saya review

Mulai dari step 1.
```

### Contoh Penggunaan (Isi {NAMA_FILE} dan {SPECIFIC_NOTES}):

**Untuk `text_rich_presence.xml`:**
```
{NAMA_FILE} = text_rich_presence
{SPECIFIC_NOTES_IF_ANY} = 
- Ini Discord/Xbox rich presence status
- Ada placeholder %s dan {0} — pertahankan
- Tone: ringkas, status-like ("Playing the quest X" style)
```

**Untuk `text_ui_minigames.xml`:**
```
{NAMA_FILE} = text_ui_minigames  
{SPECIFIC_NOTES_IF_ANY} =
- Ini konten DLC "From the Ashes" — Pribyslavitz village building
- Banyak istilah ekonomi (Forge, Bakery, Brewery, Beehives, dll)
- "Rathaus" dipertahankan (Jerman)
- Cek glossaries/places.md bagian Pribyslavitz Buildings
```

---

## 📁 Template: Terjemahkan File Menengah (200-1000 rows)

Untuk `text_ui_ingame.xml`, `text_ui_soul.xml`.

```
Translation task: {NAMA_FILE}.xml

Karena file ini ukurannya menengah, mari split dalam batch.

Tugas total:
1. Pre-read & report total rows
2. Identifikasi struktur konten (kategori, pattern ID)
3. Konsultasi semua docs & glossary relevan
4. Translate dalam batch (sebut batch size pilihan kamu, biasanya 100-200 rows per batch)
5. Setiap batch selesai → show diff & wait konfirmasi saya untuk lanjut
6. Setelah semua batch selesai → update glossary, progress.md, suggest commit

Catatan khusus untuk file ini:
{SPECIFIC_NOTES}

Mulai dari pre-read dan report struktur file.
```

### Catatan khusus per file menengah:

**Untuk `text_ui_ingame.xml`:**
```
- 396 dari 781 rows adalah Kickstarter backer names (ID: cfnm_*)
- Backer names JANGAN diterjemahkan — copy Cell #2 ke Cell #3
- Hanya ~385 rows non-cfnm yang efektif perlu diterjemahkan
- Pisahkan batch: batch backer names dulu (auto-copy), lalu batch UI real
```

**Untuk `text_ui_soul.xml`:**
```
- Ini file perks, buffs, status effects
- WAJIB konsultasi glossaries/perks-buffs.md
- Banyak deskripsi efek dengan format "Strength +2, Charisma -3"
- Numeric stats tidak diubah, hanya teks deskriptif
- Title case untuk nama perk (e.g., "Hati Nurani Bersih")
- Konsisten penggunaan nama atribut (Strength → Kekuatan, dll)
```

---

## 📁 Template: Terjemahkan File Besar (1000-7000 rows)

Untuk `text_ui_menus.xml`, `text_ui_items.xml`, `text_ui_quest.xml`.

```
Translation task: {NAMA_FILE}.xml — File besar, butuh strategi batching ketat.

Strategi:
1. Pre-read & report total rows dan kategori
2. Buat plan: split jadi berapa batch, kategori apa
3. Translate batch demi batch dengan checkpoint
4. Setelah 500 rows: pause untuk QA review oleh saya
5. Update glossary intensif (banyak istilah baru kemungkinan)

Catatan khusus untuk file ini:
{SPECIFIC_NOTES}

Workflow:
1. Pre-read & report
2. Tunggu saya approve strategi batching
3. Translate batch 1
4. Show diff & report new glossary entries
5. Tunggu saya approve lanjut
6. Repeat sampai selesai

Mulai dari pre-read.
```

### Catatan khusus:

**Untuk `text_ui_menus.xml`:**
```
- UI menus + duplikat buff descriptions (dengan suffix _t = tooltip)
- Banyak overlap dengan text_ui_soul.xml — konsisten dengan terjemahan di sana
- Konsultasi glossaries/ui-terms.md
- Banyak istilah teknis (Resolution, Anti-aliasing, dll) — terjemahkan ke Indonesia kecuali istilah baku
```

**Untuk `text_ui_items.xml`:**
```
- ITEM NAMES + DESKRIPSI + BOOK CONTENTS
- Strategi 3 jenis:
  1. Item names (literal, ringkas)
  2. Item descriptions (sastra ringan)
  3. BOOK CONTENTS (archaic style, "did commit", "did state")
- Konsultasi glossaries/items.md intensif
- Untuk book content: gunakan gaya bahasa hukum/sastra abad pertengahan
- 200+ entry book content — TBD strategi terjemahan
```

**Untuk `text_ui_quest.xml`:**
```
- Quest descriptions: pengantar, objektif, summary
- Cross-reference dengan main story
- Konsultasi character bible untuk karakter yang muncul
- Banyak quest title — pertahankan title case (e.g., "Baptism of Fire" → "Baptis Api"? atau dipertahankan?)
- TBD: terjemahkan quest titles atau pertahankan English?
```

---

## 📁 Template: Mega File (text_ui_dialog.xml — 65,982 rows)

```
Translation task: text_ui_dialog.xml — FILE MEGA, ini proyek multi-bulan.

Strategi awal:
1. Pre-read & report struktur:
   - Total rows
   - Berapa unique speaker codes
   - Berapa chapters teridentifikasi (chap0, chap1, dst)
   - Sample dialog dari beberapa chapter

2. Diskusi strategi batching dengan saya:
   - Per chapter?
   - Per character batch?
   - Per scene?

3. JANGAN langsung terjemahkan. Tunggu approval strategi.

Setelah strategi disepakati, kita lanjut per batch dengan ketat:
- Max 200 rows per batch
- Show diff setelah tiap batch
- Update character bible kalau ada karakter baru
- Update glossary intensif

Mulai dari pre-read & report.
```

---

## 🔍 Template: QA Review (Setelah Terjemah)

Untuk self-review sebelum commit, atau review file yang sudah ada.

```
QA review task: translation/indonesian/{NAMA_FILE}.xml

Tolong jalankan QA checklist lengkap (docs/07-qa-checklist.md) pada file ini.

Bagian yang harus dicek (laporkan pass/fail untuk tiap bagian):

1. Teknis XML
   - Struktur utuh
   - Jumlah Row sama dengan source
   - Cell #1 dan #2 tidak diubah
   - Encoding UTF-8
   - Karakter spesial intact

2. Placeholders
   - Semua %s, {0}, $keyname;, [tag] dipertahankan
   - Urutan sesuai grammar Indonesia
   - Tidak ada placeholder hilang

3. Markup HTML
   - <br/>, <font>, <img> struktur utuh
   - Escape level konsisten dengan source

4. Bahasa
   - Sesuai style guide
   - Konsisten dengan glossary
   - Voice karakter sesuai bible (jika dialog)
   - Spelling variants di-normalize
   - Tidak ada slang/anakronisme

5. Terminologi
   - Cross-check dengan glossaries/
   - Konsistensi terminologi berulang

6. Penulisan Indonesia
   - EYD/PUEBI
   - Kapitalisasi
   - Tanda baca

Output:
- List semua issue yang ditemukan
- Severity (critical/major/minor)
- Rekomendasi fix untuk tiap issue
- Overall verdict: ready to commit, atau perlu revisi
```

---

## 📝 Template: Update Glossary

Saat kamu temukan istilah baru selama terjemahan.

```
Glossary update task: tambahkan istilah baru yang ditemukan saat menerjemahkan {NAMA_FILE}.xml

Istilah baru:
1. {Original} - {Indonesia} - {Catatan/Konteks}
2. {Original} - {Indonesia} - {Catatan/Konteks}
...

Tugas:
1. Identifikasi glossary file yang tepat untuk tiap istilah
2. Tambahkan entry dengan format yang konsisten
3. Pastikan tidak ada duplikat dengan entry existing
4. Update last-modified date di glossary
5. Suggest commit message dengan tipe `glossary`

Output:
- Diff dari setiap glossary file yang di-update
- Konfirmasi tidak ada conflict dengan entry lama
- Commit message
```

---

## 🔄 Template: Cross-Check Konsistensi

Untuk cek konsistensi terminologi antar file.

```
Cross-check consistency task: cari inkonsistensi terminologi di translation/indonesian/

Tugas:
1. Identifikasi istilah berulang yang berpotensi inkonsisten (terutama gelar, nama karakter, item names)
2. Grep keseluruhan translation/indonesian/ untuk tiap istilah
3. Bandingkan terjemahan di berbagai file
4. Laporkan inkonsistensi yang ditemukan

Contoh istilah yang sering inkonsisten:
- "Lord X" — kadang "Tuanku X", kadang "Lord X"
- "Sir X" — biasanya "Sir X" tapi cek
- "Brother X" — "Bruder X" wajib konsisten
- "Father X" — "Pater X" wajib konsisten
- Nama tempat dengan typo asli (Samopesch vs Samopesh)

Output:
- Tabel inkonsistensi: istilah, file, terjemahan saat ini, rekomendasi
- Sarankan glossary update jika perlu
- Sarankan revise commit untuk fix
```

---

## 🐛 Template: Fix Specific Bug

Untuk perbaikan spesifik (typo, mistranslation, dll).

```
Fix task: perbaikan di translation/indonesian/{NAMA_FILE}.xml

Issue: {DESKRIPSI BUG}
Location: String ID {STRING_ID} (atau baris {BARIS})

Original Indonesia:
"{teks salah}"

Original English (Cell #2):
"{teks asli}"

Yang seharusnya:
"{teks benar}"

Alasan:
{KENAPA YANG SEKARANG SALAH}

Tugas:
1. Verifikasi issue dengan baca file
2. Apply fix
3. Cek apakah issue sama muncul di file lain (kalau ya, fix juga)
4. Update QA notes jika perlu
5. Suggest commit message dengan tipe `fix`

JANGAN auto-commit. Show diff dulu.
```

---

## 🎬 Template: Komit & Update Progress

Setelah translation task selesai dan saya sudah approve.

```
Finalize task: commit changes untuk {NAMA_FILE}.xml

Tugas:
1. Update progress.md:
   - Status file → 🟦 (selesai, menunggu review) atau 🟩 (jika solo)
   - Translator: {NAMA}
   - Tanggal: {TODAY}
2. Stage SEMUA changes yang relevan:
   - translation/indonesian/{NAMA_FILE}.xml
   - progress.md
   - glossaries/ yang ada perubahan
3. Buat commit dengan message:
   ```
   {COMMIT MESSAGE YANG SUDAH DI-APPROVE}
   ```
4. Verify commit berhasil
5. JANGAN push — saya yang push manual via VS Code sync

Output: konfirmasi commit + commit hash
```

---

## 💡 Tips Penggunaan

### Saat Mulai Session Baru
Selalu pakai **"Master Pre-Flight Check"** dulu. Ini load context.

### Saat Konsultasi Cloud (Saya)
Saat kamu butuh decision yang sulit (gelar, terjemahan ambiguous, voice character), copy konteks dari Claude Code Max ke chat sini. Saya kasih guidance, kamu balik ke Claude Code dengan jawabannya.

### Saat Stuck
- Coba prompt yang lebih spesifik
- Tambah konteks (sebagian source content)
- Eskalasi ke saya

### Saat File Mega (dialog.xml)
- JANGAN coba kerjakan sekaligus
- Plan strategy dulu (per chapter? per character?)
- Save WAJIB setelah tiap batch
- Commit per batch (jangan kumpulkan)

---

## 🔁 Iterasi & Feedback Loop

Workflow ideal:

```
1. User minta task di Claude Code Max
2. Claude Code Max execute (dengan konteks dari CLAUDE.md + docs)
3. Show output ke user
4. User cek:
   a. OK → commit di Claude Code Max
   b. Ragu → konsultasi ke Claude Cloud (sini)
5. Claude Cloud (sini) review & advise
6. User balik ke Claude Code Max dengan advice
7. Iterasi sampai OK
8. Commit & push
```

---

## 📂 Quick Reference: File-File Penting

```
CLAUDE.md                         ← Auto-load oleh Claude Code, base instructions
docs/01-style-guide.md            ← Pedoman gaya bahasa
docs/02-glossary-master.md        ← Hub glossary
docs/03-character-bible.md        ← Voice karakter
docs/04-religious-terms.md        ← Terminologi Katolik
docs/05-historical-context.md     ← Konteks Bohemia 1403
docs/06-workflow.md               ← Workflow standar
docs/07-qa-checklist.md           ← QA wajib
docs/08-xml-technical.md          ← Teknis XML
docs/09-claude-prompts.md         ← File ini (template prompts)
glossaries/*.md                   ← Sub-glossary per kategori
source/english/                   ← XML original (read-only)
translation/indonesian/           ← Hasil terjemahan
progress.md                       ← Tracking progress
```

---

**Versi:** 1.0  
**Last updated:** 2026-05-27
