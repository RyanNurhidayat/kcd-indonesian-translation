# QA Checklist — Wajib Sebelum Commit

Setiap file terjemahan **WAJIB** lolos checklist ini sebelum di-commit. Tidak ada pengecualian.

---

## ✅ Bagian 1: Teknis XML

### Struktur

- [ ] Tag `<Table>` di awal dan `</Table>` di akhir tetap utuh
- [ ] Setiap `<Row>` memiliki tepat 3 `<Cell>`
- [ ] Tidak ada `<Row>` atau `<Cell>` yang rusak/tidak lengkap
- [ ] Tidak ada Row yang terhapus (jumlah Row sama dengan original)
- [ ] Tidak ada Row yang duplikat

### ID & Cell

- [ ] Cell #1 (ID string) **TIDAK** diubah — sama persis dengan original
- [ ] Cell #2 (English reference) **TIDAK** diubah — sama persis dengan original
- [ ] Cell #3 (Display text) — INI yang diterjemahkan

### Atribut & Karakter Spesial

- [ ] Karakter escape XML masih intact:
  - `&amp;` (untuk `&`)
  - `&lt;` (untuk `<`)
  - `&gt;` (untuk `>`)
  - `&quot;` (untuk `"` dalam atribut)
  - `&apos;` (untuk `'` dalam atribut)
- [ ] **Tidak ada** `&amp;` yang tidak sengaja jadi `&amp;amp;` (double-escape)
- [ ] **Tidak ada** `&lt;` yang tidak sengaja jadi `&amp;lt;` (kecuali memang aslinya double-escape)
- [ ] **Single escape** `&lt;br/&gt;` tetap single
- [ ] **Double escape** `&amp;lt;br/&amp;gt;` tetap double

### Encoding & Formatting

- [ ] **Encoding UTF-8** (cek di status bar VS Code: pojok kanan bawah)
- [ ] Line ending **LF** bukan CRLF (auto-handled oleh `.gitattributes`)
- [ ] Tidak ada trailing whitespace di akhir baris
- [ ] Tidak ada karakter aneh dari copy-paste:
  - Smart quotes `" "` `' '` (kecuali memang ada di original)
  - Em-dash `—`, en-dash `–` (sesuaikan original)
  - Single-char ellipsis `…` (sesuaikan original)
- [ ] File berakhir dengan newline
- [ ] Indentasi konsisten (tab atau space sesuai original)

---

## ✅ Bagian 2: Placeholder & Variabel

### Format String Placeholders

- [ ] Semua `%s`, `%d`, `%i` dipertahankan
- [ ] Urutan placeholder masih sesuai grammar Indonesia
- [ ] Tidak ada placeholder yang terhapus
- [ ] Tidak ada placeholder yang ditambah (kecuali memang perlu di Indonesia)

### Positional Placeholders

- [ ] Semua `{0}`, `{1}`, `{2}` dipertahankan
- [ ] Jika perlu diubah urutan: pastikan engine support reordering

### Keybinding Placeholders (Format `$keyname;`)

