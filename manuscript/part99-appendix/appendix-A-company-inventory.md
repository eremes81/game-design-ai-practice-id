# Lampiran A. Inventaris Rinci Sistem PC Kantor

> Lampiran ini mengumpulkan dalam satu lembar seluruh lingkungan PC kantor di perusahaan pengembang MMORPG A yang saya kelola — mulai dari perangkat keras, alat, aset pengetahuan, hingga materi verifikasi. Hal-hal yang di sepanjang teks utama saya sebut sebagai "dengan alat seperti ini", "dengan struktur atom seperti ini", "dengan laporan seperti ini" saya rangkum di sini supaya Anda dapat melihat sekali pandang dalam skala dan kombinasi seperti apa semuanya benar-benar ada. Semua nama asli dan nama diri telah dianonimkan, dan karena angka berubah-ubah sesuai waktunya, mohon dibaca bukan sebagai nilai mutlak melainkan sebagai proporsi dan komposisi.

Ada dua cara membaca lampiran ini. Yang pertama adalah membandingkannya dengan lingkungan Anda sendiri, item demi item. Jika Anda mengisi kotak yang sama dengan "mesin apa yang saya pakai, alat kolaborasi apa yang saya pakai, dalam bentuk apa aset pengetahuan saya tertumpuk", kotak kosong Anda akan terungkap. Yang kedua adalah melihat keseimbangan komposisinya. Banyaknya alat tidak membuat lingkungan menjadi baik; yang penting adalah apakah lima poros — mesin, desain, seni, kolaborasi, dan AI — saling berkaitan tanpa saling menghalangi. Mohon perhatikan jalinannya, bukan tiap-tiap item satu per satu.

---

## A.1 Gambaran Umum Sistem

Yang paling pertama adalah perangkat keras dan sistem operasi yang menjadi fondasinya. Begitu Anda mulai serius memakai alat AI, akan muncul situasi di mana Anda menjalankan model diffusion atau STT secara lokal, sehingga kelapangan memori dan GPU langsung menjadi kecepatan kerja. Mohon pandang spesifikasi di bawah ini sebagai garis dasar yang mendekati batas bawah — "kalau segini, semua berjalan tanpa tersendat".

### A.1.1 Perangkat Keras

| Item | Spesifikasi |
|---|---|
| CPU | Kelas workstation desktop |
| RAM | 64GB ke atas |
| GPU | Untuk pengembangan UE5 (kompatibel CUDA) |
| Penyimpanan | SSD 2TB + berbagi NAS |
| Monitor | 2 unit 27 inci |

Dua baris RAM dan GPU adalah intinya. Sebab momen menjalankan editor mesin, alat bantu LLM lokal, dan pembangkitan gambar secara bersamaan sering datang.

### A.1.2 Sistem Operasi · Basis

| Item | Nilai |
|---|---|
| OS | Windows 11 Pro |
| Virtualisasi | WSL2 (Ubuntu), bila perlu |
| Cadangan | Otomatis harian |

WSL2 bukan dinyalakan terus-menerus, melainkan ditarik untuk dipakai hanya saat menjalankan alat khusus Linux. Bahwa pencadangan berjalan otomatis setiap hari adalah baris terpenting dalam tabel ini.

---

## A.2 Inventaris Alat

Alat dikelompokkan ke dalam lima cabang: mesin · perkakas, desain · perencanaan, seni, kolaborasi · operasional, dan AI · LLM. Tidak ada satu orang pun yang memakai kelima cabang itu seluruhnya, tetapi seorang Game Designer setiap hari bolak-balik di tiga cabang — desain · perencanaan, kolaborasi · operasional, dan AI · LLM. Mohon perhatikan bahwa tiap cabang berbentuk "satu-dua yang wajib + pendukung".

### A.2.1 Mesin Game · Perkakas

| Alat | Kegunaan |
|---|---|
| Unreal Engine 5.7 ke atas | Mesin utama |
| Visual Studio | Kode |
| Rider | IDE C# (pendukung) |
| Perforce atau SVN | Kontrol versi kode · aset |

Mesin dan kontrol versi adalah sepasang. Seorang Game Designer pun wajib bisa mengoperasikan klien kontrol versi. Sebab sheet data dan dokumen spesifikasi semuanya bergulir di repositori yang sama.

### A.2.2 Desain · Perencanaan

| Alat | Kegunaan |
|---|---|
| Excel | Sheet data + makro VBA |
| Editor Markdown | Spesifikasi · notula rapat |
| Figma | UI · wireframe |
| Mermaid | Diagram |

