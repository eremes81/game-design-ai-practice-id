---
title: "Lampiran M. Vektor Dimensi dan Embedding — Intuisi untuk Game Designer"
author: 이민수
status: v3
ip_check: done
---

# Lampiran M. Vektor Dimensi dan Embedding — Intuisi untuk Game Designer

Di lima tempat dalam buku ini — §8.2.7 (ekonomi), §5.4 (voice), §6.3 (persona), §7.3 (pola), §13.3 (data) — ungkapan seperti "memampatkan menjadi vektor dimensi", "embedding", dan "berdekatan di ruang vektor" muncul sebagai **penanda arah**. Ini adalah konsep yang bisa Anda tangkap sepenuhnya hanya dengan kepekaan desain game, bahkan tanpa latar belakang machine learning. Sekali saja Anda meletakkan intuisinya, kelima tempat itu seluruhnya bisa dibaca lewat satu gambar yang sama.

Namun ada satu hal yang ingin saya tegaskan lebih dahulu. **Intuisi konsepnya mudah, tetapi syarat penerapannya berat.** Gagasan ini bukan materi pengantar — ia adalah **penerapan di ujung paling jauh** yang hanya bisa berdiri di atas fondasi yang dibangun buku ini sejak awal: verification gate (gerbang verifikasi) dari penerapan yang konservatif, infrastruktur data dan telemetry, pemeriksa per bidang seperti `voice_lint` dan pemeriksa konsistensi, serta integrasi Layer. Tanpa fondasi itu, jika Anda menggambar koordinat lebih dahulu, seperti terlihat di M.4, peta itu menjadi ilusi yang dengan rapi turut memampatkan galat yang menyimpang dari game. Di sinilah letak alasan sebenarnya mengapa kelima tempat itu semua dinilai 'masih terlalu dini' — bukan karena gagasannya sulit, melainkan karena fondasi yang menopangnya harus didahulukan. Lampiran ini adalah peta yang dibuka oleh tim yang fondasinya sudah lengkap ketika hendak mengukur 'langkah berikutnya', bukan buku pengantar untuk melangkah yang pertama.

## M.1 Satu Kalimat — Fitur Jadi Koordinat, yang Mirip Jadi Titik yang Berdekatan

Mengubah fitur-fitur dari objek apa pun menjadi sebuah daftar angka, lalu meletakkannya sebagai satu titik di atas 'peta', itulah **embedding (penyematan)**. Daftar angka itulah yang disebut **vektor dimensi**. Janjinya hanya satu — **membuat objek yang semakin mirip menjadi titik yang semakin berdekatan di peta**.

Misalnya, jika kita meletakkan NPC sebagai koordinat dari fitur-fitur seperti (formalitas tutur kata, jumlah ekspresi emosi, tingkat kesulitan kosakata, …), maka NPC dengan tutur kata yang mirip akan berkumpul berdekatan di peta. Untuk resep masakan, kita meletakkan komposisi bahan sebagai koordinat sehingga masakan yang mirip berkumpul berdekatan — itulah persis yang dilakukan oleh Epicure yang dijadikan petunjuk di §8.2.7.

<svg viewBox="0 0 520 312" width="700" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="11">
  <defs><marker id="ax3" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 z" fill="#9aa3ad"/></marker></defs>
  <text x="260" y="20" text-anchor="middle" font-size="13" font-weight="bold">'Peta' tempat fitur dipindahkan jadi koordinat — 3D pun analogi, sebenarnya ratusan dimensi</text>
  <polygon points="210,120 305,170 210,220 115,170" fill="#f5f7f9" stroke="#cdd5dd" stroke-width="1"/>
  <line x1="257.5" y1="145" x2="162.5" y2="195" stroke="#dde3e8" stroke-width="0.8"/>
  <line x1="162.5" y1="145" x2="257.5" y2="195" stroke="#dde3e8" stroke-width="0.8"/>
  <line x1="210" y1="120" x2="305" y2="170" stroke="#9aa3ad" stroke-width="1.2" marker-end="url(#ax3)"/>
  <line x1="210" y1="120" x2="115" y2="170" stroke="#9aa3ad" stroke-width="1.2" marker-end="url(#ax3)"/>
  <line x1="210" y1="120" x2="210" y2="48" stroke="#9aa3ad" stroke-width="1.2" marker-end="url(#ax3)"/>
  <text x="312" y="178" font-size="9" fill="#888">Fitur 1</text>
  <text x="84" y="178" font-size="9" fill="#888">Fitur 2</text>
  <text x="210" y="42" text-anchor="middle" font-size="9" fill="#888">Fitur 3 … (ratusan)</text>
  <g fill="#388e3c" opacity="0.5">
    <circle cx="167" cy="148" r="5"/><circle cx="178" cy="140" r="5"/><circle cx="158" cy="151" r="5"/><circle cx="186" cy="144" r="5"/><circle cx="170" cy="145" r="5"/>
  </g>
  <text x="150" y="172" text-anchor="middle" fill="#2e7d32" font-size="9">Klaster belakang (makin jauh makin pudar)</text>
  <ellipse cx="214" cy="134" rx="29" ry="18" fill="none" stroke="#e64a19" stroke-dasharray="5" stroke-width="1.4"/>
  <text x="214" y="132" text-anchor="middle" fill="#d84315" font-size="9">Area kosong</text>
  <text x="214" y="144" text-anchor="middle" fill="#d84315" font-size="8">Kombinasi yang belum ada</text>
  <line x1="252" y1="136" x2="168" y2="148" stroke="#7b1fa2" stroke-dasharray="4" stroke-width="1.4"/>
  <circle cx="210" cy="142" r="4" fill="#7b1fa2"/>
  <g fill="#1976d2">
    <circle cx="256" cy="124" r="7"/><circle cx="252" cy="144" r="7"/><circle cx="244" cy="116" r="7"/><circle cx="253" cy="135" r="7"/><circle cx="259" cy="121" r="7"/>
  </g>
  <text x="274" y="106" text-anchor="middle" fill="#1565c0" font-size="9">Klaster depan (makin dekat makin pekat)</text>
  <text x="258" y="246" text-anchor="middle" fill="#6a1b9a" font-size="10">Hubungkan dua titik, di antaranya = interpolasi (variasi tengah)</text>
  <text x="260" y="290" text-anchor="middle" font-size="9" fill="#888">Titik dekat = mirip · Area kosong = kombinasi yang belum ada · Antara dua titik = interpolasi</text>
