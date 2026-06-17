---
title: "20.4 Manajemen Proyek dengan MCP — Menghubungkan Alat Kolaborasi dan Dokumen ke LLM"
part: 20
chapter: 4
status: v3
version: v3
written: 2026-05-24
author: 이민수
ip_check: done
---

# 20.4 Manajemen Proyek dengan MCP — Menghubungkan Alat Kolaborasi dan Dokumen ke LLM

Selasa, tepat setelah masuk kerja, pukul 9:12. Sebelum bahkan membuka papan (board) alat kolaborasi, saya mengetik satu baris di jendela Claude Code.

```
Tampilkan task P0 yang belum selesai minggu ini, urut dari yang paling dekat tenggatnya
```

Setelah berhenti sekitar 3 detik, jawabannya muncul. Saya tidak membuka alat kolaborasi secara langsung. Saya tidak menelusuri tab dasbor, juga tidak mengirim pesan ke penanggung jawab lewat messenger. Padahal, satu task yang tenggatnya sudah lewat satu hari ternyata tertangkap di paling atas. Barulah setelah itu saya membuka alat kolaborasi dan memeriksa satu kartu itu saja.

Bagaimana 3 detik ini tercipta — itulah keseluruhan bab ini. Intinya adalah bahwa saya tidak mengganti alatnya. Tim Proyek A tetap memakai alat kolaborasi (proyek ini memakai ClickUp — SaaS untuk mengelola task dan jadwal; JIRA, Redmine, dan Linear menempati posisi yang sama). Apa pun alat kolaborasinya, alur bab ini bisa dipindahkan begitu saja hanya dengan mengganti nama alatnya. Sheet data juga tetap ada di SVN, dan decision card (kartu keputusan) juga tetap ada di portal. Yang berubah hanya satu: LLM kini bisa **membuka sendiri** alat-alat itu **dengan tangannya sendiri**. Standar koneksi itulah MCP (Model Context Protocol).

Sebagai perumpamaan, ini bukan soal menambah satu orang resepsionis baru di meja informasi. Ini lebih mirip dengan membukakan kunci ruang arsip yang sudah ada, juga untuk LLM. Ruang arsipnya tetap sama. Hanya saja dibuatkan satu anak kunci tambahan.

---

## 20.4.1 Apa Sebenarnya yang Dihubungkan oleh MCP

MCP adalah protokol standar bagi LLM untuk mengakses alat dan data eksternal. Kata "standar" itulah intinya. Alih-alih membuat adapter terpisah untuk alat kolaborasi, terpisah untuk dokumen, dan terpisah untuk git, di atas satu kesepakatan bernama JSON-RPC setiap alat memaparkan dirinya sebagai "server", dan LLM berbicara ke server itu sebagai "klien".

Strukturnya terdiri dari tiga bagian.

<svg viewBox="0 0 760 220" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="13">
  <rect x="20" y="70" width="180" height="80" rx="8" fill="#e8f0fe" stroke="#3367d6" stroke-width="1.5"/>
  <text x="110" y="100" text-anchor="middle" font-weight="bold">Klien MCP</text>
  <text x="110" y="122" text-anchor="middle">LLM / Pengguna</text>
  <text x="110" y="140" text-anchor="middle" fill="#555">(Claude Code)</text>

  <rect x="300" y="70" width="160" height="80" rx="8" fill="#fef7e0" stroke="#f9a825" stroke-width="1.5"/>
  <text x="380" y="105" text-anchor="middle" font-weight="bold">Protokol</text>
  <text x="380" y="128" text-anchor="middle">JSON-RPC</text>

  <rect x="560" y="30" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="55" text-anchor="middle" font-weight="bold">Server MCP — Alat Kolaborasi</text>
  <text x="650" y="74" text-anchor="middle" fill="#555">Cari·lihat task</text>

  <rect x="560" y="100" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="125" text-anchor="middle" font-weight="bold">Server MCP — Dokumen</text>
  <text x="650" y="144" text-anchor="middle" fill="#555">Lihat decision card·GDD</text>

  <line x1="200" y1="110" x2="300" y2="110" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="100" x2="558" y2="60" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="120" x2="558" y2="128" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <defs><marker id="a" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#666"/></marker></defs>
</svg>

