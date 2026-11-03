# customer-segmentation
# Segmentasi Pelanggan Retail Fashion

Analisis kelompok pelanggan toko fashion menggunakan Python dan Pandas
di Google Colab.

## Latar Belakang
Toko ingin mengenali kelompok pelanggan agar strategi promosi lebih tepat.

## Pertanyaan Bisnis
1. Kelompok pelanggan mana yang paling bernilai?
2. Apakah umur, kategori, langganan, atau diskon memengaruhi nilai belanja?

## Data
3.900 pelanggan dan 18 kolom (umur, gender, kategori, nilai belanja,
frekuensi belanja, pembelian sebelumnya, status langganan, diskon, dll).
Hasil pemeriksaan: tanpa missing value dan tanpa baris duplikat.

## Metode
- Pemeriksaan kualitas data (`info`, `isnull`, `duplicated`, `describe`)
- Pengelompokan umur dengan `pd.cut`
- Segmentasi berdasarkan perilaku: frekuensi belanja (dikonversi ke skor)
  dan jumlah pembelian sebelumnya, dengan aturan buatan sendiri
- Perbandingan nilai belanja antar kelompok dengan `groupby`

## Segmen Pelanggan
| Segmen | Pelanggan | % Pelanggan | Rata-rata Belanja | % Belanja |
|---|---|---|---|---|
| Berpotensi | 1.171 | 30,0% | $60,0 | 30,1% |
| Jarang Beli | 1.101 | 28,2% | $59,8 | 28,3% |
| Loyal | 843 | 21,6% | $60,0 | 21,7% |
| Baru Aktif | 785 | 20,1% | $59,1 | 19,9% |

Aturan segmen: Loyal = skor frekuensi >= 4 dan pembelian sebelumnya >= 25;
Berpotensi = pembelian sebelumnya >= 25 saja; Baru Aktif = skor frekuensi
>= 4 saja; Jarang Beli = sisanya.

## Temuan
1. Nilai belanja per transaksi hampir seragam (sekitar $59-60) di
   semua umur, kategori, segmen, status langganan, dan diskon.
2. Clothing menyumbang sekitar 44,7% total belanja ($104.264 dari
   $233.081) karena jumlah transaksinya terbanyak (1.737), bukan
   karena harga lebih tinggi (rata-rata $60,0, sama dengan kategori lain).
3. Segmen terbesar: Berpotensi (30,0% pelanggan, 1.171 orang), diikuti
   Jarang Beli (28,2%), Loyal (21,6%), dan Baru Aktif (20,1%).
4. Porsi belanja tiap segmen hampir sama dengan porsi pelanggannya
   (selisih maksimal 0,2 poin), jadi tidak ada segmen yang jauh
   lebih bernilai per transaksi.
5. Diskon tidak menaikkan rata-rata belanja ($59,3 dengan diskon vs
   $60,1 tanpa diskon).

## Rekomendasi
- Fokus meningkatkan frekuensi pembelian (mengubah "Berpotensi" menjadi
  "Loyal"), bukan nominal per transaksi.
- Uji dampak diskon pada jumlah pembeli, bukan hanya pada nilai belanja.

## Keterbatasan
- Satu baris per pelanggan dan nilai belanja per transaksi, sehingga total
  nilai seluruh riwayat pelanggan tidak bisa dihitung.
- Tidak ada data waktu, jadi tidak ada analisis tren.
- Batas segmen (25 pembelian, skor frekuensi 4) ditetapkan sendiri.
- Pola sangat seragam, kemungkinan data sintetis.
- Tidak ada uji signifikansi statistik.