- [ ] Semua keybinding dipertahankan **EKSAKT** dengan semicolon di akhir
- [ ] Daftar yang ditemukan di file: lihat [XML Technical](./08-xml-technical.md#keybinding-placeholders)
- [ ] Contoh: `$attack1;`, `$block;`, `$jump;`, `$read_toggle;`, `$lock_dir_fwd;`

### State/Action Tags (Format `[tag]`)

- [ ] Semua dipertahankan: `[muttering]`, `[riposte]`, `[feint]`, `[dodge]`, dll
- [ ] Brackets `[` dan `]` tidak rusak

### Game Variable

- [ ] `[player_name]` dipertahankan jika ada
- [ ] `\n`, `\t`, `\\` dipertahankan jika ada

---

## ✅ Bagian 3: Markup HTML

### Line Break

- [ ] `&lt;br/&gt;` dipertahankan (untuk line break dalam paragraf)
- [ ] `&amp;lt;br/&amp;gt;` (double escape) dipertahankan kalau aslinya begitu
- [ ] `&amp;nbsp;` (non-breaking space) dipertahankan

### Paragraph & Alignment

- [ ] `&amp;lt;p align='center'&amp;gt;...&amp;lt;/p&amp;gt;` struktur utuh
- [ ] `&amp;lt;p align='left'&amp;gt;...&amp;lt;/p&amp;gt;` struktur utuh
- [ ] Buka & tutup tag balanced

### Font Color & Size

- [ ] `&amp;lt;font color='#XXXXXX'&amp;gt;...&amp;lt;/font&amp;gt;` struktur utuh
- [ ] Kode warna **TIDAK** diubah (`#B8AE7E` tetap)
- [ ] `&amp;lt;font size='25'&amp;gt;...&amp;lt;/font&amp;gt;` struktur utuh
- [ ] Hanya teks **di dalam** tag yang diterjemahkan

### Image Embeds

- [ ] `&amp;lt;img src='img://...' /&amp;gt;` tidak diubah sama sekali
- [ ] Path image (`img://Libs/UI/Textures/...`) tetap
- [ ] Atribut `width`, `height`, `vspace`, `align` tetap

### Custom Tags (KCD-specific)

- [ ] `[K]actionname[/K]` (keybinding label) — TEXT di dalam `[K]...[/K]` jangan diterjemahkan, karena itu action name internal
- [ ] `[COLOR=...]...[/COLOR]` — struktur tetap, teks dalam tag boleh diterjemahkan

---

## ✅ Bagian 4: Bahasa & Stilistik

### Sesuai Style Guide

- [ ] Sesuai [Style Guide](./01-style-guide.md) v1.0
- [ ] Register (formal/informal) sesuai konteks
- [ ] Pronomina (engkau/Anda/Tuanku) konsisten dengan konteks

### Sesuai Character Bible

- [ ] Voice karakter sesuai [Character Bible](./03-character-bible.md)
- [ ] Henry adaptif sesuai lawan bicara
- [ ] Bangsawan formal, rakyat membumi
- [ ] Pendeta religius, pemabuk kacau

### Tidak Ada Anachronism

- [ ] **Tidak ada** slang modern: "gue", "lo", "banget", "doang", "sih"
- [ ] **Tidak ada** bahasa SMS: "ga", "udah", "yg", "kayak"
- [ ] **Tidak ada** anglicism: "okay", "fine", "thanks"
- [ ] **Tidak ada** istilah teknologi modern dalam dialog NPC
- [ ] **Tidak ada** referensi budaya yang tidak cocok (ramen, sushi, dll)

### Idiom & Sumpah

- [ ] Idiom diadaptasi natural (tidak literal)
- [ ] Sumpah religius pakai padanan baku ("Demi Tuhan!", "Demi Kristus!")
- [ ] Sapaan religius pakai padanan baku ("Terpujilah Yesus Kristus")

---

## ✅ Bagian 5: Terminologi & Glossary

### Konsistensi Glossary

- [ ] Semua istilah dicek di [Glossary Master](./02-glossary-master.md)
- [ ] Nama karakter sesuai [characters.md](../glossaries/characters.md)
  - Spelling variants di-normalize ke canonical
  - (Lord Divis → Lord Divish)
- [ ] Nama tempat sesuai [places.md](../glossaries/places.md)
- [ ] Nama item sesuai [items.md](../glossaries/items.md)
- [ ] Gelar/sapaan sesuai [titles-honorifics.md](../glossaries/titles-honorifics.md)
- [ ] Terminologi UI sesuai [ui-terms.md](../glossaries/ui-terms.md)
- [ ] Perk/buff sesuai [perks-buffs.md](../glossaries/perks-buffs.md)
- [ ] Istilah religius sesuai [Religious Terms](./04-religious-terms.md)

### Spelling & Variants

- [ ] Variant typo di file asli sudah di-normalize:
  - Lord Divis/Divisch → **Lord Divish**
  - Lord Radziz/Razdig → **Lord Radzig**
  - Brother Nikodem/Nocodemus → **Brother Nicodemus**
  - Captain Robrad → **Captain Robard**
  - King Weceslaus → **King Wenceslas**
  - Samopesch → **Samopesh**

### Istilah Baru

- [ ] Jika ada istilah baru yang tidak di glossary:
  - [ ] Sudah ditambahkan ke glossary yang relevan
  - [ ] Sudah commit terpisah dengan `glossary` type

---

## ✅ Bagian 6: Konteks & Akurasi Historis

- [ ] **Tidak ada anakronisme** (istilah modern di setting 1403)
- [ ] **Akurasi historis** dijaga (gelar feodal, sistem militer)
- [ ] **Akurasi religius** dijaga (Katolik abad ke-15, bukan Protestan)
- [ ] **Referensi geografis** akurat (Bohemia, bukan negara modern)
- [ ] **Mata uang** konsisten: Groschen dipertahankan

---

## ✅ Bagian 7: Penulisan Indonesia

### Ejaan & Tata Bahasa

- [ ] Ejaan sesuai **EYD/PUEBI** terbaru
- [ ] Tidak ada typo
- [ ] Grammar Indonesia natural (subjek-predikat-objek)
- [ ] Tidak ada kalimat yang janggal dibaca keras

### Kapitalisasi

- [ ] Kapital konsisten untuk nama (orang, tempat, faksi)
- [ ] Kapital untuk Tuhan, Kristus, Allah, Bunda Maria, Roh Kudus
- [ ] Kata ganti untuk Tuhan: "Dia", "-Nya" (kapital)
- [ ] Awal kalimat kapital
- [ ] Setelah titik kapital
- [ ] Judul/heading: title case

### Tanda Baca

- [ ] Tanda baca Indonesia (titik, koma, titik koma, tanya, seru)
- [ ] **Tanda kutip**: `"..."` Indonesia (BUKAN smart quotes `"..."`)
- [ ] Em-dash atau hyphen sesuai konteks
- [ ] Ellipsis konsisten dengan original
- [ ] **Tidak ada** double space (dua spasi berturut-turut)
- [ ] **Tidak ada** singkatan informal: "yg", "dlm", "krn"

### Konsistensi Format

- [ ] Angka sesuai aturan (1-9 huruf, ≥10 angka)
- [ ] Tahun dalam format konsisten ("tahun 1403" atau "1403")
- [ ] Mata uang konsisten ("5 groschen", bukan "5 Groschen")

---

## ✅ Bagian 8: Dokumentasi

- [ ] [progress.md](../progress.md) di-update:
  - Status diubah ke 🟦 atau 🟩
  - Nama translator diisi
  - Tanggal selesai diisi
- [ ] Glossary di-update jika ada istilah baru
- [ ] [CHANGELOG.md](../CHANGELOG.md) di-update jika perubahan signifikan

---

## ✅ Bagian 9: Git

- [ ] Hanya file yang relevan yang di-stage
- [ ] **Tidak ada** `.pak` ter-commit
- [ ] **Tidak ada** file `.bak`, `.tmp`, atau backup
- [ ] **Tidak ada** file system (`.DS_Store`, `Thumbs.db`)
- [ ] Commit message sesuai format standar
- [ ] Commit message dalam Bahasa Indonesia atau Inggris konsisten
- [ ] Branch name sesuai konvensi

---

## ✅ Quick Self-Test

Sebelum commit, **tanya diri sendiri:**

1. **Apakah seorang pemain Indonesia bisa membaca ini dan langsung paham?**
   - ✅ Ya → lanjut
   - ❌ Tidak → revisi

2. **Apakah ini terdengar natural kalau dibaca keras?**
   - ✅ Ya → lanjut
   - ❌ Tidak → revisi struktur kalimat

3. **Apakah voice karakter terasa konsisten dengan character bible?**
   - ✅ Ya → lanjut
   - ❌ Tidak → cek character bible, revisi

4. **Apakah saya akan setuju kalau orang lain meng-edit ini sesuai gaya saya?**
   - ✅ Ya → lanjut
   - ❌ Tidak → kemungkinan inkonsisten, revisi

5. **Apakah ini akan tetap bagus dibaca 5 tahun lagi?**
   - ✅ Ya → lanjut
   - ❌ Tidak (terlalu slang/trendy) → revisi

Kalau ada satu jawaban "tidak" → **revisi dulu** sebelum commit.

---

## ✅ Final Check (Sebelum PR)

Setelah commit, sebelum membuka PR:

- [ ] Pull latest dari main branch — pastikan tidak ada konflik
- [ ] Re-run quick check pada file (kalau berbeda hari)
- [ ] Cek diff di GitHub untuk visualisasi perubahan
- [ ] Pastikan PR description lengkap (gunakan template)

---

## Jika Gagal QA

Kalau ada poin yang fail:

1. **JANGAN commit dengan force flag**
2. **Perbaiki** sesuai item yang fail
3. **Re-run QA checklist** dari awal
4. **Hanya commit** setelah semua ✅
5. Jika berulang kali fail di poin yang sama → **buka issue diskusi**

---

## Saran Produktivitas

- Print/save checklist ini → review per file
- Pakai `// TODO` atau komentar XML `<!-- TBD -->` saat ragu, **HAPUS sebelum commit**
- Setiap 30 menit terjemahkan, istirahat 5 menit
- Setiap selesai file: **istirahat dulu**, balik lagi dengan mata segar untuk QA
- 2 sesi review > 1 sesi panjang
