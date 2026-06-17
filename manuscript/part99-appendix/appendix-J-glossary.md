---
title: "Lampiran J. Daftar Singkatan dan Istilah"
appendix: J
status: v3
written: 2026-06-06
author: 이민수
version: v3
---

# Lampiran J. Daftar Singkatan dan Istilah

Saya mengumpulkan di satu tempat semua singkatan yang muncul di buku ini beserta istilah khas buku ini. Di dalam teks, setiap singkatan dijelaskan satu kali pada saat pertama kali muncul, tetapi jika Anda tidak membaca buku secara berurutan atau lupa di tengah jalan, Anda bisa langsung mencarinya di sini. Bila satu singkatan memiliki arti berbeda tergantung konteks, kedua artinya saya cantumkan.

Daftar istilah ini saya kelompokkan dengan urutan berikut. Tingkat ukuran tim → dokumen desain game → domain game → data dan operasional → AI dan alat → standar UI dan aksesibilitas → file dan format. Jika Anda lebih dulu membayangkan sifat singkatan yang dicari, Anda bisa mempersempit kelompok tempatnya berada. Misalnya, `DPS` dan `TTK` ada di "domain game", `KPI` dan `DAU` di "data dan operasional", sedangkan `atom` dan `JIT` di kelompok "AI dan alat".

Aturan penulisannya ada tiga. ① Singkatan umum saya cantumkan bersama nama resmi dan artinya dalam Bahasa Indonesia. ② Istilah yang hanya dipakai di buku ini seperti `atom` dan `Wrapper`, pada kolom nama resmi saya tandai dengan "(istilah khas buku ini)". ③ Untuk singkatan yang memiliki dua arti seperti `PK` (Player Kill dalam konteks perang ↔ Primary Key dalam konteks data), teks menyebutkan yang mana saat pertama kali muncul, sedangkan pada tabel ini saya muat kedua artinya.

## Tingkat Ukuran Tim

Buku ini tidak mematok jumlah anggota tim pada angka tertentu, melainkan menyatakannya dalam tiga tingkat berikut. Sebab, teknik yang sama pun kedalaman penerapannya berbeda tergantung ukuran tim.

| Tingkat | Patokan Jumlah | Keterangan |
|---|---|---|
| Skala kecil | \~10 orang | Dari pengembang solo atau hobiis hingga tim beranggota satu digit. Umumnya cukup dengan penerapan tahap 1–2 |
| Skala menengah | 10–50 orang | Rentang tempat tim penulis berada, sumber contoh-contoh operasional di buku ini. Skala saat efek kumulatif dari standardisasi dan otomatisasi konsistensi mulai terlihat jelas |
| Skala besar | 100+ | Banyak bagian, banyak tim. Skala yang membenarkan adanya infrastruktur khusus dan operasional yang ditangani tim tersendiri |

Tempat di mana teks menuliskan tingkat beserta rentang jumlah, seperti "tim skala menengah (10–50 orang)", mengacu pada tabel ini. Pada bagian di mana jumlah anggotanya sendiri bermakna, seperti pengembangan satu orang atau seorang diri, saya menulis angka pastinya langsung, bukan tingkatnya.

## Dokumen Desain Game

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| GDD | Game Design Document | Dokumen desain game. Spesifikasi rinci yang menetapkan sistem, nilai numerik, dan perilaku |
| CDD | Concept Design Document | Dokumen desain konsep. Dokumen desain awal tahap sebelum GDD (arah dan konsep) |
| TF | TaskForce | Tim khusus yang dikumpulkan sementara untuk tujuan jangka pendek (misalnya TF tempur) |
| DD | Design Director | Direktur desain. Peran pemimpin yang mengoordinasikan arah perancangan game secara menyeluruh |
| RnD | Research and Development | Riset dan pengembangan. Tahap atau organisasi yang mengeksplorasi prototipe dan teknik baru (misalnya RnD procedural generation) |