Server memaparkan daftar "hal-hal yang bisa saya lakukan". Untuk server alat kolaborasi, itu berupa fungsi-fungsi seperti `search_tasks`, `get_task`, `update_task`. Klien (LLM) menerima bahasa alami dari pengguna, memilih fungsi yang sesuai untuk dipanggil, lalu menerjemahkan kembali JSON yang dikembalikan menjadi bahasa alami. Ketika saya berkata "Tampilkan task P0", yang dilakukan LLM hanyalah memanggil `search_tasks(priority=P0, status=open)`.

Mari kita perjelas satu hal di sini. Buku ini tidak membahas cara menulis sendiri server MCP. Karena sebagian besar alat seperti ClickUp, JIRA, dan GitHub sudah memiliki server MCP resmi atau komunitas, tugas seorang Game Designer adalah "memasang dan menghubungkan server", bukan "mengimplementasikan protokol". Protokol itu sendiri diumumkan Anthropic sebagai standar terbuka pada November 2024, dan spesifikasinya tersedia secara publik di modelcontextprotocol.io.

---

## 20.4.2 Worked Transcript — Jalan yang Sesungguhnya Dilewati oleh "Tampilkan P0 Minggu Ini"

Kalau hanya dikatakan "ini berjalan otomatis", kesannya seperti sihir. Mari kita ikuti satu kasus nyata sampai tuntas. Berikut adalah salinan hampir apa adanya dari sesi yang pertama kali saya jalankan di Proyek A, tepat setelah memasang MCP alat kolaborasi. Saya membiarkan keluaran mentah (raw output) LLM tanpa diringkas, termasuk bagian-bagian yang janggal.

**① Prompt yang saya ketik (lengkap)**

```
Di ClickUp, rapikan task P0 yang belum selesai dan tenggatnya minggu ini, urut dari yang paling dekat tenggatnya.
Untuk tiap item, sertakan penanggung jawab dan sisa hari menuju tenggat, dan naikkan yang sudah lewat tenggat ke paling atas.
```

**② Keluaran mentah Claude (apa adanya)**

```
Saya menanyakan workspace ClickUp dengan kondisi P0·belum selesai·tenggat minggu ini.
3 item tertangkap. (Yang sudah lewat tenggat saya naikkan ke paling atas.)

1. TASK_017  Perubahan kode global cooldown
   Penanggung jawab: teammate_a / Tenggat: kemarin (−1 hari, lewat)
2. TASK_023  Penerapan voice_lint v2
   Penanggung jawab: teammate_b / Tenggat: besok (+1 hari)
3. TASK_031  Pembaruan skema log pertempuran
   Penanggung jawab: teammate_c / Tenggat: Jumat (+3 hari)

Catatan: TASK_009 (tinjauan tabel balance) tampaknya juga P0,
tetapi karena status-nya 'in review', saya ragu apakah harus dimasukkan ke 'belum selesai'.
Saya tidak menyertakannya — beri tahu saya kriterianya jika diperlukan.
```

Perhatikan titik di mana LLM berhenti dengan sendirinya. `TASK_009` berstatus 'in review', dan apakah itu termasuk "belum selesai", LLM tidak memvonisnya sendiri melainkan balik bertanya kepada manusia. MCP mengambil data secara akurat, tetapi "apakah in review dihitung sebagai belum selesai" adalah persoalan yang bergantung pada definisi tim. Seandainya LLM memutuskan ini sembarangan, justru itulah yang akan menjadi insiden.

**③ Verifikasi dan penolakan yang saya lakukan**

Saya membuka alat kolaborasi dan memeriksa satu kartu TASK_017 saja. Tenggatnya memang benar-benar sudah lewat. Namun menurut kriteria tim kami, TASK_009 yang 'in review' pun dihitung sebagai belum selesai. Klasifikasi LLM berbeda dari aturan kami. Maka saya menolaknya dan memberikan kembali kriterianya.

**④ Permintaan ulang**

```
Tim kami menghitung 'in review' juga sebagai belum selesai. Rapikan ulang dengan kriteria itu.
Mulai sekarang juga, anggap 'in review' = belum selesai.
```

Pada keluaran berikutnya, TASK_009 masuk ke posisi nomor 2. Kalimat terakhir ("Mulai sekarang juga ... anggap") hanya berlaku untuk sesi ini. Jika Anda tidak ingin mengulang aturan yang sama setiap kali, masukkan definisi ini sebagai atom ke slot `shared` pada `team_memory`, maka mulai sesi berikutnya LLM akan menerapkannya secara mandiri (lihat §20.1·§20.2).

Apa yang ditunjukkan oleh satu kali bolak-balik ini jelas. MCP adalah **alat untuk mengambil informasi secara akurat**, **bukan alat untuk menggantikan penilaian.** Data bersifat otomatis, dan definisi diberikan oleh manusia. Begitu batas itu dikaburkan, otomatisasi berubah menjadi insiden.