</svg>

## M.2 Begitu Peta Tergambar, Tiga Hal Tampak Lewat Jarak dan Posisi

1. **Titik yang berdekatan = yang mirip.** Jika titik-titik menggumpal di satu tempat, itu sinyal bahwa 'keragaman telah mati' (§5.4 konvergensi voice, §6.3 kebasian persona dilihat bukan sebagai kesan, melainkan sebagai kerapatan titik).
2. **Area kosong = kombinasi yang belum ada.** Tempat yang tak punya satu titik pun adalah ruang desain kosong yang berkata 'desain seperti ini belum ada' (§7.3 area kosong pola, §13.3 kemunculan topik baru).
3. **Antara dua titik = variasi tengah.** Hubungkan dua titik lalu ambil bagian di antaranya, maka muncul 'tengah' — inilah **interpolasi (interpolation)**. Menghubungkan antara 'beras' dan 'daun kari' memunculkan cita rasa di antara keduanya; menghubungkan dua NPC memunculkan persona di antara keduanya.

## M.3 Tiga Istilah yang Sering Muncul

- **Embedding (penyematan)**: mengubah fitur menjadi koordinat (vektor) dan meletakkannya di peta.
- **Cosine similarity (kesamaan kosinus)**: bila dua titik menunjuk ke arah yang sama dari titik asal bernilai 1, bila tegak lurus bernilai 0 — penggaris yang lazim untuk mengukur kedekatan lewat 'seberapa sama arahnya' (antara 0 dan 1). Nilai 0.83 yang muncul di §6.3 berarti "cukup mirip".
- **Klaster (cluster)**: gumpalan titik yang menyatu berkelompok di peta. Klaster yang muncul dengan sendirinya tanpa diberi nama terlebih dahulu oleh manusia disebut 'kohort emergen' di §13.3.

> **Tampak mirip tetapi berlawanan — jangan dikelirukan dengan AHP.** AHP (Analytic Hierarchy Process, Saaty) yang dipakai untuk pengambilan keputusan multikriteria juga tampak serupa dalam hal mengubah penilaian kualitatif menjadi vektor — karena ia membandingkan kriteria dua-dua lewat perbandingan berpasangan untuk menarik bobot prioritas (eigenvektor utama). Namun arahnya berlawanan. AHP adalah pengambilan keputusan top-down, tempat **manusia mendefinisikan kriteria dan hierarki terlebih dahulu** lalu memberi bobot di dalamnya, sedangkan embedding di sini adalah penemuan bottom-up, tempat **klaster muncul dengan sendirinya dari data tanpa definisi dari manusia**. Batas yang hendak ditembus §13.3 — 'segmen yang sudah didefinisikan manusia terlebih dahulu' — justru adalah titik berangkat AHP. Keduanya bukan di tempat yang sama, melainkan di sisi yang berseberangan.

## M.4 Mengapa Buku Ini Menulis 'Masih Terlalu Dini' — Harga dari Pemampatan

Peta itu ampuh, tetapi tidak gratis.

- Dimensi yang sebenarnya bukan dua, melainkan ratusan. Peta 2D pada gambar di atas hanyalah analogi, dan ratusan dimensi tak bisa dilihat dengan mata sehingga hanya ditangani lewat 'angka' seperti jarak dan klaster.
- **Pemampatan adalah tindakan membuang informasi.** Fitur mana yang dijadikan dimensi (apa yang independen dan apa yang dependen) adalah teka-teki domain, dan kecelakaan terjadi pada dimensi yang dibuang.
- Yang terpenting, jika data atau model sebelum diubah menjadi koordinat sudah menyimpang dari game, maka pemampatan hanya akan turut memampatkan galat itu dengan rapi.

Karena itu buku ini menempatkan vektor dimensi **bukan sebagai resep, melainkan sebagai penanda arah** — ranah yang akan ditengok beberapa tahun kemudian oleh tim yang fondasi verifikasinya (telemetry, simulasi) sudah kokoh. Petunjuk konkret per bidang saya sebar di §8.2.7 (ekonomi), §5.4 (voice), §6.3 (persona), §7.3 (pola), §13.3 (data), dan semuanya bisa dibaca di atas satu lembar peta dari lampiran ini.
