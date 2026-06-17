---
title: "Sampul · Kata Pengantar · Cara Membaca"
part: 0
status: v3
written: 2026-06-06
author: 이민수
version: v3
---

# AI dan Claude Code untuk Praktik Game Design: Panduan Langsung Pakai

**Tidak ada satu angka pun yang dibuat-buat — alur kerja AI yang saya jalankan selama enam bulan, dibuka seluruhnya hingga prompt, kode, dan verifikasinya**

304 aturan, 48 alat, dan sistem otomasi yang benar-benar dioperasikan seorang direktur dengan pengalaman 24 tahun di sebuah tim berukuran menengah (10–50 orang) — apa adanya

Ditulis oleh Minsoo Lee · 2026

> Seluruh isi buku ini mengacu pada **paruh pertama 2026**. Harga, model, dan fitur alat AI berubah dengan cepat, jadi mohon periksa angka spesifik dan cara pemasangan pada masing-masing halaman resmi untuk informasi terbaru.

---

## Distribusi dan Hak Cipta Buku Ini

Buku ini dipublikasikan secara gratis dengan harapan dapat dibaca seluas-luasnya. Namun, baik versi asli berbahasa Korea maupun terjemahan Bahasa Inggris dan Jepang, satu hal harus tetap dipertahankan di mana pun: bahwa penulis asli buku ini adalah **Minsoo Lee (이민수)**.

- **Lisensi**: Creative Commons **Atribusi-NonKomersial-BerbagiSerupa 4.0** (CC BY-NC-SA 4.0)
- **Penulis asli**: Minsoo Lee (이민수), 2026
- **Edisi resmi (canonical)**: `https://eremes81.github.io/game-design-ai-practice` (GitHub Pages penulis — edisi resmi yang hak penyuntingannya berada pada penulis)

**Anda bebas melakukan hal berikut.** Pembelajaran pribadi, berbagi dan mengutip untuk tujuan nonkomersial, penerjemahan nonkomersial, serta pemanfaatan untuk studi internal di kantor — selama Anda mencantumkan penulis asli beserta tautan edisi resmi, dan jika Anda mengubah isinya atau mengalihbahasakannya ke bahasa lain, sebutkanlah hal itu. Mohon bagikan pula karya turunan dengan ketentuan yang sama.

**Mohon minta izin terlebih dahulu untuk hal berikut.** Penerbitan atau penjualan komersial, penggunaan sebagai materi kursus berbayar, penyertaan dalam produk atau layanan perusahaan, serta redistribusi yang menghapus atribusi penulis asli.

Pengetahuan yang termuat dalam buku ini sudah lengkap dalam satu jilid, dan dengan sendirinya gratis. Jika buku ini bermanfaat dan Anda ingin mendukung penulis, saya akan berterima kasih bila Anda turut menyumbang lewat e-book resmi atau kit berbayar.

---

## Kata Pengantar — Buku yang Ditulis Tiga Kali

Buku ini ditulis tiga kali.

Yang pertama bukanlah sebuah buku, melainkan **manual internal**. Selama enam bulan menjalankan alur kerja AI di perusahaan, saya membakukan keputusan, alat, dan prosedur ke dalam dokumen agar tim tidak perlu menanyakan aturan yang sama dua kali. Dokumen itu tidak dibuat untuk diterbitkan, melainkan dokumen operasional yang menumpuk demi mengurangi pengulangan harian. Dari sanalah kekonkretan buku ini berasal — artinya, fondasinya bukan kasus yang direka-reka demi sebuah buku, melainkan manual yang benar-benar berjalan.

Yang kedua adalah **draf pertama** yang memindahkan manual itu menjadi sebuah buku. Tetapi hasilnya malah menjadi generalisasi yang terdengar meyakinkan tentang "AI bisa melakukan hal-hal semacam ini". Tabelnya banyak, dan angka yang memperlihatkan dampaknya pun banyak. Sebagian besar angka itu diberi keterangan dengan huruf kecil "angka rekaan". Ketika saya membacanya ulang, justru itulah cacat terbesarnya. Saya berbicara tentang pemanfaatan AI tetapi tidak memperlihatkan layar yang sesungguhnya, dan berbicara tentang dampak tetapi mengangkat angka yang dibuat-buat. Saat memindahkan kekonkretan manual ke dalam buku, justru kekonkretan itulah yang hilang.