---

## 20.4.3 Lima Pola Pemanfaatan

Hanya dengan satu kemampuan menanyakan alat kolaborasi, hasilnya tidak lebih dari "pencarian jadi sedikit lebih nyaman". MCP menjadi sebuah sistem kolaborasi justru ketika beberapa alat dirangkai menjadi satu alur. Berikut lima pola yang benar-benar dijalankan di Proyek A, dilihat sebagai alur.

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="11">
  <defs><marker id="mcpar" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#888"/></marker></defs>
  <text x="400" y="20" text-anchor="middle" font-size="14" font-weight="bold">Lima Pola Pemanfaatan MCP — Tiap Pola adalah Satu Alur Mandiri</text>
  <text x="400" y="38" text-anchor="middle" font-size="10" fill="#666">Blok berwarna di kiri adalah polanya, kotak putih di kanan adalah tahap yang dilewati pola itu (kiri→kanan)</text>

  <!-- 패턴 1 자동 보고서 -->
  <rect x="8" y="52" width="118" height="42" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1.8"/>
  <text x="67" y="70" text-anchor="middle" font-weight="bold" fill="#1565c0">Pola 1</text>
  <text x="67" y="85" text-anchor="middle" font-size="10" fill="#1565c0">Laporan otomatis</text>
  <rect x="138" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="197" y="69" text-anchor="middle" font-size="10">Tiap hari pukul 09</text>
  <text x="197" y="83" text-anchor="middle" font-size="10">pemicu penjadwal</text>
  <line x1="256" y1="73" x2="266" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="327" y="69" text-anchor="middle" font-size="10">Lihat alat kolaborasi·git·</text>
  <text x="327" y="83" text-anchor="middle" font-size="10">dasbor</text>
  <line x1="386" y1="73" x2="396" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="457" y="76" text-anchor="middle" font-size="10">LLM menyusun laporan</text>
  <line x1="516" y1="73" x2="526" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="528" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="587" y="76" text-anchor="middle" font-size="10">Kirim ke portal/messenger</text>

  <!-- 패턴 2 결정→태스크 -->
  <rect x="8" y="120" width="118" height="42" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1.8"/>
  <text x="67" y="138" text-anchor="middle" font-weight="bold" fill="#2e7d32">Pola 2</text>
  <text x="67" y="153" text-anchor="middle" font-size="10" fill="#2e7d32">Keputusan → task</text>
  <rect x="138" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="197" y="137" text-anchor="middle" font-size="10">Daftarkan decision card</text>
  <text x="197" y="151" text-anchor="middle" font-size="9">proposal P####</text>
  <line x1="256" y1="141" x2="266" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="327" y="137" text-anchor="middle" font-size="10">Buat task di</text>
  <text x="327" y="151" text-anchor="middle" font-size="10">alat kolaborasi</text>
  <line x1="386" y1="141" x2="396" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="457" y="137" text-anchor="middle" font-size="10">Penanggung jawab·tenggat</text>
  <text x="457" y="151" text-anchor="middle" font-size="10">diatur otomatis</text>

  <!-- 패턴 3 태스크→카드 -->
  <rect x="8" y="188" width="118" height="42" rx="6" fill="#fff8e1" stroke="#f9a825" stroke-width="1.8"/>
  <text x="67" y="206" text-anchor="middle" font-weight="bold" fill="#e65100">Pola 3</text>
  <text x="67" y="221" text-anchor="middle" font-size="9" fill="#e65100">Task→kartu (arah balik)</text>
  <rect x="138" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="197" y="205" text-anchor="middle" font-size="10">Task alat kolaborasi</text>
  <text x="197" y="219" text-anchor="middle" font-size="10">selesai</text>
  <line x1="256" y1="209" x2="266" y2="209" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="327" y="205" text-anchor="middle" font-size="10">Decision card</text>
  <text x="327" y="219" text-anchor="middle" font-size="9">execution_log diperbarui</text>

  <!-- 패턴 4 진행률 분석 -->
  <rect x="8" y="256" width="118" height="42" rx="6" fill="#f3e5f5" stroke="#7b1fa2" stroke-width="1.8"/>
  <text x="67" y="274" text-anchor="middle" font-weight="bold" fill="#6a1b9a">Pola 4</text>
  <text x="67" y="289" text-anchor="middle" font-size="10" fill="#6a1b9a">Analisis progres</text>
  <rect x="138" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="197" y="273" text-anchor="middle" font-size="10">Lihat seluruh task</text>
  <text x="197" y="287" text-anchor="middle" font-size="10">satu kuartal</text>
  <line x1="256" y1="277" x2="266" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="327" y="273" text-anchor="middle" font-size="10">LLM menganalisis</text>
  <text x="327" y="287" text-anchor="middle" font-size="10">pola keterlambatan</text>
  <line x1="386" y1="277" x2="396" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="457" y="280" text-anchor="middle" font-size="10">Input retrospektif kuartal</text>

  <!-- 패턴 5 1:1 사전 자료 -->
  <rect x="8" y="324" width="118" height="42" rx="6" fill="#fff3e0" stroke="#e64a19" stroke-width="1.8"/>
  <text x="67" y="342" text-anchor="middle" font-weight="bold" fill="#d84315">Pola 5</text>
  <text x="67" y="357" text-anchor="middle" font-size="10" fill="#d84315">Materi pra-1:1</text>
  <rect x="138" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="197" y="348" text-anchor="middle" font-size="10">5 menit sebelum 1:1</text>
  <line x1="256" y1="345" x2="266" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="327" y="341" text-anchor="middle" font-size="9">Task anggota +</text>
  <text x="327" y="355" text-anchor="middle" font-size="9">team_memory·aktivitas</text>
  <line x1="386" y1="345" x2="396" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="457" y="348" text-anchor="middle" font-size="10">Ringkasan awal otomatis</text>
