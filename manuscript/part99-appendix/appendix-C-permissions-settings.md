# Lampiran C. Referensi Izin dan Pengaturan

Lampiran ini mengumpulkan di satu tempat tabel referensi izin dan pengaturan untuk alat serta sistem yang dikutip pada bagian utama buku. Bagian utama menjelaskan "mengapa dijalankan seperti ini", tetapi saat hendak menerapkannya pada lingkungan Anda sendiri, Anda butuh jawaban atas "lalu secara konkret nilai apa yang harus dimasukkan dan ke mana". Lampiran ini mengisi celah itu.

Alasan pemilihan sebuah nilai lebih penting daripada nilai pengaturan itu sendiri. Daripada menyalin begitu saja angka yang tertulis di tabel, bacalah keterangan singkat di bawah setiap butir lalu sesuaikan dengan skala tim dan tingkat risiko Anda. Jika Anda bekerja sendiri, tidak perlu membagi tingkat izin; jika tidak ada pihak alih daya (outsourcing), butir outsourcing dapat dilewati seluruhnya.

Ada dua cara memakai lampiran ini. Saat pertama kali menyiapkan lingkungan, telusuri secara berurutan mulai dari C.1 dan gunakan seperti daftar periksa untuk memastikan tidak ada butir yang terlewat. Saat sedang beroperasi, ketika terjadi insiden, bukalah lebih dulu C.7 (Penanganan Insiden), cari baris insiden yang sesuai, lalu telusuri ke atas menuju butir pencegahan di atasnya.

---

## C.1 Izin LLM API

Kunci LLM API berhubungan langsung dengan biaya, dan jika bocor langsung berujung pada insiden finansial. Karena itu, pengelolaan kunci dan tingkat izin dibahas paling awal.

### C.1.1 Pengelolaan Kunci

| Kunci | Penyimpanan |
|---|---|
| Anthropic API | Variabel lingkungan + 1Password |
| OpenAI API | Variabel lingkungan + 1Password |
| Self-hosted | Internal perusahaan |

Kunci diinjeksikan melalui variabel lingkungan, bukan ditulis di dalam kode, dan aslinya disimpan di alat manajemen rahasia (misalnya 1Password). Insiden paling umum adalah menaruh kunci di dalam kode lalu mengunggahnya ke git, jadi menyertakan kunci ke dalam git dilarang tanpa kecuali.

### C.1.2 Tingkat Izin

| Pengguna | Izin |
|---|---|
| Direktur·Senior | full (bertanggung jawab atas operasi cost cap) |
| Anggota umum | cap per tugas |
| Outsourcing | sekali pakai per tugas |

Izin dibagi bukan berdasarkan kepercayaan, melainkan berdasarkan besarnya tanggung jawab. Orang yang memegang izin full juga memikul tanggung jawab mengelola batas biaya (cost cap). Untuk pihak alih daya, izin dibuka hanya sekali per unit tugas, dan ditarik kembali setelah selesai.

---

## C.2 Standar Pengaturan Alat

Pengaturan yang direkomendasikan berbeda-beda untuk tiap alat, tetapi intinya adalah memisahkan tugas analisis dari tugas kreatif. Analisis harus dapat direproduksi, sedangkan tugas kreatif membutuhkan keragaman.

### C.2.1 Claude Code

Berikut adalah contoh pengaturan dasar Claude Code. Jika dibaca baris demi baris: mengunci model, mengaktifkan extended thinking, menetapkan batas token, mengaktifkan pembaruan otomatis, dan memasang hook yang menginjeksikan memori saat prompt dikirim.

```json
{
  "model": "claude-opus-4-8",
  "extended_thinking": true,
  "max_tokens": 100000,
  "auto_update": true,
  "hooks": {
    "UserPromptSubmit": ["~/.claude/hooks/inject_memory.py"]
  }
}
```

Nilai `model` hanyalah contoh. Karena nama model berubah tiap generasi (contoh ini berdasarkan waktu penulisan), jangan menyalinnya begitu saja, melainkan periksa nama terbaru yang tersedia saat ini lewat `/model` lalu masukkan. Meskipun namanya berubah, kerangka alur kerja buku ini tetap bekerja sebagaimana adanya (lihat Lampiran K).

