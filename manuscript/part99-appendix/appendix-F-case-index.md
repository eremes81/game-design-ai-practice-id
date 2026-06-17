# Lampiran F. Indeks Kasus (Perusahaan / PC Pribadi)

> Mengindeks kasus-kasus yang muncul dalam buku ini berdasarkan lingkungan perusahaan vs lingkungan PC pribadi. Materi ini membantu pembaca dengan cepat menemukan kasus yang paling dekat dengan lingkungan mereka sendiri.

---

## F.1 Kasus Lingkungan Perusahaan (Pengembang MMORPG A, Proyek A)

### F.1.1 Kasus Sistem

| Kasus | Lokasi Kemunculan |
|---|---|
| Operasional CombatBalance·CombatFormula | 8.1 |
| Economy Machinations Pilot | 8.2 |
| Damage Simulator (2008\~) | 8.3 |
| Procedural Level Design Master | 7.1 |
| Editor BehaviorTree | 7.2 |
| Pustaka pola dungeon·field | 7.3 |
| HUD Layout v3 | 9.1 |
| Keputusan Skill UI 6 kolom | 9.2 |
| NarrativeDocs 5 lapisan | 5.1 |
| voice_profile + voice_lint | 5.2·5.4 |
| proj_city_hunting_generator | 6.2 |
| NPC Persona/Squad | 6.3 |

### F.1.2 Kasus Operasional

| Kasus | Lokasi Kemunculan |
|---|---|
| Operasional 95_BattleTF | 16.1 |
| Kolaborasi 97_DevGuide | 16.2 |
| Sistem notula 17.x | Seluruh Bagian 17 |
| Alpha Gap Report | 10.3 |
| decision_validation 3-layer | 10.2 |
| Operasional 304 atom | 20.1 |
| Memori anggota tim | 20.2 |
| Portal web | 20.3 |

### F.1.3 Kasus Organisasi

| Kasus | Lokasi Kemunculan |
|---|---|
| Visi·peta jalan tim skala menengah (10\~50 orang) | 19.1 |
| Pendelegasian oleh Design Director | 19.2 |
| Manajemen konflik·budaya tim | 19.3 |
| Pengelolaan rapat (dari sudut pandang pemimpin) | 19.4 |
| Komunikasi ke atas (PD/CEO) | 19.5 |
| Strategi adopsi AI | 19.6 |
| Tata kelola (prompt·halusinasi·biaya·hukum·etika) | Seluruh Bagian 22 |

---

## F.2 Kasus Lingkungan PC Pribadi

Kasus yang penulis alami langsung di lingkungan PC pribadi (rumah).

### F.2.1 Peminjaman Alat

| Kasus | Lokasi Kemunculan |
|---|---|
| Peminjaman 6 alat seperti excel-reader | Lampiran B |
| Sistem injeksi JIT atom | (Infrastruktur PC pribadi) |
| Slash command PC pribadi (book-capture dll.) | (Infrastruktur PC pribadi) |

### F.2.2 Penulisan Buku Itu Sendiri

Proses penulisan buku ini sendiri merupakan kasus pemanfaatan AI.

| Area | Penerapan |
|---|---|
| Produksi massal isi bab | LLM (Claude) |
| Perlindungan IP (perusahaan → anonimisasi) | grep watchlist + aturan |
| Pelacakan sumber | Dicantumkan saat mengutip lingkungan perusahaan |
| Siklus produksi massal → tinjauan → pembenahan | Masuk mode tinjauan setelah produksi massal bulan Mei |

---

## F.3 Panduan Pemanfaatan Kasus

### F.3.1 Pembaca Lingkungan Perusahaan

Kasus lingkungan perusahaan (tim skala menengah 10\~50 orang, MMORPG, Live Ops) dapat diterapkan pada perusahaan dengan skala·domain serupa.

| Lingkungan Pembaca | Kasus yang Sesuai |
|---|---|
| Pengembang MMORPG mobile | Hampir semua kasus |
| MMORPG PC | Sesuaikan kasus mobile pada Bagian 14 |
| Game indie | Terapkan secara diperkecil untuk kasus skala menengah (10\~50 orang) ke atas |
| Game Live Ops | Bagian 15 + kasus operasional |

### F.3.2 Pembaca Lingkungan Pribadi

Lingkungan pribadi (1\~2 orang, atau hobi) meminjam kasus perusahaan dengan menyederhanakannya.

| Area | Penyederhanaan |
|---|---|
| Sistem rapat | Tidak diperlukan untuk solo. Cukup catatan sendiri |
| Operasional TF | Tidak diperlukan untuk solo |
| Decision card | Hanya keputusan besar |
| atom·wikilink | Manfaatkan secara aktif (bernilai bahkan untuk solo) |

