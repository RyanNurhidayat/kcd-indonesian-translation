# Kingdom Come: Deliverance — Terjemahan Bahasa Indonesia

Fan translation proyek untuk **Kingdom Come: Deliverance** (Warhorse Studios, 2018) dari bahasa Inggris ke Bahasa Indonesia, dikerjakan dengan standar lokalisasi game profesional.

## Skala Proyek

| Metrik | Jumlah |
|--------|-------:|
| Total file XML | 11 |
| Total string | **81,033** |
| Backer names (tidak diterjemahkan) | 396 |
| String efektif untuk diterjemahkan | **~80,637** |
| Karakter NPC teridentifikasi | 50+ |
| Lokasi unik | 20+ |

### Distribusi per File

| File | Rows | % | Kategori |
|------|------:|----:|----------|
| text_ui_dialog.xml | 65,982 | 81.4% | Dialog karakter |
| text_ui_quest.xml | 6,292 | 7.8% | Quest descriptions |
| text_ui_menus.xml | 3,074 | 3.8% | UI menu & tooltip |
| text_ui_items.xml | 2,638 | 3.3% | Item names + book contents |
| text_ui_soul.xml | 1,824 | 2.3% | Skills, perks, buffs |
| text_ui_ingame.xml | 781 | 1.0% | UI in-game + backer names |
| text_ui_tutorials.xml | 149 | 0.2% | Tutorial dengan keybinds |
| text_ui_misc.xml | 148 | 0.2% | Game over + DLC summary |
| text_ui_minigames.xml | 131 | 0.2% | From the Ashes DLC |
| text_rich_presence.xml | 12 | 0.0% | Discord/Xbox status |
| text_ui_HUD.xml | 2 | 0.0% | HUD elements |

## Struktur Repository

```
.
├── source/english/              File XML asli Inggris (referensi, jangan diubah)
├── translation/indonesian/      Hasil terjemahan
├── reference/czech/             File Ceko untuk cross-check (opsional)
├── docs/                        Dokumentasi gaya, glosarium, workflow
├── glossaries/                  Glosarium per kategori
└── .github/                     Templates untuk issue & PR
```

## Status Proyek

🚧 **Work in Progress** — Setup awal selesai, terjemahan belum dimulai.

Lihat **[progress.md](./progress.md)** untuk tracking per file.

## 📖 Dokumentasi (WAJIB DIBACA)

Sebelum berkontribusi, **WAJIB** baca berurutan:

1. **[Style Guide](./docs/01-style-guide.md)** — Pedoman gaya bahasa, register, T-V distinction
2. **[Glossary Master](./docs/02-glossary-master.md)** — Hub glosarium
3. **[Character Bible](./docs/03-character-bible.md)** — Voice tiap karakter NPC
4. **[Religious Terms](./docs/04-religious-terms.md)** — Terminologi Katolik abad ke-15
5. **[Historical Context](./docs/05-historical-context.md)** — Konteks Bohemia 1403
6. **[Workflow](./docs/06-workflow.md)** — Proses kerja end-to-end
7. **[QA Checklist](./docs/07-qa-checklist.md)** — Checklist wajib sebelum commit
8. **[XML Technical](./docs/08-xml-technical.md)** — Detail teknis XML KCD (placeholders, markup)

## Glossaries

- [Characters](./glossaries/characters.md) — Nama NPC
- [Places](./glossaries/places.md) — Nama tempat
- [Items](./glossaries/items.md) — Senjata, armor, makanan, ramuan
- [Titles & Honorifics](./glossaries/titles-honorifics.md) — Gelar & sapaan
- [UI Terms](./glossaries/ui-terms.md) — Istilah antarmuka
- [Perks & Buffs](./glossaries/perks-buffs.md) — Skill, perk, status efek

## Kontribusi

Lihat **[CONTRIBUTING.md](./CONTRIBUTING.md)**.

## Disclaimer & Lisensi

Ini adalah **fan translation non-komersial**:

- Aset asli (teks, dialog, nama, karakter, dunia) © **Warhorse Studios** & **Deep Silver**
- Proyek ini TIDAK mendistribusikan file game — hanya file teks XML yang dimodifikasi
- Hasil terjemahan (kontribusi original) berlisensi **Creative Commons BY-NC 4.0**
- Lihat **[LICENSE](./LICENSE)**

Proyek ini **tidak berafiliasi** dengan Warhorse Studios atau Deep Silver. Kingdom Come: Deliverance adalah merek dagang terdaftar Warhorse Studios a.s.

## Link Berguna

- [Kingdom Come: Deliverance — Official](https://kingdomcomerpg.com/)
- [Warhorse Studios](https://warhorsestudios.cz/)
- [KCD Wiki (Fandom)](https://kingdom-come-deliverance.fandom.com/)
- [Nexus Mods — KCD](https://www.nexusmods.com/kingdomcomedeliverance)
