# Translation Progress

**Total file:** 11  
**Total string:** 81,033  
**Status:** 0/11 selesai (0%)  
**String diterjemahkan:** 0 / ~80,637

## Legenda Status

- ⬜ Belum dimulai
- 🟨 Sedang dikerjakan
- 🟦 Selesai, menunggu review
- 🟩 Selesai & ter-review
- ⛔ Diblokir (ada masalah)

---

## Tahap 1: Kalibrasi (file kecil)

**Tujuan:** Tetapkan gaya, glosarium awal, kalibrasi tone & terminologi.

| Status | File | Rows | Translator | Reviewer | Tanggal Mulai | Tanggal Selesai |
|--------|------|-----:|------------|----------|---------------|-----------------|
| ⬜ | text_ui_HUD.xml | 2 | - | - | - | - |
| ⬜ | text_rich_presence.xml | 12 | - | - | - | - |
| ⬜ | text_ui_minigames.xml | 131 | - | - | - | - |
| ⬜ | text_ui_misc.xml | 148 | - | - | - | - |

---

## Tahap 2: Sistem & UI

**Tujuan:** Selesaikan terminologi UI baku.

| Status | File | Rows | Translator | Reviewer | Tanggal Mulai | Tanggal Selesai |
|--------|------|-----:|------------|----------|---------------|-----------------|
| ⬜ | text_ui_tutorials.xml | 149 | - | - | - | - |
| ⬜ | text_ui_ingame.xml | 781 | - | - | - | - |
| ⬜ | text_ui_soul.xml | 1,824 | - | - | - | - |
| ⬜ | text_ui_menus.xml | 3,074 | - | - | - | - |

**Catatan text_ui_ingame.xml:** 396 dari 781 rows adalah Kickstarter backer names (`cfnm_*`). Backer names **TIDAK diterjemahkan** — hanya copy Cell #2 ke Cell #3. Efektif translation: ~385 rows.

---

## Tahap 3: Konten Game

**Tujuan:** Items, quest descriptions, book contents.

| Status | File | Rows | Translator | Reviewer | Tanggal Mulai | Tanggal Selesai |
|--------|------|-----:|------------|----------|---------------|-----------------|
| ⬜ | text_ui_items.xml | 2,638 | - | - | - | - |
| ⬜ | text_ui_quest.xml | 6,292 | - | - | - | - |

**Catatan text_ui_items.xml:** Berisi item names + deskripsi alchemy + **isi buku in-game** dengan gaya bahasa archaic ("did commit", "did state"). Strategi terjemahan: bedakan item names (literal) vs book content (sastra arkais).

---

## Tahap 4: Mega-Project

**Tujuan:** Dialog karakter (terbesar & paling kompleks).

| Status | File | Rows | Translator | Reviewer | Tanggal Mulai | Tanggal Selesai |
|--------|------|-----:|------------|----------|---------------|-----------------|
| ⬜ | text_ui_dialog.xml | 65,982 | - | - | - | - |

**Catatan text_ui_dialog.xml:**
- 82% dari total string proyek
- ID format encode speaker: `t[N]_s[N]_[N]_[speaker]_[hash]`
- Karakter `_ui` = pilihan dialog player
- WAJIB konsultasi Character Bible untuk voice tiap NPC
- Strategi: split per chapter / per character batch

---

## Statistik Konten

### Karakter NPC (per Character Bible)

- Bangsawan/Ksatria: 25+
- Pendeta/Biarawan: 35+
- Rakyat/Pedagang: 30+
- Generik (guard, soldier, peasant, dll): banyak instances

### Lokasi Disebutkan

- Rattay: 209 mentions
- Talmberg: 192
- Sasau: 189
- Uzhitz: 111
- Merhojed: 98
- Skalitz: 80
- Lainnya: 100+

### Terminologi Teridentifikasi (Per Glossary)

- Senjata: 30+ jenis (lihat [items.md](./glossaries/items.md))
- Armor: 25+ jenis
- Makanan/minuman: 50+ items
- Ramuan/alchemy: 40+ items + 20+ herbs
- Perks/Buffs: 100+ (lihat [perks-buffs.md](./glossaries/perks-buffs.md))
- UI elements: 200+ (lihat [ui-terms.md](./glossaries/ui-terms.md))

---

## Glosarium Progress

| Glossary | Entries Awal | Last Update |
|----------|-------------:|-------------|
| [characters.md](./glossaries/characters.md) | 50+ | 2026-05-27 |
| [places.md](./glossaries/places.md) | 25+ | 2026-05-27 |
| [items.md](./glossaries/items.md) | 100+ | 2026-05-27 |
| [titles-honorifics.md](./glossaries/titles-honorifics.md) | 40+ | 2026-05-27 |
| [ui-terms.md](./glossaries/ui-terms.md) | 100+ | 2026-05-27 |
| [perks-buffs.md](./glossaries/perks-buffs.md) | 50+ | 2026-05-27 |

---

## Catatan Khusus

### Spelling Variants di Game Asli

Ada beberapa typo/variant di file asli Warhorse yang HARUS dinormalisasi:

| Variant | Canonical |
|---------|-----------|
| Lord Divis, Lord Divisch | **Lord Divish** |
| Lord Radziz, Lord Razdig | **Lord Radzig** |
| Brother Nikodem, Brother Nocodemus | **Brother Nicodemus** |
| Captain Robrad | **Captain Robard** |
| King Weceslaus | **King Wenceslas** |
| Samopesch | **Samopesh** |

Selalu pakai versi canonical di terjemahan Indonesia.
