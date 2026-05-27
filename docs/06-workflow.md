# Translation Workflow — Proses Kerja End-to-End

Dokumen ini menjelaskan alur kerja untuk menerjemahkan satu file XML.

---

## Alur Standar (Per File)

```
1. PILIH FILE       ← progress.md
        ↓
2. KLAIM           ← Issue: "WIP: text_ui_X.xml"
        ↓
3. COPY FILE       ← source/english/ → translation/indonesian/
        ↓
4. READ-THROUGH    ← Baca seluruh file dulu (tanpa terjemah)
        ↓
5. RISET           ← Identifikasi istilah baru, cek glossary
        ↓
6. TERJEMAHKAN     ← Tahap utama
        ↓
7. UPDATE GLOSSARY ← Tambah istilah baru
        ↓
8. SELF-REVIEW     ← QA checklist
        ↓
        ├─ Lolos? → 9. COMMIT
        └─ Tidak? → ulang 6-8
              ↓
9. COMMIT          ← Format standar
        ↓
10. UPDATE PROGRESS ← progress.md
        ↓
11. PUSH & PR      ← (kalau kolaborasi)
```

---

## Step-by-Step

### Step 1: Pilih File

1. Buka [progress.md](../progress.md)
2. Pilih file dengan status ⬜ (belum dimulai)
3. **Untuk kontribusi PERTAMA**: mulai dari Tahap 1 (file kecil)
4. Update status ke 🟨 + isi nama translator

### Step 2: Klaim & Setup

```bash
# Buat branch baru
git checkout -b translate/text_ui_HUD

# Atau via VS Code: Source Control → Branch → Create
```

1. Buat issue: `WIP: text_ui_HUD.xml — [Nama Translator]`
2. Beri label: `translation`, `in-progress`
3. Assign ke diri sendiri

### Step 3: Copy File

```bash
cp source/english/text_ui_HUD.xml translation/indonesian/text_ui_HUD.xml
```

Atau di VS Code: copy-paste manual.

### Step 4: Read-Through Pertama

**JANGAN langsung terjemahkan!** Baca dulu seluruh file:

- Pahami konteks
- Identifikasi karakter yang muncul (dari dialog ID)
- Catat terminologi yang berulang
- Catat istilah yang tidak familiar
- Catat placeholder/markup yang ada

**Tools:**
- Buka file di VS Code dengan extension **XML Tools**
- Buka [Character Bible](./03-character-bible.md) di tab terpisah
- Buka [Glossary Master](./02-glossary-master.md) di tab terpisah

### Step 5: Riset Terminologi

Untuk setiap istilah/karakter yang baru:

1. **Cek glossary master** dan sub-glossary
2. **Cek character bible** untuk voice karakter
3. **Cek religious terms** untuk istilah religi
4. **Cek historical context** untuk istilah era

Jika belum ada:
- Wiki KCD: https://kingdom-come-deliverance.fandom.com/
- Cek bahasa Ceko asli (`reference/czech/` kalau tersedia)
- Cek konteks dialog sekitarnya
- Kalau masih ragu → **buka issue diskusi**

### Step 6: Terjemahkan

**Aturan teknis WAJIB** (lihat [XML Technical](./08-xml-technical.md)):