</svg>

**Pola 1 — Laporan otomatis.** Tiap pagi pukul 9, ketika penjadwal melempar pemicunya, LLM sekaligus menanyakan status task alat kolaborasi, commit git, dan metrik dasbor, lalu menulis laporan harian. Tujuan pengirimannya adalah portal atau messenger tim. "Portal" di sini merujuk pada portal web internal yang dibahas di §20.3. Karena `server.py` (FastAPI) selalu menyala dan `View_*.html` yang ditulis Claude berjalan di atasnya, laporan pun secara alami menempel sebagai salah satu halaman portal.

**Pola 2 — Pembuatan task otomatis dari keputusan.** Ketika decision card (`proposal P####`) didaftarkan, item implementation dan verification pada kartu itu langsung menjadi task alat kolaborasi. Penanggung jawab dan tenggatnya pun terisi otomatis. Apa yang diputuskan dalam rapat dengan "kalau begitu kita lakukan seperti ini" jatuh menjadi kartu di papan tanpa lewat tangan.

**Pola 3 — Referensi balik dari task ke decision card.** Ini arah kebalikan dari Pola 2. Ketika task alat kolaborasi selesai, MCP memperbarui `execution_log` pada decision card asalnya. "Apakah keputusan ini benar-benar dijalankan" terlacak secara otomatis. Keputusan dan eksekusi terikat dua arah (garis putus-putus pada gambar).

**Pola 4 — Analisis progres.** Di akhir kuartal, seluruh task pada kuartal itu ditarik sekaligus untuk menganalisis pola keterlambatan. "Jenis task seperti apa yang berulang kali tertunda" menjadi input bagi retrospektif.

**Pola 5 — Materi persiapan 1:1.** Lima menit sebelum rapat 1:1, task alat kolaborasi anggota terkait, slot `team_memory`, dan aktivitas terakhirnya disintesiskan menjadi ringkasan awal. Alih-alih menghabiskan 5 menit untuk "Kemarin Anda sedang mengerjakan apa, ya?", 1:1 langsung dimulai dari pokok pembahasan.

Kesamaan dari kelima pola itu satu. **Nilai baru terambil kembali hanya di tempat yang mengurangi pekerjaan berulang di tangan manusia.** Pola yang dipasang sekadar agar terlihat keren hanya menambah beban operasional.

---

## 20.4.4 Adopsi Bertahap — Jangan Pasang Semuanya Sekaligus

Menghubungkan kelima server MCP sekaligus di hari pertama adalah kegagalan yang paling umum. Ada urutannya.

| Tahap | Apa | Perkiraan durasi |
|---|---|---|
| 1 | Pasang 1 server MCP (ClickUp atau JIRA) | 1\~2 hari |
| 2 | Uji coba 1 pola (laporan otomatis) | sekitar 1 minggu |
| 3 | Operasikan 5 pola | 1\~2 bulan |
| 4 | Kembangkan server MCP sendiri (jika perlu alat khusus) | 1\~3 bulan |

