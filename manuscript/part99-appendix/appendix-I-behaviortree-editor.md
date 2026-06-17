# Lampiran I. Studi Kasus Editor BehaviorTree (Mendalam)

> Studi kasus mendalam tentang editor BehaviorTree yang dibahas di 7.2. Pengalaman dalam pengambilan keputusan, implementasi, dan pengoperasian pengembangan mandiri.

---

## I.1 Keputusan Pengembangan Mandiri

Rincian dari empat dasar keputusan yang dibahas di 7.2.8.

| Dasar | Rincian |
|---|---|
| diff·pelacakan git wajib | BT di UE berupa binary .uasset, sehingga sulit melacak perubahan. Dengan JSON, diff teks menjadi mungkin |
| referensi subtree + pelacakan dampak | Saat mengoperasikan 100\~300 unit BT, analisis dampak per subtree menjadi penentu |
| verifikasi simulasi | BT dapat dijalankan terpisah tanpa build |
| penulisan dibantu AI | LLM membangkitkan dan menafsirkan BT JSON secara alami |

---

## I.2 Tahap Implementasi

```
[1. Perencanaan·Definisi Kebutuhan (1~2 minggu)]
   - Merumuskan 4 kebutuhan secara tertulis
   - Merancang skema JSON
   
[2. Implementasi Runtime (3~4 minggu)]
   - Parser JSON
   - Mesin eksekusi BT
   - Resolusi referensi subtree
   
[3. Implementasi Editor (4~6 minggu)]
   - Editor JSON (grafis)
   - UI pustaka subtree
   - Alat analisis dampak
   
[4. Simulator (2~3 minggu)]
   - Eksekusi BT terpisah
   - Ekstraksi statistik
   
[5. Integrasi AI (2~3 minggu)]
   - Penulisan BT dibantu LLM
   - Injeksi konteks
   
[6. Integrasi UE (2~4 minggu)]
   - Konversi dengan BT UE
   - Integrasi build
```

Total sekitar 4\~6 bulan. 1\~2 pengembang.

---

## I.3 Desain Operasional dan Antisipasi Insiden

### I.3.1 Mengenai Angka Operasional

Editor ini adalah alat internal pada tahap R&D, dan tidak dioperasikan dalam jangka panjang maupun skala besar yang cukup untuk disebut "pengukuran nyata operasi selama 1 tahun". Karena itu, sesuai prinsip buku ini, di sini saya tidak mencantumkan statistik operasional yang dibuat-buat. Skala 100\~300 unit yang dibahas di I.1 adalah **target desain** yang membenarkan pengembangan mandiri, bukan hasil yang terukur.

Di antara batasan yang dipatok desain, yang benar-benar masuk ke dalam kode adalah **batas depth 5 untuk referensi subtree** (mencegah rekursi tak terbatas). Nilai seperti jumlah BT dan jumlah eksekusi simulasi saat operasi bergantung pada skala proyek, jadi alih-alih menuliskan angka yang dibuat-buat, saya menyarankan Anda mengukurnya sendiri di lingkungan Anda.

### I.3.2 Insiden yang Diantisipasi dalam Operasi dan Pembelajarannya

| Insiden | Pembelajaran |
|---|---|
| referensi subtree tak terbatas (rekursi) | batas depth 5 untuk referensi |
| selisih perilaku simulasi vs. nyata | kalibrasi lingkungan simulasi setiap bulan |
| halusinasi pada BT keluaran LLM | verifikasi + penguatan tinjauan oleh desainer |
| ledakan jumlah BT (di luar rencana) | siklus pembersihan triwulanan |

---

## I.4 Biaya·ROI

Biaya pengembangan dan operasional adalah perkiraan berdasarkan jadwal yang ditetapkan saat membuat alat ini, dan sisi "efek" bukanlah nilai terukur melainkan arah yang ditargetkan melalui penerapan. Alih-alih angka penghematan yang dibuat-buat, saya hanya menuliskan arahnya.

| Item | Nilai | Sifat |
|---|---|---|
| Biaya pengembangan | 4\~6 bulan pengembang | Jadwal rencana (perkiraan) |
| Biaya operasional | 1\~2 minggu pengembang per triwulan (pemeliharaan) | Jadwal rencana (perkiraan) |
| Efek yang ditargetkan — tenaga operasional | Memampatkan jumlah orang penanggung jawab BT saat mengoperasikan NPC musuh dalam skala besar | Arah (belum terukur) |
| Efek yang ditargetkan — insiden | Mengurangi secara struktural insiden BT seperti rekursi subtree·halusinasi LLM | Arah (belum terukur) |

Periode pengembalian biaya penerapan bervariasi tergantung skala NPC dan biaya tenaga kerja proyek, jadi saya menyarankan Anda mengukur item di atas di lingkungan Anda sendiri untuk menilainya. Saya tidak membuat klaim sepihak seperti "akan kembali modal dalam 1 tahun" — angka itu tidak kami miliki.

---

## I.5 Studi Kasus Bantuan LLM

### I.5.1 Penulisan BT NPC Musuh Baru

Menggunakan prompt 7.2.6. Berikut adalah contoh yang menunjukkan struktur keluaran (contoh format, bukan data operasional nyata).

```json
{
  "bt_id": "bt_new_mage_v1",
  "category": "ranged_combatant",
  "tags": ["scholar_faction", "ranged", "magic"],
  "root": {
    "type": "selector",
    "children": [
      {
        "type": "sequence",
        "name": "low_hp_retreat",
        "children": [
          {"type": "condition", "fn": "hp_below", "param": 0.3},
          {"type": "subtree_ref", "id": "subtree_retreat_to_ally"}
        ]
      },
      {
        "type": "sequence",
        "name": "magic_attack",
        "children": [
          {"type": "condition", "fn": "enemy_in_range", "param": 15},
          {"type": "subtree_ref", "id": "subtree_magic_attack_pattern"}
        ]
      }
    ]
  }
}
```

Desainer meninjau lalu simulasi → lolos → diterapkan ke build.

---

## I.6 Catatan untuk Pembaca

Pengembangan mandiri BehaviorTree cenderung dapat dibenarkan pada skala operasi 100 unit+ (pertimbangan desain). Di bawah itu, BT bawaan UE sudah cukup.

Opsi alternatif:
- BehaviorTree.CPP (sumber terbuka, standar)
- Behavior Designer (komersial pihak ketiga)
- Pengembangan mandiri (kebebasan tertinggi, beban operasional)

Untuk kriteria pemilihan, lihat 7.2.8.