Skrip yang dipasang pada `hooks.UserPromptSubmit` berperan menyisipkan secara otomatis potongan memori yang relevan setiap kali prompt dikirim. Mekanisme injeksi memori ini dibahas secara rinci di Bagian 24 pada bagian utama buku.

**C.2.1.1 Skema Izin Alat (allow / deny)**

Di dalam `settings.json` yang sama, izin diletakkan terpisah dalam blok `permissions`. Alat yang boleh dijalankan AI secara otomatis tanpa persetujuan manusia ditulis di `allow`, sedangkan alat yang fatal jika sekali saja terjadi insiden — sehingga eksekusi otomatisnya harus dicegah — ditulis di `deny`. Notasinya berbentuk `alat(pola perintah)`, dan `:*` berarti "semua pemanggilan yang diawali perintah tersebut".

```json
{
  "permissions": {
    "allow": [
      "Bash(ls:*)",
      "Bash(git status:*)",
      "Bash(git diff:*)",
      "Read(*)",
      "Grep(*)"
    ],
    "deny": [
      "Bash(rm -rf:*)",
      "Bash(git push --force:*)"
    ]
  }
}
```

Perintah yang tidak akan menimbulkan dampak balik seperti baca·cari (`Read`·`Grep`) dan pengecekan status (`git status`·`git diff`) diberi izin otomatis lewat `allow` untuk mengurangi kelelahan akibat pop-up persetujuan. Sebaliknya, perintah yang satu kesalahannya saja tidak dapat dipulihkan seperti `rm -rf` dan `git push --force` tetap dimasukkan ke `deny`, seberapa luas pun cakupan izin otomatis diperlebar.

Prinsip operasinya ada empat.

| Prinsip | Isi |
|---|---|
| Mulai dengan whitelist | Izin otomatis dimulai seminimal mungkin, tambahkan ke `allow` hanya saat diperlukan |
| Blokir eksplisit perintah berbahaya | `rm -rf`·`git push --force` masuk `deny` tanpa kecuali |
| Rapikan secara berkala | Tiap kuartal, tinjau ulang `allow` dan singkirkan izin yang tidak terpakai |
| Pisahkan per domain | Bagi izin global dan izin proyek, agar PC rumah dan PC kantor memiliki kebijakan yang berbeda |

Daftar `allow` bukanlah konfigurasi statis, melainkan jejak akumulasi pekerjaan. Semakin banyak tugas yang berulang, semakin panjang daftarnya, jadi sebaiknya siapkan juga siklus pembersihan kuartalan beriringan dengannya. Latar belakang pengoperasian izin ini dibahas secara rinci di Bagian 1 Bab 3 pada bagian utama buku.

### C.2.2 Alat Buatan Sendiri

| Pengaturan | Nilai yang Direkomendasikan |
|---|---|
| LLM temperature (analisis) | 0 |
| LLM temperature (kreatif) | 0.7 |
| Cache TTL | 1 jam |
| Cost cap (harian) | Didefinisikan per alat |
| Siklus backup | Harian |

Pemanggilan untuk analisis disetel pada temperature 0 agar input yang sama menghasilkan output yang sama. Tugas yang hasilnya tidak boleh goyah seperti verifikasi·lint·klasifikasi termasuk di sini. Sebaliknya, untuk curah gagasan atau pembuatan draf diberi keragaman sekitar 0.7. Batas biaya jangan dibuat satu standar tunggal, melainkan ditetapkan terpisah per alat, karena setiap alat berbeda frekuensi pemanggilan dan konsumsi tokennya.

---

## C.3 Izin git