Durasi di atas adalah perkiraan penulis (belum terverifikasi) berdasarkan tim berskala menengah (10\~50 orang) di Proyek A, dan dapat berbeda tergantung ukuran tim serta keakraban dengan alat. Yang jelas adalah **bagi sebagian besar tim, tahap 1\~3 sudah cukup**. Tahap 4 (pengembangan server sendiri) baru ditempuh ketika benar-benar harus menghubungkan alat internal khusus yang server MCP-nya belum ada di pasaran. Tanpa sampai ke sana pun, sebagian besar efeknya sudah terambil kembali.

Ada alasan untuk menyinggung JIRA secara tersendiri. Jika ClickUp adalah papan internal tim, JIRA sering kali merupakan alat yang **dibagikan dengan organisasi eksternal** seperti penerbit atau pihak outsourcing. Dengan memasang MCP JIRA, progres papan pihak outsourcing bisa ditarik otomatis setiap minggu sebelum rapat, sehingga task yang dicurigai terlambat dapat dipilah lebih dulu. Rapat pun dimulai bukan dari "berbagi situasi" melainkan dari "keputusan". Namun, semakin sebuah alat dibagikan ke luar, semakin berat pula jebakan izin dan kebocoran pada subbab berikutnya membebani.

---

## 20.4.5 Empat Jebakan — Mengapa MCP Bermata Dua

MCP adalah perkara memberikan alat ke tangan LLM. Kalau yang ada di tangan adalah pisau, bisa juga melukai.

**Jebakan 1 — Insiden izin.** Jika LLM bahkan memegang izin write, perubahan yang tidak dikehendaki bisa terjadi. Misalnya, satu kalimat "rapikan, dong" malah mengubah status sejumlah besar task sekaligus. Resepnya jelas. **Mulailah server MCP dengan read-only.** Izin write hanya dibuka di tempat yang benar-benar perlu seperti Pola 2·3, itu pun dengan gerbang konfirmasi sebelum eksekusi. Bahwa LLM pada transkrip sebelumnya balik bertanya kepada manusia soal klasifikasi 'in review' juga lahir dari semangat yang sama — kalau ragu, berhenti.

**Jebakan 2 — Kebocoran data.** Data perusahaan yang ditarik lewat MCP dikirim ke API LLM eksternal. Angka balance, konten yang belum dirilis, dan metrik pendapatan bisa mengalir keluar begitu saja. Resepnya adalah, khusus untuk data sensitif, memakai LLM yang di-hosting sendiri, atau mengganti data dengan placeholder di sisi server MCP sebelum dikirim keluar (sama dengan prinsip perlindungan IP yang dipegang buku ini secara keseluruhan).

**Jebakan 3 — Ledakan dependensi.** Jika 5 server MCP digantungkan pada jalur critical, ketika satu mati maka seluruh laporan pagi berhenti. Resepnya adalah menempatkan hanya 1\~2 server inti sebagai critical dan memisahkan sisanya sebagai pendukung. Kalau server pendukung mati, hanya item itu yang kosong, sedangkan laporannya sendiri tetap keluar.

**Jebakan 4 — Ledakan biaya API.** Satu kali panggilan MCP membakar token LLM dan panggilan API eksternal sekaligus. Kalau laporan otomatis dijalankan tiap 5 menit, biaya membengkak diam-diam. Resepnya adalah memasang cap pada frekuensi panggilan dan melakukan caching pada hasil query yang jarang berubah.

Jika keempat jebakan diringkas dalam satu baris, posisi aman MCP adalah **"mulai dengan read-only, tempatkan hanya yang inti sebagai critical, saring data sensitif, dan pasang batas atas pada panggilan"**.

---

## 20.4.6 Efek — Di Mana Waktu Terambil Kembali

Berikut perubahan yang saya rasakan di Proyek A, sebelum dan sesudah mengoperasikan MCP. Angka waktu di bawah adalah perkiraan empiris penulis (belum terverifikasi); mohon dibaca sebagai **arah dan rasio**, bukan sebagai nilai mutlak.

| Item | Tanpa MCP | Dengan MCP | Arah |
|---|---|---|---|
| Penyusunan informasi laporan harian | manual 30\~60 menit | otomatis \~5 menit | jauh lebih singkat |
| Sinkronisasi informasi antaralat | kerja manual manusia | otomatis | kerja manual hilang |
| Persiapan awal 1:1 | 10\~15 menit | ringkasan otomatis \~3 menit | lebih singkat |
| Memantau progres outsourcing | hanya lewat rapat | query real-time | jadi berkelanjutan |
| Tautan keputusan ↔ task | kerja manual | otomatis dua arah | mencegah kelolosan |

