---
title: "5.1 Struktur NarrativeDocs Layer 0–4"
part: 5
chapter: 1
status: v3
version: v3
written: 2026-05-24
author: 이민수
ip_check: done
---

# 5.1 Struktur NarrativeDocs Layer 0–4

Begitu saya masuk ke ruang rapat, ada satu nama karakter yang dilingkari merah di papan tulis. Sebuah NPC bernama Kim. Di side quest milik seorang Game Designer, ia adalah "ayah angkat yang memungut dan membesarkan sang protagonis sejak kecil", sementara di bab 3 main quest milik Game Designer lain, ia adalah "mantan rekan yang mengkhianati protagonis lalu pergi". Kedua dokumen sama-sama disetujui sebulan lalu, dan keduanya sudah masuk ke build. Bahkan estimasi biaya rekaman suaranya pun sudah keluar.

Ini bukan salah siapa pun. Kedua Game Designer sudah membaca dokumen worldbuilding dan mengacu pada setelan karakter. Masalahnya, setelan karakter yang sama tersebar di tiga berkas yang berbeda, dan tak seorang pun bisa memastikan mana yang "asli". Dokumen worldbuilding itu satu berkas Word setebal 70 halaman dalam satu gumpalan, dan saat dicari, nama Kim muncul di sebelas tempat. Tidak ada pembeda antara baris mana yang merupakan keputusan dan baris mana yang sekadar catatan.

Setelah rapat hari itu selesai, yang kami putuskan adalah memecah NarrativeDocs menjadi lima lapis. Bab ini adalah kisah tentang kelima lapis itu.

---

## 5.1.1 Alasan Memulai dari Bidang yang Paling Abstrak

Ada alasan mengapa pembongkaran Layer per bidang saya buka lebih dulu dari naratif.

Naratif adalah yang paling abstrak. Hal-hal seperti worldbuilding, emosi, dan tone tidak bisa dijatuhkan menjadi angka. Tidak ada satuan yang jelas seperti "jumlah sprite" atau "koefisien damage" sebagaimana pada art atau sistem. Jika bidang seabstrak ini bisa terurai rapi menjadi Layer, maka bidang lain yang lebih konkret pun otomatis terselesaikan dengan pola yang sama. Anggap saja kita melihat dulu apakah ia bekerja di tempat yang paling sulit.

Selain itu, naratif punya antarmuka (interface) paling banyak. Karakter bersentuhan dengan art, quest bersentuhan dengan konten dan level, dialog bersentuhan dengan UX dan lokalisasi, dan reward bersentuhan dengan sistem. Karena ia adalah titik yang paling banyak melintasi antarbidang, nilai dari penyatuan Layer langsung terlihat.

Terakhir, porsi keluaran berupa bahasa alami (natural language) di sini paling tinggi. Karena itu pula ia menjadi bidang tempat bantuan AI bekerja paling besar. Hanya saja, tidak semua game berpusat pada naratif. Untuk genre kasual atau arkade, kedalaman bab ini bisa jadi berlebihan. Meski begitu, kerangka dasarnya sendiri — "memecah dokumen segumpal menjadi Layer lalu mempersempit antarmuka" — bisa dipindahkan apa adanya ke bidang mana pun.

---

## 5.1.2 Laci Berlima Sekat

Bentuk NarrativeDocs setelah dipecah menjadi lima lapis adalah sebagai berikut. Visi (L0) berada di atas, build dan QA (L4) berada di bawah, dan lorong yang menghubungkan antarlapis sengaja dibuat sempit.