Maka untuk yang ketiga, saya menulis ulang semuanya. Inilah naskah yang kini ada di tangan Anda. Saya menghidupkan kembali kekonkretan manual internal, tetapi menjaga prinsip buku ini tetap sederhana.

Pertama, **setiap bab memperlihatkan sesi nyata hingga tuntas.** Saya memuat prompt lengkap yang saya ketik, keluaran mentah yang dilontarkan AI, apa yang saya tolak dari keluaran itu, hingga bagaimana saya memintanya kembali. Saya tidak mengakhiri bab dengan kalimat "AI yang mengerjakannya".

Kedua, **angka hanya berasal dari salah satu dari tiga sumber.** Standar publik yang dapat diperiksa siapa pun (harga token model, pedoman aksesibilitas), konstanta yang benar-benar tertanam dalam kode sistem saya, atau nilai yang secara eksplisit saya nyatakan sebagai "ini perkiraan saya". Tidak ada satu pun tabel penghematan biaya yang dibuat-buat. Kejujuran saya jadikan sebagai pembeda.

Ketiga, **saya mengutip apa adanya sistem nyata yang telah saya jalankan selama enam bulan di lapangan.** 304 decision card (atom), 48 alat (skill), hook yang secara otomatis menarik ingatan terkait pada setiap masukan, hingga struktur memori yang memungkinkan satu orang mengelola konteks kolaborasi setara empat orang. Bukan "suatu alat" yang abstrak, melainkan nama berkas, kode, dan skornya saya tulis apa adanya. Pada kasus-kasus di dalam buku, saya hanya menyamarkan nama perusahaan, proyek, dan rekan tim, tanpa menghapus kekonkretan alur kerjanya. (Perusahaan yang mengizinkan penerbitan buku ini saya sebut dengan nama sebenarnya pada bagian ucapan terima kasih — karena saya telah memperoleh persetujuannya.)

Saya seorang Game Designer dengan pengalaman 24 tahun. Saya memasuki industri ini lewat QA dan tinjauan untuk game single-player, lalu menghabiskan waktu membuat RPG, MMORPG, beserta variasinya — dari direktur sebuah MMORPG yang dilayankan ke puluhan negara, pengembangan awal MMORPG AAA berskala 200 orang, hingga Live Ops MMORPG mobile global. Saya terlibat dalam proyek seperti Ragnarok Online, Bless Online, dan seri Mir dengan berbagai peran — sebagai direktur, lead desain, System Designer, dan kadang PM — bahkan pernah mendirikan perusahaan game mobile kecil.

Sejujurnya, saya menyandang kursi direktur terlalu dini. Setelah itu, saya melewati masa panjang sebagai anggota tim: sebagai System Designer yang langsung menyentuh sheet data dan angka pertarungan, sebagai Content Designer yang memproduksi quest dan NPC baris demi baris, merancang event, dan memproduksi konten baru. Sebagian besar alur kerja dalam buku ini lahir dari kursi itu — kursi yang membuat tangan kotor secara langsung, bukan kursi orang yang mengelola — dengan tekad "bagaimanapun caranya saya ingin mengurangi pengulangan ini". Kini di lapangan saya memimpin sebuah tim berukuran menengah (10–50 orang) sebagai Design Director sebuah MMORPG, tetapi alat-alat dalam buku ini bukan alat manajemen seorang direktur, melainkan lahir dari tangan seorang praktisi. Oleh karena itu, sistem dalam buku ini bukanlah teori, melainkan lingkungan kerja yang berjalan setiap hari. Saya juga membahas dengan cara yang sama satu kasus game puzzle kecil yang saya buat sendiri di rumah — saya mengutip apa adanya commit git dan kode nyata game tersebut.

AI tidak dapat menggantikan pekerjaan seorang Game Designer. Namun, AI membebaskan tangan kita dari pekerjaan remeh. Apa yang akan dikerjakan dengan tangan itu tetap menjadi bagian manusia. Saya berharap buku ini menjadi panduan praktis untuk peralihan tersebut.

---

## Cara Membaca Buku Ini

Buku ini tidak harus dibaca berurutan dari awal hingga akhir. Pilihlah jalur yang sesuai dengan situasi Anda. Jika Anda baru pertama kali berkenalan dengan terminal dan pemasangan, bukalah lebih dulu **1.0 "Sebelum Memulai"** — bab yang lebih dahulu meredakan rasa takut terhadap layar hitam.

