# Lampiran D. Standar Penamaan dan Frontmatter Dokumen R&D

> Versi yang digeneralisasi dari standar penamaan dan frontmatter dokumen R&D Proyek A milik perusahaan (`_NAMING_FRONTMATTER_STANDARD`).

---

## D.1 Standar Penamaan

### D.1.1 atom

```
<category>_<topic>_<subtopic>.md

Contoh:
combat_global_cooldown_constant.md
narrative_voice_profile_K_007.md
ui_button_primary_style.md
```

snake_case. Prefiks kategori.

### D.1.2 Decision Card

```
D<YEAR>_Q<QUARTER>_<NUMBER>.md

Contoh:
D2026_Q2_017.md
```

Tahun, kuartal, nomor.

### D.1.3 Notulen Rapat

```
<category>_<YYYY-MM-DD>[_<seq>].md

Contoh:
95_BattleTF_2026-05-18.md
art_review_2026-05-18_1.md
art_review_2026-05-18_2.md
```

### D.1.4 Spesifikasi

```
spec_<topic>.md

Contoh:
spec_combat_global_cooldown.md
spec_guild_attendance.md
```

### D.1.5 Laporan

```
report_<period>_<type>.md

Contoh:
report_W21_alpha_gap.md
report_Q2_user_voice.md
```

---

## D.2 Standar Frontmatter

### D.2.1 atom

```yaml
---
name: combat_global_cooldown_constant
description: Definisi nilai standar global cooldown sistem combat
type: atom
category: combat
status: active
priority: P0
related_atoms:
  - combat_skill_cooldown_rule
  - combat_healing_skill_cooldown_exception
created: 2026-05-18
last_modified: 2026-05-18
related:
  derives_from: [combat_design_principle]
  affects: [combat_skill_cooldown_rule, ui_skill_cooldown_indicator]
---
```

### D.2.2 Decision Card

```yaml
---
decision_id: D2026_Q2_017
title: Penyeragaman global cooldown combat menjadi 0.5 detik
type: system_change
status: active
created: 2026-05-18
created_by: Anggota Tim A
approved_by: Minsoo Lee
scope:
  - combat_system
affected_atoms: [...]
implementation:
  target_build: 2026-05-18
verification:
  layer_1: passed
  layer_2: passed
  layer_3: pending
---
```

### D.2.3 Notulen Rapat

```yaml
---
type: meeting_note
category: battle
date: 2026-05-18
attendees: [Anggota Tim A, Anggota Tim B, Minsoo Lee]
related_atoms: [...]
---
```

### D.2.4 Spesifikasi

```yaml
---
title: Spesifikasi fitur kehadiran guild
type: spec
priority: P1
target_milestone: MS2
---
```

---

## D.3 Field Wajib vs Opsional

### D.3.1 Field Wajib

| Jenis Dokumen | Wajib |
|---|---|
| atom | name, description, type, category, status |
| Decision Card | decision_id, title, type, status, created, scope |
| Notulen Rapat | type, category, date, attendees |
| Spesifikasi | title, type, priority |

### D.3.2 Field Opsional (lebih baik jika ada)

| Jenis Dokumen | Opsional |
|---|---|
| atom | related, last_modified, priority |
| Decision Card | rationale, related_decisions, verification |
| Notulen Rapat | related_atoms, sub_topic |
| Spesifikasi | target_milestone, related_atoms |

---

## D.4 Pemeriksaan Lint Otomatis

```bash
# frontmatter_lint.py

for file in glob("**/*.md"):
    fm = parse_frontmatter(file)
    if not fm:
        warn(f"{file}: frontmatter tidak ada")
    
    doc_type = infer_type_from_filename(file)
    required = REQUIRED_FIELDS[doc_type]
    
    for field in required:
        if field not in fm:
            warn(f"{file}: field wajib {field} hilang")
```

Dijalankan otomatis saat build. Pelanggaran memicu alert.

---

## D.5 Pencegahan Konflik Penamaan

| Area | Pencegahan |
|---|---|
| atom name | unique secara global |
| Decision ID | unique dalam kuartal |
| Meeting ID | tanggal + seq |
| Nama file | unique dalam folder |

Konflik penamaan diblokir otomatis.

---

## D.6 Prosedur Perubahan

### D.6.1 Mengubah Nama atom

```
1. Buat atom dengan nama baru
2. Perbarui semua wikilink atom lama ke nama baru (otomatis)
3. Tandai atom lama sebagai deprecated + redirect
4. Pindahkan ke _archive setelah 1 bulan
```

Perubahan nama yang terburu-buru berisiko merusak materi.

### D.6.2 Mengubah Standar Frontmatter

```
1. Ajukan alasan perubahan (prosedur decision)
2. Skrip migrasi untuk semua dokumen yang ada
3. Perbarui lint build
4. Beri tahu tim
```

---

## D.7 Catatan untuk Pembaca

Standar ini adalah lingkungan kerja penulis. Pembaca perlu menyesuaikannya dengan lingkungan masing-masing. Intinya:

| Inti | Alasan |
|---|---|
| Konsistensi penamaan | Pencarian, otomatisasi |
| Standar frontmatter | Ramah perkakas |
| Pemisahan wajib dan opsional | Beban penulisan ↓ |
| Lint otomatis | Pemberlakuan standar |
| Prosedur perubahan | Perlindungan materi |