Pengembalian terbesar terjadi pada "waktu untuk mengumpulkan informasi". Keputusan dan penilaian tetap menjadi urusan manusia. Yang dipangkas MCP adalah bagian di hulunya, yaitu kerja kasar menelusuri alat-alat yang tercerai-berai untuk dikumpulkan dalam satu tempat. 3 detik di awal bab ini persis menempati posisi itu.

---

## 20.4.7 Menutup Bagian 20

Bagian 20 menumpuk sistem kolaborasi tim dalam empat lapis.

| Bab | Inti |
|---|---|
| 20.1 | Operasi atom — pengelompokan kategori, perapian per kuartal |
| 20.2 | Memori anggota tim — `team_memory` slot 5 orang (leeminsoo·anggota A/b/c·shared), pemisahan bersama vs pribadi |
| 20.3 | Portal web — beroperasi terus-menerus dengan `server.py`(FastAPI)·`build_index.py`·nginx·nssm, `View_*.html` berjalan |
| 20.4 | MCP — 5 pola·adopsi bertahap·izin diutamakan |

Keempat bab bukanlah alat yang berdiri sendiri-sendiri, melainkan satu kesatuan. Portal (20.3) adalah tempat laporan menempel, atom dan memori (20.1·20.2) adalah tempat LLM mengingat definisi tim seperti 'in review = belum selesai', dan MCP (20.4) adalah jaringan kabel yang menghubungkan semua itu dengan alat kolaborasi dan dokumen. Kalau salah satunya dicabut, nilai dari sisanya pun berkurang separuh.

Pada bagian berikutnya, kita membahas tata kelola dan operasional. Masalah keamanan, biaya, hak cipta, dan etika yang menyertai ketika sudah memasang sebanyak ini akan dirangkum dengan mengangkat jebakan-jebakan bab ini menjadi aturan di tingkat tim.

---

### Poin-Poin Penting

- MCP adalah standar yang membuatkan kunci alat lama untuk LLM tanpa mengganti alatnya.
- Data diambil oleh MCP dan definisi·penilaian diberikan oleh manusia — batas itulah garis amannya.
- Jika dimulai dengan read-only dan hanya yang inti ditempatkan sebagai critical, otomatisasi tidak akan merembet menjadi insiden.

---

## 20.4.8 Coba Sendiri — Koneksi Pertama MCP ClickUp

**setup**
1. Pasang server MCP ClickUp (resmi atau komunitas), dan terbitkan token API ClickUp.
2. Daftarkan server MCP ke pengaturan Claude Code, tetapi mulailah **hanya dengan scope read-only**.
3. Pastikan ID workspace untuk membatasi cakupan query ke papan Anda sendiri.

**prompt**
```
Di ClickUp, rapikan task P0 yang belum selesai dan tenggatnya minggu ini, urut dari yang paling dekat tenggatnya.
Sertakan penanggung jawab dan sisa hari menuju tenggat, dan naikkan yang sudah lewat tenggat ke paling atas.
```

**verify**
1. Buka langsung 1 dari task yang dikeluarkan di ClickUp dan cocokkan apakah tenggat dan penanggung jawabnya benar.
2. Perhatikan apakah LLM balik bertanya sendiri terhadap item yang ambigu — kalau ia memvonis tanpa balik bertanya, perintahkan ulang dengan menyebutkan kriteria klasifikasi secara eksplisit.
3. Definisi yang sering dipakai (seperti 'in review = belum selesai') masukkan sebagai atom ke `shared` pada `team_memory` agar otomatis diterapkan pada sesi berikutnya.

### Versi Ringkas Solo

Jika Anda developer solo tanpa tim maupun alat kolaborasi, sasaran pertama MCP adalah **GitHub dan dokumen lokal**. Pasang MCP GitHub secara read-only dan mulai dari query seperti "isu yang belum ditutup minggu ini, urut dari yang paling lama", lalu alih-alih decision card, tanyakan markdown pada folder `decisions/` lokal lewat MCP dokumen. Laporan otomatis (Pola 1) berlaku begitu saja — cukup ganti tujuan pengirimannya dari messenger tim menjadi file catatan Anda sendiri. Jebakan izin dan biaya tetap berlaku sama meski Anda sendirian, jadi sebaiknya patuhi memulai dengan read-only dan cap panggilan sejak awal.