| Cabang (branch) | Izin |
|---|---|
| main | Hanya direktur·senior yang boleh push |
| feature/* | Semua anggota |
| protected branches | Code review wajib |

Cabang main dilarang di-push langsung, dan semua perubahan masuk melalui code review di cabang feature. Force-push menimpa riwayat kolaborasi sehingga dilarang, dan pengecualian hanya diberikan atas kesepakatan direktur dan code lead saat pemulihan insiden yang tak terhindarkan diperlukan.

---

## C.4 Izin Sistem Berkas

Folder dokumen membagi izin mengikuti struktur Layer (L0\~L4). Semakin ke atas, cakupan dampaknya semakin luas sehingga izin tulis dipersempit; semakin ke bawah, pekerjaan semakin terdistribusi sehingga izin tulis diperlebar.

| Folder | Izin |
|---|---|
| docs/L0_vision/ | Direktur write, semua read |
| docs/L1_systems/ | Direktur bidang write, semua read |
| docs/L2_content/ | Penanggung jawab read·write |
| docs/L4_meta/ | Semua write |
| team_memory/per-pengguna/ | Hanya yang bersangkutan read·write |

Visi (L0) hanya ditulis direktur dan dibaca semua orang. Sistem (L1) ditulis oleh direktur bidang. Konten (L2) ditulis oleh penanggung jawab, dan meta·sementara (L4) boleh ditulis siapa saja. Memori pribadi hanya dapat diakses oleh yang bersangkutan. Struktur Layer ini sendiri dibahas di Bagian 6 pada bagian utama buku.

---

## C.5 Backup·Pemulihan

| Data | Backup |
|---|---|
| git repo | git itu sendiri + backup jarak jauh |
| Sheet (Excel) | git + backup harian |
| Data pengguna | Backup DB (standar server) |
| Notula·keputusan | git |
| Memori | Sinkronisasi otomatis harian |

Jalur backup berbeda untuk tiap jenis data, tetapi prinsipnya satu. Semakin sulit dipulihkan jika hilang, semakin perlu disimpan ganda. Aset teks (notula·keputusan·kode) menjadikan git sebagai backup itu sendiri, sedangkan data biner atau data server diberi backup terpisah. Target waktu pemulihan (RTO) ditetapkan dalam 4 jam, tetapi nilai ini disesuaikan dengan downtime yang sanggup ditanggung tim.

---

## C.6 Keamanan

| Area | Aturan |
|---|---|
| Data sensitif ke LLM eksternal | placeholder atau self-hosted |
| Pembayaran·informasi pribadi | Dilarang keras dikirim ke LLM |
| Pengutipan materi eksternal | Sumber + tinjauan hukum |
| Perlindungan data pengguna | Anonimisasi + kepatuhan GDPR |

Aturan yang paling mudah dipatuhi sekaligus paling sering dilanggar adalah "jangan mengirim data sensitif ke LLM eksternal". Sebab saat pekerjaan mendesak, godaan untuk menempelkan data nyata apa adanya sangat besar. Pembayaran·informasi pribadi ditetapkan dilarang dikirim tanpa kecuali, dan jika analisis diperlukan, gantilah dengan placeholder atau gunakan model self-hosted.

---

## C.7 Penanganan Insiden

| Insiden | Penanganan |
|---|---|
| Informasi keliru terkirim akibat halusinasi LLM | Segera tarik kembali + laporkan |
| Cost cap terlampaui | Pemblokiran otomatis + tinjauan |
| Insiden hak cipta | Hentikan pemakaian dalam 1 jam + hukum |
| Insiden keamanan (kunci bocor) | Segera ganti kunci + tinjau riwayat pemakaian |
| Kehilangan data | Pemulihan dari backup + analisis insiden |

Dalam banyak kasus, menghentikan insiden dengan cepat lebih penting daripada mencegahnya. Semua penanganan di tabel mengikuti urutan "hentikan dulu, baru analisis". Jika kunci bocor, ganti kunci lebih dahulu sebelum menelusuri penyebabnya, lalu lihat riwayat pemakaiannya. Jika biaya melampaui batas, blokir otomatis terlebih dahulu lalu tinjau. Prosedur penanganan ini dituangkan secara tertulis sebagai aturan baku, dan dilatih secara berkala agar bekerja tanpa ragu saat insiden benar-benar terjadi.
