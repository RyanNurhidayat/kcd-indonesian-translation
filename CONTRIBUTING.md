# Panduan Kontribusi

Terima kasih atas minat untuk berkontribusi! Proyek ini menggunakan standar lokalisasi game profesional.

## Persiapan

**WAJIB BACA** dokumen berikut secara berurutan sebelum kontribusi pertama:

1. [Style Guide](./docs/01-style-guide.md)
2. [Glossary Master](./docs/02-glossary-master.md)
3. [Character Bible](./docs/03-character-bible.md)
4. [Religious Terms](./docs/04-religious-terms.md)
5. [Historical Context](./docs/05-historical-context.md)
6. [Workflow](./docs/06-workflow.md)
7. [QA Checklist](./docs/07-qa-checklist.md)
8. [XML Technical Notes](./docs/08-xml-technical.md)

## Alur Kerja Singkat

1. **Pilih file** dari `progress.md` yang belum dikerjakan
2. **Klaim** dengan membuat issue: `WIP: text_ui_X.xml — [Nama]`
3. **Copy** file dari `source/english/` ke `translation/indonesian/`
4. **Terjemahkan** mengikuti style guide & glossary
5. **Self-review** dengan QA checklist
6. **Update** `progress.md` dan glossary jika ada istilah baru
7. **Commit** dengan format standar
8. **Push & PR** dengan template yang disediakan

## Format Commit Message

```
<tipe>(<file>): <ringkasan singkat>

<deskripsi opsional, bullet points>

Refs: <issue/PR/baris terkait>
```

### Tipe Commit

| Tipe | Penggunaan |
|------|-----------|
| `translate` | Terjemahan baru |
| `revise` | Perbaikan terjemahan |
| `glossary` | Update glossary |
| `docs` | Perbaikan dokumentasi |
| `fix` | Perbaikan bug/typo |
| `style` | Perubahan formatting (bukan terjemahan) |
| `chore` | Housekeeping |

### Contoh Commit

```
translate(text_ui_HUD): selesaikan 2 string HUD elements

- "Drop body" → "Letakkan jasad"
- "Pick up body" → "Angkat jasad"
- Konsisten dengan style guide v1.0

Refs: progress.md
```

## Aturan Wajib

### ❌ JANGAN

- Ubah struktur XML (`<Row>`, `<Cell>`, atribut)
- Ubah/hapus ID string (Cell #1)
- Ubah Cell #2 (English reference)
- Hapus placeholder (`%s`, `{0}`, `$keyname;`, `[muttering]`)
- Hapus markup (`&lt;br/&gt;`, `&amp;lt;font...&amp;gt;`)
- Ubah karakter spesial (`&amp;`, `&lt;`, `&gt;`)
- Commit file `.pak`
- Gunakan slang modern ("gue", "lo", "banget", "doang")

### ✅ WAJIB

- Encoding UTF-8
- Line ending LF (auto-handled oleh .gitattributes)
- Konsultasi glossary untuk istilah berulang
- Update progress.md saat menyelesaikan file
- Update glossary saat menemukan istilah baru
- Self-review dengan QA checklist
- Konsisten dengan voice karakter (lihat character bible)

## Branch Naming (multi-translator)

```
translate/text_ui_X
revise/text_ui_X-quest-Y
glossary/add-religious-terms
docs/update-style-guide
fix/typo-text_ui_dialog
```

## PR Process

1. Push branch
2. Buat PR dengan template (otomatis terisi dari `.github/PULL_REQUEST_TEMPLATE.md`)
3. Pastikan semua poin QA checklist tercentang
4. Tunggu review minimal 1 reviewer
5. Setelah approved, squash & merge

## Eskalasi & Diskusi

**JANGAN** putuskan sendiri kalau:

- Istilah baru yang impactful (gelar penting, konsep religius)
- Voice karakter ambigu
- Perubahan style guide
- Terjemahan dengan >2 alternatif valid yang sama-sama bagus

Buka **issue dengan label `discussion`** dulu.

## Pertanyaan & Bantuan

- Issue baru dengan label `question`
- Diskusi terbuka di GitHub Discussions

Selamat berkontribusi! 🎮📜