Inilah meja kerja sehari-hari seorang Game Designer. Excel adalah markas besar data, Markdown adalah markas besar tulisan, dan keduanya juga merupakan dua titik tempat alat AI menempel paling dalam. Alasan Mermaid menempati satu kotak adalah, seperti ditekankan dalam teks utama, diagram itu sendiri merupakan bahasa kesepakatan.

### A.2.3 Seni

| Alat | Kegunaan |
|---|---|
| Maya / Blender | 3D |
| Substance 3D | Tekstur · material |
| Photoshop | 2D · ilustrasi |
| Stable Diffusion(SDXL) / ComfyUI | Produksi massal konsep · tekstur utama dengan hosting sendiri (LoRA · ControlNet) |
| Midjourney | Moodboard awal (pendukung) |

Memang ini bukan alat yang dipakai langsung oleh Game Designer, tetapi ketika bertukar konsep dengan bagian seni, mengetahui alat apa yang ada di sisi mereka akan mengubah resolusi permintaan Anda. Produksi massal utama berporos pada Stable Diffusion(SDXL)/ComfyUI yang di-hosting sendiri — karena aset tidak diunggah ke luar sehingga IP terjaga, dan dengan LoRA · ControlNet untuk karakter, konsistensi orang yang sama dapat dikendalikan pada setiap pembangkitan berulang. Alat tertutup seperti Midjourney hanya dipakai sebagai pendukung sebatas moodboard awal saat pertama meraba-raba nuansa proyek, dan tidak dipakai untuk produksi massal utama yang menuntut kendali konsistensi · pengulangan.

### A.2.4 Kolaborasi · Operasional

| Alat | Kegunaan |
|---|---|
| Alat kolaborasi (ClickUp) | Task |
| Messenger tim internal | Komunikasi waktu nyata |
| Wiki bikinan sendiri | Wiki · dokumen jangka panjang |
| Web portal bikinan sendiri | Antarmuka terpadu (20.3) |

Sumbu waktu komunikasilah yang memilah alatnya. Komunikasi waktu nyata yang menuntut kesegeraan lewat messenger tim internal, hal yang harus dikerjakan lewat alat kolaborasi (tim kami memakai ClickUp), dan pengetahuan yang ingin disimpan lama lewat wiki bikinan sendiri — sekalipun tracker diganti dengan JIRA · Redmine dan wiki diganti dengan Confluence · Notion, dan apa pun messengernya, alur buku ini tetap sama. Web portal bikinan sendiri adalah jendela terpadu yang menyambungkan ketiganya dengan alat AI dalam satu layar, dan dibahas rinci di 20.3.

### A.2.5 AI · LLM

| Alat | Kegunaan |
|---|---|
| Claude (Opus + Sonnet) | LLM utama |
| GPT-4 | Alternatif |
| Whisper (hosting sendiri) | Pengenalan suara (STT) |
| Stable Diffusion | Pembangkitan gambar (hosting sendiri) |
| Server MCP | Integrasi alat (20.4) |

Yang utama ditaruh Claude, dan GPT-4 ditaruh sebagai verifikasi silang · alternatif. Prinsip bahwa suara · gambar sensitif tidak dikirim ke luar melainkan diproses dengan hosting sendiri tertuang dalam dua baris Whisper dan Stable Diffusion. Server MCP adalah perekat yang menyisipkan alat-alat ini ke dalam alur kerja, dan strukturnya dijelaskan di 20.4.

---

## A.3 Inventaris atom

atom adalah keping pengetahuan dari "unit terkecil keputusan" yang dibahas di teks utama, yang dijatuhkan ke dalam berkas. Berikut adalah tabel yang menunjukkan bagaimana atom itu terdistribusi menurut bidang — satu potret pada momen Mei 2026. Mohon perhatikan di bidang mana keputusan terkumpul, bukan jumlah mutlaknya. Tempat keputusan terkumpul adalah titik yang paling sengit dipikirkan oleh proyek itu.

| Kategori | Jumlah atom | Keterangan |
|---|---|---|
| combat | 47 | Keputusan sistem tempur |
| narrative | 38 | Naratif 5 lapis |
| ui | 31 | UI · HUD |
| balance | 28 | Nilai balance |
| level | 22 | Level Design |
| character | 19 | Karakter · voice_profile |
| meta · governance | 18 | Prosedur · aturan |
| qa · integrity | 16 | Verifikasi |
| content | 14 | Produksi massal konten |
| operations | 14 | Alur kerja operasional |
| external_reference | 12 | Materi eksternal |
| economy | 11 | Ekonomi · sumber daya |
| lainnya | 34 | Klasifikasi sedang berjalan |