| Jalur | Rute | Pembaca yang Cocok |
|---|---|---|
| Jalur pengenalan | 1.0 (pemasangan) → Bagian 1 (pengenalan) → Bagian 2 (arsitektur informasi) → 1 bidang Anda | Game Designer yang baru mulai menggunakan alat AI |
| Jalur keseluruhan | Bagian 1·2 → per bidang (Bagian 3–15) → proses (Bagian 16–19) → operasional (Bagian 20–24) | Lead yang merancang adopsi tingkat tim |
| Jalur indie · solo | 1.0 (pemasangan) → Bagian 1·2 → Bagian 23 (pengembangan game pribadi) → "Versi Ringkas Solo" tiap bab | Developer yang membuat sendirian · sebagai hobi, tanpa tim |
| Jalur pekerjaan umum | Bagian 1·2 → Bagian 17 (notula rapat) → Bagian 16 (kolaborasi) → Bagian 18 (pengambilan keputusan) → Bagian 21·22 (perbaikan diri · tata kelola) | Perencana · PM · pekerja kantoran umum di luar game |
| Jalur pemecahan masalah | Indeks lampiran → mundur ke bab terkait | Pembaca yang punya masalah untuk segera dipecahkan |

Di akhir setiap bab terdapat "Coba Sendiri". Tujuannya bukan bab yang dibaca lalu ditutup, melainkan membuat Anda menggerakkan tangan walau satu langkah saja di lingkungan Anda sendiri hari ini.

Satu hal lagi untuk Anda yang bekerja di luar game. Sebagian besar alur kerja dalam buku ini — mengubah notula rapat menjadi keputusan, melacak dampak sebuah keputusan, verification gate (gerbang verifikasi), pengelolaan biaya, hak cipta dan etika — bekerja apa adanya tanpa kaitan dengan game. **Anda boleh membacanya dengan mengganti "game design" menjadi pekerjaan Anda sendiri.** Kotak "Penerapan di Luar Game" di tiap bab adalah jembatannya, dan jika waktu Anda terbatas, dengan mengikuti kursus kilat 90 menit saja (17.1 → 16.2 → 22.1 → 21.1) Anda sudah dapat merasakan kerangka intinya dengan tangan sendiri.

Saya tegaskan satu pembedaan. Dalam buku ini, "solo" dipakai dengan dua makna. Yang satu adalah **direktur solo** — seorang lead yang memikul sendirian konteks kolaborasi setara beberapa orang — dan yang lain adalah **developer solo · hobiis yang membuat game seorang diri**. "Versi Ringkas Solo" di akhir tiap bab ditujukan untuk yang kedua, menuliskan jalur untuk mengambil hanya inti bab tersebut tanpa tim maupun folder perusahaan.

Buku ini boleh dibaca tuntas sebagai satu jilid, atau dibagi menjadi dua jalur — Bagian 1–15 'fondasi · bidang' dan Bagian 16–24 'proses · operasional' — dengan membaca lebih dulu sisi yang Anda butuhkan. Selain itu, sebagian besar kode dalam isi buku dapat dijalankan apa adanya tanpa dependensi eksternal, hanya dengan pustaka standar Python. Hanya sebagian alat seperti grafik relasi yang memerlukan paket di luar standar (networkx, PyYAML), dan di situ saya tuliskan satu baris pemasangan (`pip install …`) berdampingan dengan kodenya. Selain kasus tersebut, tanpa perlu mengunduh apa pun, Anda dapat menyalin blok kode dan langsung menjalankannya untuk memeriksanya.

Bila Anda tersangkut pada sebuah istilah, jangan berhenti di situ; lewati saja dulu. Asingnya terminal hitam bukanlah cacat alat, melainkan soal kebiasaan, dan jarak itu kita perpendek bersama di 1.0 dan Bagian 1.

---

## Cara Pemanfaatan Termudah

Terakhir, saya bisikkan satu cara tercepat untuk memanfaatkan buku ini: membiarkan alat AI seperti Claude Code membaca buku ini secara utuh.

Buku ini tidak ditulis hanya untuk dibaca manusia. Prompt lengkap, kode, dan prosedur verifikasi tiap bab saya tulis dalam bentuk yang dapat dipahami dan direproduksi langsung oleh AI. Jadi, di folder proyek Anda sendiri, Anda dapat menyerahkan buku ini kepada AI — entah dalam bentuk PDF maupun teks — dan memintanya seperti "Baca pola pemeriksaan konsistensi dalam buku ini, lalu buatkan alat pemeriksa yang sesuai dengan sheet data kami". Maka AI akan memasang alur kerja bab terkait sesuai lingkungan Anda. Jalur membuat sendiri bab demi bab dengan tangan, dan jalur menyerahkan buku secara utuh kepada AI lalu membuatnya bersama-sama — keduanya sama-sama terbuka.

