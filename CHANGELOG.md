# Changelog

Semua perubahan signifikan didokumentasikan di sini.

Format mengikuti [Keep a Changelog](https://keepachangelog.com/id-ID/1.1.0/),
dan proyek ini menggunakan [Semantic Versioning](https://semver.org/lang/id/).

## [Unreleased]

### Added
- Skeleton lengkap untuk semua dokumentasi
- Glosarium awal berdasarkan analisis konten aktual

## [0.1.0] - 2026-05-27

### Added
- Inisialisasi repository
- File XML asli Inggris (referensi) di `source/english/` (11 files, 81,033 strings)
- README dengan statistik proyek
- Struktur folder standar (source/, translation/, reference/, docs/, glossaries/)
- Konfigurasi `.gitignore`, `.gitattributes`, `.editorconfig`
- Lisensi CC BY-NC 4.0 untuk kontribusi original
- Disclaimer copyright untuk aset Warhorse Studios
- Dokumentasi lengkap (style guide, glossary master, character bible, religious terms, historical context, workflow, QA checklist, XML technical)
- Sub-glosarium per kategori (characters, places, items, titles-honorifics, ui-terms, perks-buffs)
- Template GitHub (PR, issues)
- Tracking progress di `progress.md`

### Analyzed
- Total string: 81,033 (efektif ~80,637 setelah dikurangi 396 backer names)
- 50+ karakter NPC teridentifikasi dari dialog ID encoding
- 20+ lokasi unik dengan spelling variants
- 26 keybinding placeholders (`$keyname;` format)
- 4 jenis placeholder: `%s`, `{0}`, `$name;`, `[tag]`
- 2 tingkat HTML escape (single `&lt;` dan double `&amp;lt;`)
- 10+ jenis markup tag yang harus dipertahankan