Distribusi di mana tempur (combat) paling tebal dan naratif menyusul di belakangnya menampakkan apa adanya karakter proyek ini: ia adalah MMORPG berpusat pada tempur, sekaligus tidak ingin melepaskan bobot kisahnya. "Lainnya 34" adalah keputusan-keputusan baru yang kategorinya belum dipastikan; jika kotak ini membengkak terlalu besar, itu sinyal bahwa sudah waktunya membenahi sistem klasifikasi. Per Mei 2026, totalnya adalah 304 buah.

---

## A.4 Materi Verifikasi · Operasional

Sekalipun ada alat dan pengetahuan, kalau tidak ada perangkat untuk memastikan apakah semuanya berjalan benar, kualitas akan meluruh. Bagian ini memperlihatkan perangkat pemastian itu dalam dua jenis: laporan yang dicetak secara berkala, dan kartu keputusan (decision card) yang ditinggalkan agar pengambilan keputusan bisa dilacak di kemudian hari.

### A.4.1 Laporan

| Laporan | Frekuensi |
|---|---|
| Laporan build harian | Setiap hari |
| Laporan kesenjangan alpha | Mingguan (10.3) |
| Laporan kualitas sprint | Dwimingguan |
| Laporan QA milestone | Tiap milestone |
| Retrospektif kuartalan | Kuartalan |

Frekuensi itulah sifat laporannya. Yang dicetak setiap hari adalah pemeriksaan status, yang mingguan · dwimingguan adalah pemeriksaan tren, dan yang milestone · kuartalan adalah pemeriksaan arah. Titik di mana AI berkontribusi paling besar adalah penyusunan draf laporan berulang seperti harian · mingguan, dan contohnya dibahas di 10.3.

### A.4.2 Kartu Keputusan

| Kuartal | Jumlah keputusan |
|---|---|
| Kuartal 4 2025 | 132 |
| Kuartal 1 2026 | 156 |
| Kuartal 2 2026 (sedang berjalan) | 89 |
| Kumulatif | 547 |

Fakta bahwa sekitar 100 keputusan per kuartal tersisa sebagai kartu, dengan sendirinya menunjukkan prinsip operasional bahwa keputusan diperlakukan bukan sebagai ingatan melainkan sebagai catatan. Angka 89 di kuartal 2 adalah kumulatif pada titik tengah kuartal, jadi merupakan nilai yang sedang berjalan; pada akhir kuartal angkanya mencapai tingkat kuartal sebelumnya. Aliran di mana kartu-kartu ini menumpuk lalu dipromosikan menjadi atom di A.3 adalah sumbu pembelajaran sistem ini.

---

## A.5 Distribusi Rapat (Referensi)

Rapat adalah tempat waktu paling banyak bocor sekaligus tempat efek alat AI paling cepat terasa. Berikut adalah distribusi rata-rata rapat per kuartal yang dikelompokkan menurut kategori — materi referensi untuk memperkirakan skala input dari sistem notula rapat yang dibahas di 17.3. Karena angka beriak-riak tiap kuartal, ditulis sebagai rentang.

| Kategori | Rata-rata per kuartal |
|---|---|
| harian (daily) | 65\~70 kali |
| tempur (battle) | 35\~45 kali |
| seni (art) | 25\~30 kali |
| isu (issue) | 8\~15 kali |
| tinjauan (review) | 6\~10 kali |
| lainnya (1:1 · eksternal) | 40\~50 kali |

Rapat harian paling sering, dan rapat terkait tempur menyusul di belakangnya. Bahwa bentuknya sama dengan distribusi atom di A.3 sungguh bermakna. Di bidang tempat keputusan terkumpul, rapat pun terkumpul. Semakin sering rapat di sebuah lingkungan seperti ini, semakin besar manfaat perapian otomatis notula, dan operasional konkretnya dijelaskan di 17.3.

---

## A.6 Catatan untuk Pembaca

Semua tabel sejauh ini adalah satu lembar foto yang memotret lingkungan saya. Ini bukan daftar untuk disalin mentah-mentah, melainkan mohon dipakai sebagai contoh untuk merapikan lingkungan Anda sendiri dengan kerangka yang sama. Bila ukuran tim, genre, dan platform berbeda, alat, distribusi atom, maupun bobot rapat pun akan berbeda. Yang penting bukan kecocokan item, melainkan apakah empat lapis — "fondasi → alat → pengetahuan → verifikasi" — di lingkungan Anda pun tersambung tanpa terputus. Jika di antara keempat lapis itu ada kotak yang kosong, kotak itulah tempat yang akan Anda benahi berikutnya.