## Domain Game

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| NPC | Non-Player Character | Karakter yang tidak dikendalikan oleh pemain |
| HUD | Heads-Up Display | Informasi status yang ditumpangkan di layar game (HP, minimap, dan sebagainya) |
| DPS | Damage Per Second | Jumlah kerusakan per detik |
| GCD | Global Cooldown | Cooldown global. Waktu tunggu bersama saat satu skill dipakai, semua skill ikut terkunci sejenak |
| TTK | Time To Kill | Waktu yang dibutuhkan untuk menjatuhkan sasaran |
| PK | Player Kill | (konteks perang/PvP) Pertarungan atau pembunuhan antarpemain |
| BT | BehaviorTree | Behavior Tree. Struktur yang mendefinisikan percabangan perilaku AI NPC dalam bentuk pohon |
| FSM | Finite State Machine | Mesin keadaan terbatas. Model yang mendefinisikan perilaku melalui keadaan dan transisi |
| PCG | Procedural Content Generation | Pembangkitan konten prosedural. Membangkitkan konten secara otomatis dengan aturan dan algoritma |
| VFX | Visual Effects | Efek visual |
| SFX | Sound Effects | Efek suara |
| VA | Voice Actor | Pengisi suara |
| RPG / MMORPG | (Massively Multiplayer Online) Role-Playing Game | Game peran (role-playing) / RPG daring multipemain masif |
| P2W / P2E | Pay To Win / Play To Earn | Struktur yang membuat kuat lewat pembayaran / struktur yang menghasilkan pendapatan lewat bermain |
| RMT | Real Money Trading | Jual beli mata uang game dengan uang sungguhan |

## Data dan Operasional

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| KPI | Key Performance Indicator | Indikator kinerja utama |
| DAU | Daily Active Users | Jumlah pengguna aktif harian |
| FK | Foreign Key | Kunci asing. Kolom yang menunjuk ke kunci primer (primary key) sheet lain |
| PK | Primary Key | (konteks data) Kunci primer. Kolom yang mengidentifikasi setiap baris secara unik |
| ROI | Return on Investment | Hasil terhadap investasi (pengembalian) |
| MECE | Mutually Exclusive, Collectively Exhaustive | Saling lepas dan menyeluruh. Prinsip klasifikasi yang membagi tanpa tumpang tindih dan tanpa ada yang terlewat |
| STT | Speech-to-Text | Mengubah suara menjadi teks |
| VBA | Visual Basic for Applications | Bahasa makro yang tertanam di Excel |
| SVN | Subversion | Sistem manajemen versi file |
| telemetry | (data pengukuran) | Log dan metrik permainan yang dikumpulkan otomatis dari build dan eksekusi game (input, tempur, churn, dan sebagainya). Dibaca "telemetri" |

## AI dan Alat

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| AI | Artificial Intelligence | Kecerdasan buatan |
| LLM | Large Language Model | Model bahasa besar (dasar dari ChatGPT, Claude, dan sebagainya) |
| JIT | Just-In-Time | Cara menyisipkan sesuatu hanya pada saat dibutuhkan (di buku ini, penyuntikan otomatis ingatan yang sesuai dengan input) |
| MCP | Model Context Protocol | Standar untuk menghubungkan alat AI dengan layanan eksternal |
| API | Application Programming Interface | Aturan pemanggilan antarprogram |
| UE | Unreal Engine | Unreal Engine |
| atom | (istilah khas buku ini) | Kartu keputusan/aturan yang dibakukan dengan format 1 keputusan = 1 file |
| Wrapper / Cascade / Junction | (istilah khas buku ini) | Titik masuk alat yang sering dipakai / alat yang menggabungkan beberapa pemeriksaan sekaligus / tautan simbolis yang menghubungkan ke badan utama |
| rg | ripgrep | Perintah pencarian teks cepat (alat CLI pengganti grep). Dipakai untuk pencarian menyeluruh pada kode dan dokumen |
| ClickUp | (pelacak tugas/isu) | Alat kolaborasi cloud yang mengelola pekerjaan dan jadwal. JIRA, Redmine, dan Linear termasuk kategori yang sama. Dihubungkan lewat MCP agar AI dapat membaca dan memperbaruinya |

## Standar UI dan Aksesibilitas

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| UI / UX | User Interface / User Experience | Antarmuka pengguna / pengalaman pengguna |
| WCAG | Web Content Accessibility Guidelines | Pedoman aksesibilitas web (ambang batas seperti rasio kontras dan ukuran target sentuh) |
| HIG | (Apple) Human Interface Guidelines | Pedoman antarmuka dari Apple |
| SC | Success Criterion | Nomor kriteria lulus individual pada WCAG (misalnya SC 1.4.3) |
| pt / dp / px | point / density-independent pixel / pixel | Satuan ukuran layar |

## File dan Format

| Singkatan | Nama Resmi | Arti |
|---|---|---|
| YAML | YAML Ain't Markup Language | Format penulisan konfigurasi dan data yang mudah dibaca manusia |
| JSON | JavaScript Object Notation | Format penulisan untuk pertukaran data |
| HTML / SVG | HyperText Markup Language / Scalable Vector Graphics | Dokumen web / format grafik vektor |
| GLB | GL Transmission Format (Binary) | Format file biner model 3D |

---

*Singkatan yang artinya bercabang tergantung konteks, seperti PK, disebutkan yang mana saat pertama kali muncul di teks. Jika ragu, Anda bisa kembali ke tabel ini.*