- ❌ JANGAN ubah struktur XML (`<Row>`, `<Cell>`, atribut)
- ❌ JANGAN ubah/hapus ID string (Cell #1)
- ❌ JANGAN ubah Cell #2 (English reference)
- ❌ JANGAN ubah/hapus placeholder:
  - `%s`, `%d`
  - `{0}`, `{1}`
  - `$keyname;` (key bindings)
  - `[muttering]`, `[riposte]`, dll (state tags)
- ❌ JANGAN ubah karakter escape (`&amp;`, `&lt;`, `&gt;`)
- ❌ JANGAN ubah markup (`<br/>`, `<font>`, `<img>`, dll)
- ✅ HANYA ubah teks bahasa Inggris di **Cell #3** (kolom paling kanan)

**Aturan linguistik:**

- Ikuti [Style Guide](./01-style-guide.md)
- Konsultasi glossary untuk konsistensi
- Sesuaikan dengan voice karakter (jika dialog)

**Tips Workflow:**

1. **Terjemahkan baris per baris** dari atas
2. **JANGAN skip** baris — terjemahkan secara berurutan
3. Kalau ragu: tinggalkan komentar XML (`<!-- TBD: discuss -->`) tapi JANGAN commit dengan komentar
4. Setiap 50 baris: save & cek format XML masih valid
5. Setiap istilah baru: **langsung tambahkan ke glossary** (jangan ditunda)

### Step 7: Update Glossary

Saat menerjemahkan, jika menemukan:

**Karakter baru** → update [characters.md](../glossaries/characters.md)
- Format: `Nama Asli | Indonesia | Peran | Catatan`

**Tempat baru** → update [places.md](../glossaries/places.md)

**Item baru** → update [items.md](../glossaries/items.md)

**Gelar/sapaan baru** → update [titles-honorifics.md](../glossaries/titles-honorifics.md)

**UI term baru** → update [ui-terms.md](../glossaries/ui-terms.md)

**Perk/buff baru** → update [perks-buffs.md](../glossaries/perks-buffs.md)

**Istilah religius baru** → update [religious-terms.md](./04-religious-terms.md)

**Commit terpisah** dengan tipe `glossary`:
```
glossary(items): tambah 5 jenis senjata Cuman

- Cuman saber: Sabel Cuman
- Cuman composite bow: Busur Komposit Cuman
- ...
```

### Step 8: Self-Review (QA Checklist)

**WAJIB** lolos [QA Checklist](./07-qa-checklist.md) — semua poin tercentang ✅.

Kalau ada poin yang gagal:
- Stop dulu
- Perbaiki
- Re-run checklist
- Ulangi sampai semua ✅

### Step 9: Commit

**Format commit message:**

```
<tipe>(<file>): <ringkasan singkat>

<deskripsi opsional, bullet points>

Refs: <links>
```

**Contoh nyata:**

```
translate(text_ui_HUD): selesaikan 2 string HUD elements

- "Drop body" → "Letakkan jasad"
- "Pick up body" → "Angkat jasad"
- Konsisten dengan style guide v1.0
- Tidak ada glossary update (vocabulary sederhana)

Refs: progress.md
```

**Tipe commit (sudah dibahas di CONTRIBUTING.md):**

| Tipe | Penggunaan |
|------|-----------|
| `translate` | Terjemahan baru |
| `revise` | Perbaikan terjemahan |
| `glossary` | Update glossary |
| `docs` | Perbaikan dokumentasi |
| `fix` | Perbaikan bug/typo |
| `style` | Formatting (bukan konten) |
| `chore` | Housekeeping |

**Git command line:**

```bash
git add translation/indonesian/text_ui_HUD.xml
git commit -m "$(cat <<'EOF'
translate(text_ui_HUD): selesaikan 2 string HUD elements

- "Drop body" → "Letakkan jasad"
- "Pick up body" → "Angkat jasad"
- Konsisten dengan style guide v1.0

Refs: progress.md
EOF
)"
```

**Via VS Code:**
- Source Control panel
- Stage file
- Tulis message di kotak (single line dulu, body di baris baru)
- Commit (✓)

### Step 10: Update Progress

1. Buka `progress.md`
2. Ubah status file ke:
   - 🟦 (selesai, menunggu review) — jika kolaborasi
   - 🟩 (selesai & ter-review) — jika solo
3. Isi nama translator dan tanggal selesai
4. Update statistik total
5. Commit: `docs(progress): mark text_ui_HUD.xml as complete`

### Step 11: Push & PR (Kolaborasi)

```bash
git push -u origin translate/text_ui_HUD
```

Buat PR:
- Template otomatis terisi
- Centang semua poin
- Request review
- Tunggu approve
- Merge

---

## Strategi per File (Sesuai Kompleksitas)

### File Sangat Kecil (text_ui_HUD.xml, text_rich_presence.xml)

**Estimasi: 5–15 menit per file**

- Langsung terjemahkan baris per baris
- Tidak perlu split

### File Kecil–Sedang (text_ui_minigames.xml, text_ui_misc.xml)

**Estimasi: 1–3 jam per file**

- Read-through dulu (10 menit)
- Identifikasi terminologi khusus
- Terjemahkan
- Self-review

### File Menengah (text_ui_tutorials.xml, text_ui_ingame.xml, text_ui_soul.xml)

**Estimasi: 5–15 jam per file**

- Skip 396 backer names di text_ui_ingame.xml (copy Cell #2 ke Cell #3)
- Banyak istilah skill/perk — konsultasi glossary intensif
- Terjemahkan dalam beberapa sesi
- Self-review per session

### File Besar (text_ui_menus.xml, text_ui_items.xml)

**Estimasi: 30–60 jam per file**

- WAJIB split sesi (jangan satu hari)
- Save & commit per 100 baris
- text_ui_items.xml ada book contents — strategi terjemahan terpisah untuk text arkais

### File Mega (text_ui_quest.xml)

**Estimasi: 80–120 jam**

- Split per chapter/quest
- Cross-reference dengan main story
- Konsultasi character bible intensif

### File Mega-Mega (text_ui_dialog.xml — 65K rows)

**Estimasi: 500+ jam (proyek multi-bulan)**

Strategi terbaik:
1. **Split per chapter** (chap0, chap1, chap5, chap12, dst)
2. **Split per karakter** (semua dialog Henry dulu, lalu Sir Radzig, dst)
3. **Atau split per scene** (satu dialog tree sekali)
4. **Multi-translator** wajib (1 orang tidak realistis)
5. **Review berlapis** — translator + reviewer + LQA

---

## Branch Naming (Kolaborasi)

```
translate/text_ui_HUD              ← terjemahan baru
revise/text_ui_HUD-fix-bleeding    ← perbaikan
glossary/add-religious-terms       ← update glossary
docs/update-style-guide            ← dokumentasi
fix/typo-dialog-line-5234          ← typo fix
chore/cleanup-trailing-whitespace  ← housekeeping
```

---

## Konflik & Merge

Jika kerja kolaboratif:

1. **Selalu pull sebelum commit baru**:
   ```bash
   git pull origin main
   ```

2. **Resolve konflik** dengan hati-hati di XML:
   - JANGAN auto-merge XML — review manual
   - Cek struktur tidak rusak

3. **Conflict di glossary** → diskusi tim, jangan auto-resolve

---

## Eskalasi & Diskusi

**JANGAN putuskan sendiri kalau:**

- Istilah baru yang impactful (gelar penting, konsep religius)
- Voice karakter ambigu
- Perubahan style guide
- Terjemahan punya >2 alternatif valid yang sama-sama bagus

**Cara eskalasi:**

1. Buka issue dengan label `discussion`
2. Sertakan:
   - Konteks (file & baris)
   - Original English
   - Alternatif terjemahan yang dipertimbangkan
   - Argumen pro/kontra
3. Tag reviewer / maintainer
4. Tunggu minimal 24 jam untuk respons
5. Setelah konsensus → update glossary, lanjut terjemahkan

---

## Tools yang Direkomendasikan

### Wajib

- **VS Code** dengan extension:
  - **XML Tools** (Josh Johnson) — auto-format, validate
  - **GitLens** — git insights
  - **Markdown All in One** — for editing docs

### Berguna

- **DeepL** (https://deepl.com) — quick draft (TIDAK untuk final!)
- **Google Translate** — quick comparison (TIDAK untuk final!)
- **KCD Wiki** — context research

### Untuk Pack ke .pak (Final)

- **7-Zip** — pack XML back to .pak
- **Test in-game** — load translation & cek