<svg viewBox="0 0 720 520" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif">
  <style>
    .layerbox { rx: 8; }
    .ltitle { font-size: 15px; font-weight: bold; fill: #1a1a2e; }
    .ldesc { font-size: 11px; fill: #444; }
    .iface { font-size: 11px; fill: #b03030; font-style: italic; }
    .owner { font-size: 10px; fill: #2a6; }
  </style>

  <!-- L0 -->
  <rect x="120" y="20" width="480" height="60" rx="8" fill="#fdeaea" stroke="#c0392b" stroke-width="2"/>
  <text x="140" y="44" class="ltitle">L0 Visi — "Dunia ini itu apa"</text>
  <text x="140" y="64" class="ldesc">world_premise · narrative_pillar · tone_manifesto  (tetap · sekitar 4.5 halaman)</text>
  <text x="560" y="44" class="owner" text-anchor="end">Director·Lead</text>

  <!-- arrow L0->L1 -->
  <line x1="360" y1="80" x2="360" y2="108" stroke="#888" stroke-width="2"/>
  <polygon points="360,116 355,106 365,106" fill="#888"/>
  <text x="372" y="100" class="iface">pillar · tone (saat berubah, L1 ditinjau ulang)</text>

  <!-- L1 -->
  <rect x="120" y="116" width="480" height="60" rx="8" fill="#eef2fb" stroke="#2c5fa0" stroke-width="2"/>
  <text x="140" y="140" class="ltitle">L1 Sistem — "Cara kerjanya bagaimana"</text>
  <text x="140" y="160" class="ldesc">faction_system · reputation_model · dialogue_branching_rule · lore_consistency_rule</text>
  <text x="560" y="140" class="owner" text-anchor="end">Naratif Senior</text>

  <!-- arrow L1->L2 -->
  <line x1="360" y1="176" x2="360" y2="204" stroke="#888" stroke-width="2"/>
  <polygon points="360,212 355,202 365,202" fill="#888"/>
  <text x="372" y="196" class="iface">rulebook·kebijakan cabang (quest terdampak otomatis terdaftar)</text>

  <!-- L2 -->
  <rect x="120" y="212" width="480" height="60" rx="8" fill="#eef9ee" stroke="#2e8b57" stroke-width="2"/>
  <text x="140" y="236" class="ltitle">L2 Konten — "Apa yang terjadi"</text>
  <text x="140" y="256" class="ldesc">main_quest · side_quest · character_bible · lore_codex  (lapis paling tebal)</text>
  <text x="560" y="236" class="owner" text-anchor="end">Banyak Game Designer</text>

  <!-- arrow L2->L3 (narrow!) -->
  <line x1="360" y1="272" x2="360" y2="300" stroke="#b03030" stroke-width="3"/>
  <polygon points="360,308 354,297 366,297" fill="#b03030"/>
  <text x="372" y="292" class="iface">quest_id · npc_id · dialogue_id (satu kolom)</text>

  <!-- L3 -->
  <rect x="120" y="308" width="480" height="60" rx="8" fill="#fbf5e9" stroke="#c08a2c" stroke-width="2"/>
  <text x="140" y="332" class="ltitle">L3 Data — "Bentuk yang dibaca mesin"</text>
  <text x="140" y="352" class="ldesc">quest_table · npc_table · dialogue_id_table · reward_table  (0 baris bahasa alami)</text>
  <text x="560" y="332" class="owner" text-anchor="end">Naratif+Data</text>

  <!-- arrow L3->L4 -->
  <line x1="360" y1="368" x2="360" y2="396" stroke="#888" stroke-width="2"/>
  <polygon points="360,404 355,394 365,394" fill="#888"/>
  <text x="372" y="388" class="iface">saat sheet berubah, lint otomatis terpicu</text>

  <!-- L4 -->
  <rect x="120" y="404" width="480" height="60" rx="8" fill="#f2eefb" stroke="#7a4fa0" stroke-width="2"/>
  <text x="140" y="428" class="ltitle">L4 Build·QA — "Sudah layak rilis"</text>
  <text x="140" y="448" class="ldesc">narrative_qa_checklist · voice_review_log · localization_status</text>
  <text x="560" y="428" class="owner" text-anchor="end">Naratif+QA</text>

  <!-- side note: locked anchor -->
  <line x1="120" y1="50" x2="60" y2="50" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="50" x2="60" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="434" x2="120" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <text x="52" y="245" class="iface" text-anchor="middle" transform="rotate(-90 52 245)">L0 disuntikkan sebagai konteks setiap kali (anchor pembuatan·tinjauan)</text>
</svg>

Jika dipindahkan ke folder, bentuknya seperti berikut. Tiap nama berkas bukan nama yang diabstraksikan untuk buku ini, melainkan nama berkas yang benar-benar ada di folder tersebut.

```
NarrativeDocs/
├── Layer0_Vision/
│   ├── world_premise.md          (premis worldbuilding — tetap)
│   ├── narrative_pillar.md       (3 pilar emosi)
│   └── tone_manifesto.md         (daftar kosakata tone·terlarang)
├── Layer1_System/
│   ├── faction_system.md
│   ├── reputation_model.md
│   ├── dialogue_branching_rule.md
│   └── lore_consistency_rule.md
├── Layer2_Content/
│   ├── main_quest/               (per bab)
│   ├── side_quest/
│   ├── character_bible/
│   └── lore_codex/
├── Layer3_Data/
│   ├── quest_table.xlsx
│   ├── npc_table.xlsx
│   ├── dialogue_id_table.xlsx
│   └── reward_table.xlsx
└── Layer4_Build_QA/
    ├── narrative_qa_checklist.md
    ├── voice_review_log.md
    └── localization_status.md
```

Yang penting adalah bahwa kelima lapis tidak dipikul oleh satu orang. Penanggung jawab utama berbeda di tiap lapis, dan hanya lorong di antara lapis yang bersebelahan yang dibakukan. Panah merah pada gambar di atas itulah lorong tersebut. Khususnya lorong antara L2 dan L3 sengaja digambar paling sempit (panah merah tebal), dan alasannya akan terlihat di bagian belakang.

Dengan perumpamaan laci, ini adalah laci berlima sekat. Sekat pertama berisi satu baris worldbuilding yang sama sekali tak boleh dipindah, sekat kedua berisi rulebook, sekat ketiga berisi naskah utama, sekat keempat berisi sheet, dan sekat kelima berisi log tinjauan. Lorong antarsekat sempit, dan di atas lorong terpasang lonceng pemberitahuan perubahan.

---

## 5.1.3 L0 — Ditulis Kecil agar Tidak Berubah

L0 tidak berubah. Kalau berubah, berarti identitas game-nya yang berubah. Karena itu volumenya harus kecil. Kecil supaya tidak berubah.

| Dokumen | Volume |
|---|---|
| world_premise.md | 1.5 halaman A4 |
| narrative_pillar.md | 1 halaman A4 (3 emosi) |
| tone_manifesto.md | 2 halaman A4 (tone + daftar kosakata terlarang) |

Totalnya sekitar 4.5 halaman. Inilah bobot L0. Kalau menjadi berat, perubahan akan menakutkan, dan kalau menakutkan, lapis-lapis lain mulai memutari L0. Begitu pemutaran dimulai, L0 menjadi dokumen mati.

Kerangka asli `narrative_pillar.md` bentuknya seperti ini (isinya diabstraksikan).

```markdown
---
title: Pilar Emosi Naratif
layer: L0
status: locked
last_updated: 2026-05-18
---

## 1. Kerinduan akan yang Telah Hilang
- Pemain kehilangan satu hal di akhir tiap bab.
- Yang hilang tidak akan kembali lagi (hanya lewat kilas balik).

## 2. Konflik antara Kewajiban dan Kebebasan
- Setiap NPC utama memikul dua kewajiban.
- Pilihan pemain hanya bisa menyelamatkan salah satu kewajiban.

## 3. Bobot Sentuhan Kecil
- Kebaikan kecil melahirkan hasil yang lebih besar daripada tindakan kepahlawanan besar.
```

Ketiga baris pilar inilah yang menentukan arah ratusan halaman di bawahnya. `status: locked` bukan sekadar label. Salah satu pemeriksaan otomatis di L4 membaca label ini, sehingga apabila dokumen locked diubah dalam sebuah PR, merge dipasang agar terblokir tanpa persetujuan Lead Naratif.

---

## 5.1.4 L1 — Naratif yang Paling Dekat dengan Kode

L1 bisa diubah, tetapi biayanya besar. Sebab ia adalah rulebook. Jika satu baris rulebook berubah, semua konten yang mengikuti aturan itu terdampak.

Kerangka `faction_system.md` adalah sebagai berikut.

```markdown
---
title: Sistem Faksi
layer: L1
atoms:
  - faction_relation_matrix
  - faction_membership_rule
  - faction_quest_eligibility
---

## 1. Konsep Faksi
Ada N faksi. Tiap faksi didefinisikan oleh (ideologi, sumber daya, wilayah).

## 2. Relasi Antarfaksi
- relation_matrix.json (-3 bermusuhan ~ +3 beraliansi)
- Pemicu perubahan relasi: keputusan main quest, ambang reputasi

## 3. Aturan Keanggotaan Pemain
- Maksimum 2 keanggotaan serentak (tidak boleh serentak pada relasi bermusuhan)
- Penalti keluar: reputasi -2, faksi sekutu -1
```

Perhatikan baik-baik daftar `atoms:` pada frontmatter. Ketiga nama atom ini bukan sekadar catatan, melainkan pengidentifikasi yang dilacak oleh ontologi di Bagian 7 dan peta relasi di Bagian 11. Jika sebuah quest mengacu pada `faction_quest_eligibility`, maka saat aturan ini berubah, quest tersebut otomatis naik ke daftar terdampak. L1 adalah keluaran naratif yang paling dekat dengan kode game, jadi dikerjakan berpasangan dengan System Designer.

---

## 5.1.5 L2 — Lapis Paling Tebal, Tempat Naskah Utama Tinggal

L2 adalah yang paling tebal. Main quest, side quest, character bible, dan lore codex semuanya tinggal di sini. Setelan asli si Kim — yang di ruang rapat tadi berbenturan sebagai "ayah angkat vs rekan pengkhianat" — kini hanya ada sebagai satu berkas di dalam `character_bible/`. Berkas itulah satu-satunya sumber kebenaran (single source of truth), dan quest hanya mengacu ke sana.

Folder main quest berbentuk seperti berikut.

```
main_quest/
├── chapter_01_awakening/
│   ├── 00_chapter_overview.md
│   ├── 01_quest_a_call_to_arms.md
│   ├── 02_quest_b_first_choice.md
│   └── ...
├── chapter_02_road/
│   └── ...
└── _TEMPLATES/
    └── quest_template.md
```

Tiap berkas quest mengikuti format standar atom.

```markdown
---
title: Saat Mengangkat Senjata
layer: L2
type: main_quest
atoms:
  - quest_chapter_01_awakening_a
related:
  affects: [reputation_model, faction_relation_matrix]
  derives_from: [narrative_pillar, world_premise]
  requires: [character_kim, faction_alpha]
  part_of: chapter_01_awakening
---

## Tahap Progres
1. ...

## Cabang
- Saat memilih opsi A: ...
- Saat memilih opsi B: ...

## Reward (lihat L3)
- reward_table.xlsx → baris quest_001
```

Intinya ada pada blok `related:`. Begitu tertulis `requires: [character_kim]`, quest ini sudah menyatakan bahwa ia mengambil setelan Kim dari character_bible, dan tidak lagi mendefinisikan ulang Kim di dalam berkasnya sendiri. Naskah utama naratif diletakkan di L2, sedangkan reward berupa angka diletakkan di sheet L3. Jika keduanya berada dalam satu berkas, setiap kali memperbaiki satu baris sheet kita harus menyentuh naskah utama, dan akibatnya kunci terjemahan jadi melenceng.

---

## 5.1.6 L3 — Lapis Tanpa Satu Baris pun Bahasa Alami

L3 adalah sheet dan ID. Tidak ada satu baris pun kalimat bahasa alami yang masuk.

```
quest_table.xlsx
| quest_id | chapter | type | unlock_level | reward_xp | reward_gold | dialogue_set_id |
|----------|---------|------|--------------|-----------|-------------|-----------------|
| q_001    | ch01    | main | 1            | 500       | 100         | ds_001          |
| q_002    | ch01    | main | 2            | 800       | 150         | ds_002          |
```

Dialog pun hanya diacu lewat ID. Naskahnya berada terpisah di `dialogue_id_table.xlsx`, dan dipetakan 1:1 dengan kunci terjemahan. Lorong yang menghubungkan L2 dan L3 cukup hanya satu kolom `quest_id`. Di sinilah alasan mengapa pada gambar sebelumnya hanya lorong ini yang berupa panah merah tebal. Membuat antarmuka menjadi sempit hingga satu kolom adalah inti dari pemisahan Layer. Kalau lorongnya lebar, kedua sisi jadi terlalu banyak saling mengetahui, dan ketika salah satu sisi diperbaiki, sisi lain ikut rusak.

---

## 5.1.7 L4 — Gerbang Rilis

L4 adalah tinjauan dan rilis. Setiap kali konten baru masuk, pemeriksaan otomatis dan manual bekerja. Pemeriksaan otomatis dijalankan dengan skrip. Empat pemeriksaan di bawah adalah lint yang benar-benar terpasang di CI.

| Pemeriksaan | Alat |
|---|---|
| Semua dialogue_id punya pemetaan | `dialogue_lint.py` |
| Semua quest_id termasuk dalam suatu chapter | `quest_lint.py` |
| Total reward berada dalam rentang kurva per bab | `reward_curve_check.py` |
| Kemunculan kosakata terlarang | `tone_lint.py` (berbasis L0 tone_manifesto) |

Perhatikan bahwa `tone_lint.py` membaca langsung `tone_manifesto.md` milik L0. Lapis paling atas (visi yang tetap) dan lapis paling bawah (gerbang rilis) terhubung langsung lewat otomatisasi. Jika kosakata terlarang yang ditulis dalam visi terdeteksi di naskah tepat menjelang rilis, build akan terblokir.

Hal yang tak bisa ditangkap secara otomatis akan dilihat oleh manusia.

| Pemeriksaan | Penanggung Jawab |
|---|---|
| Kesesuaian dengan pilar emosi L0 | Lead Naratif |
| Konsistensi voice karakter | Penanggung jawab karakter + Naratif |
| Kemungkinan lokalisasi | Localizer |

Jika batas antara otomatis dan manual jelas, waktu tinjauan menjadi dapat diprediksi. Kita jadi bisa menjawab pertanyaan, "Tinjauan bab ini perlu berapa hari?"

---

## 5.1.8 Mencoba Menyuruh AI Mengerjakan Layer — Worked Transcript

Sampai sini adalah strukturnya. Namun tempat struktur ini benar-benar bekerja adalah saat membuat konten baru. Saya pindahkan apa adanya sebuah sesi nyata, ketika saya menyuruh Claude — pada proyek yang lima lapisnya sudah terpasang — mengambil ide side quest sepanjang satu baris lalu menebarkannya ke dalam Layer. Tanpa diringkas, termasuk bagian yang melenceng dan bagian yang ditolak.

**Prompt yang dikirim (teks lengkap):**

```
Jangan langgar konteks L0/L1 yang dilampirkan, dan uraikan dengan struktur Layer kita.

[narrative_pillar.md teks lengkap — 3 pilar emosi]
[tone_manifesto.md cuplikan — kosakata terlarang: "takdir", "nubuat", "sang terpilih"]
[character_bible/character_kim.md cuplikan — Kim: ayah angkat yang memungut protagonis,
 pendiam, kalimatnya menggantung, tidak mengutarakan perasaan secara langsung]

Ide: "Side quest singkat di mana Kim menyerahkan benda peninggalan mendiang istrinya kepada pemain."

Tulis berkas quest L2 (termasuk blok related, naskah utama sekitar 200 karakter), baris L3 quest_table dan
dialogue_id, serta pemeriksaan-mandiri pelanggaran tone. Untuk sekarang tulis L2 saja lalu berhenti.
```

**Keluaran mentah Claude (L2):**

```markdown
---
title: Saputangan yang Pudar
layer: L2
type: side_quest
atoms:
  - quest_side_kim_keepsake
related:
  affects: [reputation_model]
  derives_from: [narrative_pillar]
  requires: [character_kim]
  part_of: chapter_02_road
---

## Tahap Progres
1. Kim memanggil pemain dengan tenang. Tidak langsung menyampaikan urusannya seperti biasa.
2. Ia menyodorkan saputangan usang. "Ini… rasanya lebih baik kalau kau yang menyimpannya."
3. Bila pemain bertanya itu apa, Kim malah memandang ke luar jendela alih-alih menjawab.
4. (Pilihan) Menerima / Menolak.

## Cabang
- Menerima: reputasi Kim +1. Di bab berikutnya, 1 kilas balik terkait saputangan terbuka.
- Menolak: Kim mengangguk dan memasukkan kembali saputangan itu. Tidak ada perubahan reputasi.
  Saputangan itu tidak akan pernah muncul lagi.

## Reward (lihat L3)
- reward_table.xlsx → baris quest_side_kim_keepsake
```

Di sini Claude berhenti, dan menambahkan satu baris.

> "Mengacu pada pilar L0 nomor 1 (yang hilang tidak akan kembali lagi), saya membuat saputangan menghilang selamanya jika pemain memilih 'Menolak'. Namun ada satu hal yang perlu dikonfirmasi. Setelan mendiang istri tidak ada dalam cuplikan character_kim.md. Karena saya memasukkannya atas inisiatif sendiri, hal itu bisa berbenturan dengan character bible."

**Verifikasi dan penolakan oleh manusia:**

Keluaran ini tone-nya tepat. Sikap pendiam Kim, kalimat yang menggantung, dan kebiasaan tidak mengutarakan perasaan secara langsung semuanya hidup. Kosakata terlarang juga tidak ada. Namun pemeriksaan-mandiri terakhir tepat menunjuk pada masalah yang sesungguhnya. Tidak ada satu pun setelan yang menyebut Kim punya mendiang istri. AI menyimpulkan secara alami sosok pasangan yang telah meninggal dari kata "benda peninggalan" — dan ini adalah tindakan menyelipkan diam-diam sebuah fakta baru ke dalam bible. Inilah persis benih dari insiden yang terjadi di ruang rapat di awal bab ini.

Maka saya menolaknya. Saya mengirim permintaan ulang.

**Permintaan ulang:**

```
Tone-nya bagus. Tapi "mendiang istri" itu setelan baru yang tidak ada di bible, jadi tidak bisa dipakai.
Masa lalu Kim baru pasti sebatas "meninggalkan sesuatu saat pergi dari kampung halaman". Jangan
tentukan identitas benda peninggalannya, tulis ulang dengan kabur sebatas "sesuatu yang lama
ditinggalkan" saja. Saputangan juga tidak ada di bible, jadi turunkan jadi "secarik kain" saja.
```

**Keluaran setelah permintaan ulang (cuplikan):**

```
2. Ia menyodorkan secarik kain usang. "Dulu… ada satu hal yang kutinggalkan.
   Anggap saja ini ujungnya."
3. Bila pemain bertanya itu apa, Kim malah memandang ke luar jendela alih-alih menjawab.
```

Kali ini saya menerimanya. Tanpa memaku masa lalu Kim sebagai sesuatu yang baru, ia tetap menyentuh pilar emosi nomor 1 (kehilangan). Apa yang hilang dibiarkan kabur sampai akhir.

Satu sesi ini menunjukkan dua hal. Pertama, jika konteks Layer (pilar L0 + tone L1 + bible L2) disuntikkan dengan tepat, AI mencocokkan tone secara mengagumkan baiknya. Kedua, ketika menemui ruang kosong, AI mengisinya dengan sesuatu yang terdengar masuk akal. Saat isian itu berupa fakta baru yang tidak ada di bible, yang menangkapnya tetaplah manusia. Karena `requires: [character_kim]` pada struktur Layer memberi tahu "ke mana harus melihat", verifikator langsung tahu berkas mana yang harus dibandingkan. Seandainya tidak ada struktur, ia akan mengaduk-aduk 70 halaman lagi.

---

## 5.1.9 Lonceng Pemberitahuan di Atas Lorong Sempit

Alasan sebenarnya membagi lima lapis adalah untuk mempersempit antarmuka. Dan di tiap antarmuka yang sempit itu dipasang otomatisasi pendeteksi perubahan.

| Antarmuka | Apa yang mengalir |
|---|---|
| L0 → L1 | pillar, tone (saat berubah, memicu tinjauan ulang rulebook L1) |
| L1 → L2 | rulebook·kebijakan cabang (saat berubah, quest terdampak otomatis terdaftar) |
| L2 → L3 | quest_id, npc_id, dialogue_id (satu kolom) |
| L3 → L4 | saat sheet berubah, lint otomatis terpicu |

Misalnya, jika diajukan PR yang mengubah "maksimum 2 keanggotaan serentak" menjadi "maksimum 1" pada `faction_system.md` di L1, maka peta relasi menyisir quest-quest L2 yang mengacu pada `faction_quest_eligibility`, membuat daftar terdampak, dan daftar itu otomatis dilampirkan ke komentar PR. Orang yang mengubah aturan, alih-alih "menjadwalkan dua-tiga rapat untuk mencari tahu siapa yang terdampak", cukup melihat daftar yang menempel di komentar lalu menuntaskannya dalam rapat 30 menit.

Intinya begini. Kalau hanya Layer yang dibagi tetapi antarmukanya kabur, hasilnya cuma bertambah banyak sekat. Yang esensial adalah otomatisasi antarmuka, bukan pemisahan Layer itu sendiri.

---

## 5.1.10 Enam Bulan Operasional, Apa yang Berubah

Ini adalah pengukuran setelah berpindah ke lima lapis dan menjalankannya selama enam bulan. Angka di bawah berbasis catatan operasional tim penulis, tetapi nilai absolutnya hanya saya pindahkan dalam bentuk arah dan rasio (perkiraan penulis·belum terverifikasi). Ada keterbatasan: sebelum pemisahan berbasis ingatan, sesudah pemisahan berbasis pengukuran nyata, jadi ini bukan menakar materi yang sama dua kali.

| Item | Sebelum Pemisahan Layer | Sesudah Pemisahan Layer |
|---|---|---|
| Onboarding Game Designer baru | 3 minggu | 1 minggu |
| Pemetaan cakupan dampak perubahan rulebook | Rapat 2\~3 kali | Komentar otomatis + rapat 30 menit |
| Pembuatan 1 bab main quest baru | 4 minggu | 2.5 minggu |
| Tinjauan 1 bab pra-rilis | 5 hari | 2 hari |
| Insiden kelolosan lokalisasi | 3\~5 per kuartal | 0\~1 per kuartal |

Yang paling jelas berkurang adalah kelolosan lokalisasi. Karena dialogue_id terikat 1:1 dengan kunci terjemahan di L3 dan `dialogue_lint.py` mencegah pemetaan yang terlewat, insiden "dialog yang belum diterjemahkan masuk ke build" nyaris lenyap. Memendeknya onboarding juga besar pengaruhnya. Kepada Game Designer baru, alih-alih "baca habis 70 halaman Word", kini saya bisa bilang "hafalkan saja 4.5 halaman L0, lalu untuk quest-mu isi template L2".

Sejujurnya saya tambahkan satu hal: efek ini tidak muncul sekaligus. Pada kuartal pertama hanya satu komentar otomatis yang dipasang, sisanya masih kerja manual. Otomatisasi antarmuka saya tambahkan satu per satu tiap kuartal. Memasang otomatisasi memakan waktu lebih lama daripada membagi Layer.

---

## 5.1.11 Alasan yang Lebih Dalam — Jalan Menuju Procedural Generation

Sampai sini adalah alasan permukaan. "Menyatukan bahasa kolaborasi antarbidang." Namun ada satu alasan lagi yang lebih hakiki. Pembongkaran Layer adalah prasyarat yang memungkinkan procedural generation (pembangkitan prosedural). Tesis umum bahwa masing-masing dari lima lapis berpadanan dengan satu peran dalam procedural generation (L0 anchor → L1 rulebook → L2 naskah utama → L3 angka → L4 gerbang), dan bahwa kalau tercampur dalam satu gumpalan, pembangkit tidak bisa menentukan dari mana membaca dan ke mana menulis sehingga runtuh, sudah dibahas utuh di §6.6. Di sini kita hanya melihat bagaimana prasyarat itu benar-benar bekerja di atas lima lapis naratif.

Di atas satu dokumen segumpal 70 halaman, algoritma pembangkit tidak bisa menentukan dari mana membaca dan ke mana menulis. Lima lapis naratif langsung menjadi lima tahap pipeline pembangkitan — L0 anchor, L1 aturan input, L2 tempat naskah utama menumpuk, L3 input simulasi, L4 gerbang verifikasi.

Worked transcript sebelumnya sebenarnya sudah merupakan versi ringkas dari kelima tahap ini. Pilar L0 dan tone L1 disuntikkan sebagai konteks (anchor), naskah utama digenerasi di L2, baris L3 menyusul keluar, dan pemeriksaan-mandiri pelanggaran tone menirukan gerbang verifikasi. Apa yang dikerjakan manusia satu quest pada satu waktu, jika dipindahkan agar generator memproduksi side quest secara massal di atas struktur yang sama, jadilah ia procedural generation.

Jika dibawa lebih jauh, alurnya seperti ini — akumulasi perilaku pemain → perubahan status node BT dunia (Squad tingkat atas) → perubahan angka NPC (reputasi·minat·prioritas) → tag+angka NPC itulah yang menjadi kondisi pemunculan → quest yang cocok muncul dari quest cloud. Quest tidak ditulis lengkap sejak awal, melainkan dibiarkan seperti "awan yang melayang di udara" dengan tag terpasang, dan saat perilaku pemain mengubah angka NPC, quest yang angkanya cocok dengan kondisi pemunculan akan turun dan tampil. Model progresif ini akan dibahas lebih rinci lagi di 5.3 (termasuk diagram alir). Yang ingin ditekankan di sini adalah bahwa seluruh alur ini hanya bekerja di atas pembongkaran lima lapis.

Sebaliknya, tim yang Layer-nya tercampur tidak akan bisa menuju procedural generation. Begitu mencoba, ia runtuh oleh insiden konsistensi. Bayangkan saja insiden Kim yang menjadi ayah angkat sekaligus pengkhianat itu diproduksi secara massal dan otomatis lewat pembangkit.

Hanya saja, ini bukan berarti laci berlima sekat harus lengkap sempurna sejak awal. Pada kuartal pertama, memisahkan satu baris L0 dan satu rulebook L1 saja sudah cukup. Pemisahan dilakukan secara bertahap, antarmuka dibuat sempit.

Terakhir, satu hal tentang penanggalan. Pembongkaran Layer itu sendiri adalah pemisahan yang sudah ada sejak era PCG (Procedural Content Generation, pembangkitan konten prosedural) deterministik. Yang baru adalah bahwa kini LLM menangani naskah utama berbahasa alami, persona, hingga percabangan narasi di atas pemisahan tersebut — pada transcript di atas, tindakan AI menulis dialog dengan mencocokkan tone Kim adalah hal yang mustahil dilakukan dengan tabel aturan lima tahun lalu. Argumen penanggalan ini dibahas lebih lanjut di 5.3.

Di bab berikutnya (5.2) kita akan melihat bagaimana `lore_consistency_rule` di atas lima lapis ini secara otomatis memverifikasi konsistensi worldbuilding→karakter→quest, yakni checker yang mencegah insiden Kim secara struktural.

---

## Coba Sendiri — Pembongkaran Layer Pertama

Kita asumsikan Anda mulai dari kondisi yang sudah memiliki dokumen worldbuilding segumpal.

**setup.** Buatlah lima folder kosong di bawah folder NarrativeDocs. Dari `Layer0_Vision` sampai `Layer4_Build_QA`. Biarkan dokumen segumpal yang lama apa adanya, lalu dari situ pilih hanya "satu baris yang sama sekali tak berubah" dan pindahkan ke `Layer0_Vision/narrative_pillar.md`. Masukkan `status: locked` pada frontmatter. Buat satu berkas ini tidak melebihi 4.5 halaman.

**prompt.** Saat membuat konten baru, berikan konteks kepada AI dalam urutan ini.

```
[narrative_pillar.md teks lengkap]
[tone_manifesto.md kosakata terlarang]
[cuplikan berkas character_bible terkait]

Ide: "<ide satu baris>"

Jangan langgar konteks ini, dan mulai tulis dari berkas quest L2. Isi blok related
(requires/derives_from/affects), jangan masukkan setelan baru yang tidak ada di bible,
dan kalau perlu berhentilah lalu bertanya.
```

**verify.** Lihat dua hal pada keluaran. (1) Buka berkas yang tertulis di `requires:` secara nyata, lalu bandingkan apakah AI tidak membuat fakta baru yang tidak ada di sana. (2) Cari kosakata terlarang di dalam naskah utama (otomatis jika ada `tone_lint.py`, jika tidak ada maka dengan mata). Jika salah satu saja terdeteksi, tolak dan ajukan permintaan ulang sambil menyebut jelas apa yang salah. Penolakan "mendiang istri" pada transcript di atas itulah persis (1).

---

## 5.1.12 Versi Ringkas Solo

Jika Anda developer indie yang membuat sendirian tanpa tim, lima lapis bisa terlihat berlebihan. Cukup dua sekat.

Letakkan satu halaman `vision.md` (gabungan L0+L1), satu folder `content/` (L2), dan satu lembar spreadsheet (L3). Untuk QA, alih-alih lapis tersendiri, gantikan dengan kebiasaan menulis satu baris `requires:` saja pada frontmatter berkas content. Setiap kali menulis quest baru, jika Anda membuka kembali dan membandingkan hanya berkas yang tertulis di `requires`, Anda bisa mencegah insiden Kim tanpa harus mengaduk-aduk 70 halaman. Intinya bukan jumlah lapis, melainkan kebiasaan "memisahkan satu baris yang sama sekali tak berubah lalu menunjukkannya lebih dulu kepada AI setiap kali". Satu baris itulah anchor konteks, dan baik Anda sendirian maupun tim berukuran menengah, mulailah dari sana.

---

### Poin-Poin Penting

- Jika naratif yang paling abstrak bisa terurai menjadi Layer, bidang lain akan mengikuti dengan pola yang sama.
- L0 harus kecil supaya tidak berubah, dan harus tidak berubah supaya menjadi anchor konteks bagi pembuatan dan tinjauan.
- Yang esensial adalah memasang otomatisasi pada antarmuka yang sempit, bukan membagi Layer.