---

## F.4 Penanganan IP saat Mengutip Kasus

Semua kasus perusahaan dalam buku ini dianonimkan.

| Asli | Anonimisasi |
|---|---|
| Nama perusahaan | Pengembang MMORPG A |
| Proyek | Proyek A |
| Nama asli anggota tim | Anggota tim A·B·C |
| Nama unik dalam game | Direkayasa (Kerajaan X, Karakter K_001, dll.) |
| Angka | Direkayasa (rasionya nyata) |
| Nama alat perusahaan | proj_* (mis. proj_city_hunting_generator) |

---

## F.5 Indeks Pekerjaan Non-Game — Menelusuri Kotak "Penerapan di Luar Game"

> Indeks balik bagi pembaca yang bekerja di luar game (perancang·PM·pekerja kantoran umum). Kotak "Penerapan di Luar Game" di akhir setiap bab pada isi utama adalah jembatan untuk membaca alur kerja bab tersebut dengan memindahkannya ke pekerjaan yang tidak terkait dengan game. Jika isi domain game terasa berat, Anda boleh membuka dahulu kotak-kotak di bawah ini dan masuk melalui kasus pekerjaan Anda sendiri. Indeks ini adalah jangkar bagi "Jalur Pekerjaan Umum" (Bagian 1·2 → 17 → 16 → 18 → 21·22) dan Kursus Kilat 90 Menit (17.1 → 16.2 → 22.1 → 21.1).

### F.5.1 Proses·Kolaborasi (Transfer ke luar game paling langsung)

| Bab | Pekerjaan yang Dialihkan oleh "Penerapan di Luar Game" |
|---|---|
| 16.1 | Mengisolasi pekerjaan yang membanjir ke ruang kerja sementara, lalu menyerap hanya hasilnya sebagai versi resmi |
| 16.2 | Mengklasifikasikan satu permintaan satu baris ke dalam tiga jalur: kesepakatan·cacat·jadwal |
| 16.3 | Membingkai keluaran ke dalam medium yang sesuai untuk lintas-bidang·pemangku kepentingan |
| 17.1 | Membuat notula mengalir ke dalam 4 bidang keputusan (apa·siapa·mengapa·berikutnya) |
| 17.2 | Pipeline ekstraksi keputusan·tindakan dari notula |
| 17.3 | Klasifikasi·sinkronisasi keputusan rapat |
| 17.4 | Otomatisasi ringkasan rapat·pelacakan tindak lanjut |
| 18.1 | Memasukkan alamat permanen·penanggung jawab·dasar pada keputusan, dan mencari keputusan lampau terlebih dahulu |
| 18.2 | Klasifikasi dampak — sejauh mana satu keputusan berpengaruh |
| 18.3 | Alur kerja pelacakan sebelum dan sesudah perubahan |
| 18.4 | Memastikan cakupan dampak perubahan dokumen melalui pencarian |

### F.5.2 Perbaikan Diri·Tata Kelola

| Bab | Pekerjaan yang Dialihkan oleh "Penerapan di Luar Game" |
|---|---|
| 21.1 | Menjadikan retrospektif sebagai titik awal perbaikan diri |
| 21.2 | Mempromosikan pola berulang dari retrospektif menjadi aturan |
| 21.3 | Menutup loop perbaikan |
| 22.1 | Memasukkan konteks·format·penangkal halusinasi·verifikasi ke dalam satu lembar surat perintah kerja (prompt) |
| 22.2 | Pertahanan berlapis terhadap halusinasi·keselamatan |
| 22.3 | Mengelola biaya AI secara jujur |
| 22.4 | Pemeriksaan hak cipta·etika |

### F.5.3 Kepemimpinan

| Bab | Pekerjaan yang Dialihkan oleh "Penerapan di Luar Game" |
|---|---|
| 19.1 | Penyampaian visi dan pendelegasian |
| 19.2 | Manajemen konflik dan kepemimpinan rapat |
| 19.3 | Strategi adopsi AI organisasi |

> Indeks di atas hanya menghimpun kotak "Penerapan di Luar Game" yang benar-benar ada di isi utama (22 kotak per Juni 2026). Bab yang tidak memiliki kotak adalah bab dengan ketergantungan domain game yang tinggi sehingga sulit ditransfer apa adanya; alih-alih memaksakan pemindahan, kami menyarankan Anda masuk melalui bab-bab di atas pada "Jalur Pekerjaan Umum".