Hanya satu hal yang tidak berubah. Apa yang akan diadopsi dan apa yang akan ditolak — keputusan akhir itu, seperti yang berulang kali ditegaskan buku ini dari awal hingga akhir, tetap menjadi bagian Anda. Sekalipun Anda membiarkan AI membaca buku ini untuk memasang sistem, kursi untuk meninjau kandidat yang dilontarkan sistem itu tetap dijaga oleh manusia. Bahkan cara pemanfaatan termudah pun bekerja di atas prinsip tersebut.

---

## Satu Janji

Tidak ada satu pun tabel dalam buku ini yang memuat "angka yang digelembungkan demi meyakinkan pembaca". Alih-alih melebih-lebihkan dampak, saya memperlihatkan **struktur** tempat dampak itu muncul. Jika Anda memindahkan struktur yang sama ke proyek Anda sendiri, angka Anda akan Anda ukur sendiri. Itulah bantuan paling jujur yang dapat buku ini berikan.

---

## Janji di Balik Kata 'Rekonstruksi'

Dalam isi buku ini, keluaran worked transcript (rekaman sesi nyata) sering diberi keterangan **'rekonstruksi (reconstruction)'** — misalnya seperti "Langkah 3 — Keluaran Claude (rekonstruksi)". Apa yang dipertahankan dan apa yang disentuh oleh kata ini, akan saya janjikan dengan tepat sekali saja. Sebab inilah tempat yang tidak boleh dibiarkan paling kabur oleh sebuah buku yang menjadikan kejujuran sebagai judulnya.

'Rekonstruksi' **bukan berarti dibuat-buat, melainkan berarti sesi nyata yang disunting.** Batasannya begini.

| Yang Dipertahankan Apa Adanya | Yang Disunting |
|---|---|
| Prompt masukan lengkap yang saya ketik — dalam bentuk yang bisa disalin dan langsung dipakai | Nama spesifik perusahaan · proyek · NPC · rekan tim → disamarkan untuk buku (perlindungan IP) |
| **Struktur dan kegagalan** keluaran yang dilontarkan AI — kandidat yang meleset, bagian yang diam-diam melanggar aturan, bolak-balik saat saya menolak dan memintanya ulang | Panjang — cabang yang tidak masuk ke isi diringkas menjadi "Kutipan" |
| Kode · konstanta · nilai verifikasi — apa adanya agar dapat direproduksi lewat eksekusi eksternal | Tata letak yang disesuaikan dengan halaman, seperti pemenggalan baris dan margin |

Dengan kata lain, pada keluaran yang direkonstruksi, **saya tidak menambahkan angka yang menggelembungkan dampak ataupun keberhasilan yang tidak pernah ada.** Saya hanya menyamarkan, mengutip, dan merapikannya agar sesuai dengan halaman. Tidak ada satu tempat pun yang keluaran gagalnya saya ubah menjadi keberhasilan — justru saya sengaja membiarkan kegagalannya. Sebab itulah tempat yang memperlihatkan apa yang ditolak manusia. (Sebaliknya, tempat yang saya tandai sebagai 'hasil ukur nyata' · 'dikutip apa adanya' untuk hasil eksekusi kode atau log sistem adalah yang dipindahkan tanpa penyuntingan.)

*Catatan penerjemah: Edisi Bahasa Indonesia ini diterjemahkan dengan AI sebagai draf awal, lalu ditinjau dan disunting oleh manusia. Seluruh worked transcript dalam edisi ini adalah terjemahan dari sesi asli berbahasa Korea — bukan dijalankan ulang dalam Bahasa Indonesia. Prompt dan keluaran di dalam blok kode juga diterjemahkan agar mudah dibaca. Teks asli Korea — materi yang dijanjikan buku ini untuk tidak diubah — tetap dipertahankan apa adanya di edisi Korea (pada repository sumber di GitHub). Sintaksis kode, pengidentifikasi, angka, dan nilai verifikasi tidak diubah sama sekali. Konversi mata uang bersifat perkiraan, dengan kurs sekitar 1.500 won per dolar AS pada pertengahan 2026.*

---
