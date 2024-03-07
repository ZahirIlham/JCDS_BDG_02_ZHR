# JCDS_BDG_02_ZHR
# **Latar Belakang**
AWS adalah sebuah perusahaan yang bergerak dibidang penyedia layanan SaaS (*Software as a Service*). Sebagai penyedia layanan berbasis cloud perusahaan melakukan pengelolaan terhadap *platform*, sistem operasi dan perangkat lunak perantara. Model layanan ini berbasis langganan dimana pelanggan dapat menaikkan atau menurunkan layanan sesuai kebutuhan bisnis mereka.

# **Pernyataan Masalah**
Perusahaan mengalami kerugian pada beberapa produk sehingga manajemen ingin mencari tahu "**Faktor Apa Saja yang Mempengaruhi Kinerja Penjualan dan Profitabilitas Berdasarkan Segmen Pelanggan, Produk dan Subregion**". Informasi ini akan membantu perusahaan untuk menetapkan strategi penjualan yang tepat agar kerguian dapat ditekan namun kinerja `Sales` tetap meningkat.

Sebagai seorang *data analyst*, kita diberi tugas untuk menjawab pertanyaan berikut:<br>
**Faktor-faktor apa yang menyebabkan kinerja penjualan dan profitabilitas serta bagaimana strategi untuk menangani berbagai faktor tersebut**

# **Data**
Untuk menjawab pertanyaan di atas, kita akan menganalisa data peserta yang sudah dikumpulkan oleh perusahaan. Dataset dapat diakses [di sini](https://drive.google.com/drive/folders/1dlpJfgvs8P_IyXqWB4WrNwk91fx0XAzU). Untuk Story maupun dashbord menggunakan Tableu dapat dilihat pada link berikut: 
1. [Story](https://public.tableau.com/app/profile/zahir.ilham/viz/Saas-sales_capstone2-zhr/Story1)
2. [Dashboard](https://public.tableau.com/app/profile/zahir.ilham/viz/Saas-sales_Dashboard/Dashboard7?publish=yes)

## **Data Understanding and Cleaning**
Sebelum masuk ke dalam analisis, kita perlu mengenal dataset kita lebih jauh dalam tahapan *data understanding*. Dari proses ini, kita akan tahu anomali-anomali apa saja yang terdapat di dalam dataset kita dan perlu ditangani dalam tahapan *data cleaning*. Setiap penangan anomali yang dilakukan, akan disertai dengan justifikasi langkah yang diambil, baik secara *domain knowledge* maupun secara statistik.

Pertama, mari kita lihat informasi umum dari dataset Saas_Sales.

Dataset ini berisi informasi data transaksi dari sebuah perusahaan penyedia layanan SaaS kepada perusahaan lain (B2B). Pada dataset setiap baris terdapat informasi *transaction/order* (9,994 transaksi), yaitu:

1. Row ID       : Nomer baris dari setiap transaksi.
2. Order ID     : Nomer *unique* dari setiap transaksi.
3. Order Date   : Tanggal pembelian.
4. Date Key     : Tanggal pembelian dengan format (YYYYMMDD).
5. Contact Name : Nama orang yang melakukan pembelian.
6. Country      : Negara tempat pembelian dilakukan.
7. City         : Kota tempat pembelian dilakukan.
8. Region       : Wilayah tempat pembelian dilakukan.
9. Subregion    : Subwilayah tempat pembelian dilakukan.
10. Customer    : Nama Perusahaan yang melakukan pembelian.
11. Customer ID : Nomor ID dari Perusahaan pelanggan.
12. Industry    : Jenis industri dari perusahaan pelanggan.
13. Segment     : Segmen pelanggan (SMB, Strategic, Enterprise, etc.).
14. Product     : Jenis produk yang dibeli.
15. License     : *License key* dari produk yang dibeli.
16. Sales       : Jumlah penjualan dari setiap transaksi.
17. Quantity    : Jumlah produk yang dibeli dari setiap transaksi.
18. Discount    : Diskon yang dikenakan dari setiap transaksi.
19. Profit      : Keuntungan dari setiap transaksi.

### **Check Dupplikat dan Missung Value**

Berdasarkan informasi diatas dapat diketahui bahwa:
1. Terdapat `19` kolom
2. Terdapat `9994` baris
3. Tidak terdapat nilai null pada setiap baris di seluruh kolom.
4. Tidak terdapat duplikat.
5. `Row ID`, `Customer ID` seharusnya bertipe `object`.
6. `Order Date` dan `Date Key` seharusnya bertipe `datetime`.

# **Kesimpulan dan Rekomendasi**
## **Kesimpulan**

Dari analisis yang telah dilakukan, kita bisa membuat kesimpulan:

**Segment dan Industry**

1. Sebanyak **51.9%** pelanggan berasal dari `Segment` *SMB* (*Small to Medium Business*), Artinya lebih dari setengah konsumen berasal dari perusahaan dengan skala bisnis kurang dari 1000 karyawan.
2. `Segment` *SMB (Small to Medium Business)* memberikan kinerja `Sales` dan `Profit` tertinggi, yaitu **$ 134,119.2092**.
3. Profit yang diberikan dari setiap sektor `Industry` tidak berbeda signifikan.

**Product**

1. Top `Sales` produk adalah ContactMatcher, yaitu  **$ 410,378.26**.
2. Top `Profit` produk adalah Alchemy, yaitu  **$ 55,617.8249**.
3. `Product` dengan median kinerja `Profit Margin` rendah (kurang dari 10%) berdasarkan `Segment`, antara lain:
    * *Marketing Suite*
    * *Marketing Suite - Gold*
    * *Big OI Database*
    * *Site Analytics*

**Discount**

1. Terdapat korelasi yang Moderate (**-0.61**) antara `Discount` dengan `Profit` pada produk *Marketing Suite*.
2. *Site Analytics* memiliki kinerja `Sales` yang baik tetapi `Profit Margin` rendah. Hal ini disebabkan oleh:
    - 65.02 % penjualan dikenakan diskon diatas 20%.
    - 34.98% penjualan tidak dikenakan diskon (0%).
3. Frekuensi pemberian profit pada tiap kelompok memiliki pola yang berbeda-beda. Kelompok lower dan midle lebih sering memberikan diskon dengan besaran lebih dari 20%. Sedangkan pada kelompok top margin lebih jarang memberikan diskon (0%).
4. Profit pada `Product`:
    - Kerugian pada produk *Marketing Suite* terjadi ketika pemberian diskon lebih dari 20%.
    - Kerugian pada produk *ContactMatcher* terjadi ketika pemberian diskon lebih dari 30%.
    - Pada produk *Alchemy* maksimal diskon yang diberikan 40% dan pada besaran diskon tersebut median `Profit` masih bernilai positif.
5. Diskon berdasarkan Subregion 
    - Subregion JAPN, ANZ dan EU-WEST memiliki median `Sales` dan `Profit` terendah.
    - Subregion IND, EU dan APAC memiliki median `Sales` dan `Profit` pada posisi teratas.
6. Perbandingan cohort antara lower sales `Subregion`
    - Secara analisis cohort customer pada `Subergion` *lower sales* (*ANZ, JAPN dan EU-WEST*) lebih retain dibandingkan `Subergion` top sales (IND, EU dan APAC).
    - Banyaknya frekuensi pemberian diskon pada Subregion*lower sales* (*ANZ, JAPN dan EU-WEST*)  mengakibatkan peningkatan jumlah pembelian setiap tahunnya.

## **Rekomendasi**
1. Fokus Pada Segmen SMB: 
Karena Segment SMB memiliki total Sales dan Profit tertinggi, disarankan untuk mengalokasikan sumber daya dan upaya pemasaran yang lebih baik untuk meningkatkan pelanggan dari segmen ini. Upaya yang dilakukan bisa mencakup kampanye pemasaran dan peningkatan layanan yang sesuai dengan kebutuhan SMB.

2. Optimalkan Strategi Produk: 
Untuk produk dengan Profit Margin rendah, seperti Marketing Suite, perusahaan perlu meninjau ulang strategi harga dan pemberian diskon. Mungkin ada kebutuhan untuk mengurangi diskon atau meningkatkan nilai produk untuk meningkatkan profitabilitasnya. Seperti menerapkan besaran diskon maksimal diangka 20% dan menaikkan harga minimum dari produk tersebut.

3. Perhatikan Subregion Performa Rendah: 
Subregion seperti JAPN, ANZ, dan EU-WEST memiliki sales dan profit yang lebih rendah. Walaupun pemberian diskon pada subregion ini bertujuan untuk meningkatkan engagement. Perlu dipertimbangkan untuk menetapkan besaran diskon yang terukur. Seperti pemberian diskon diatas 20% hanya untuk pengguna baru ataupun pemberian diskon pada periode tertentu.

4. Perbaiki Retensi Pelanggan: 
Subregion "lower sales" memiliki retention yang lebih baik. Ini menunjukkan potensi untuk memfokuskan upaya retensi pelanggan pada setiap wilayah. Salah satunya dengan memberikan layanan tambahan, program loyalitas, atau dukungan pelanggan yang lebih baik.

5. Analisis Produk dengan Diskon Tinggi: 
Pada beberapa produk akan mulai mengalami kerugian jika memberikan diskon diatas 20% ataupun 30%.<br>
Kita tidak perlu menghapuskan diskon, salah satu strategi yang bisa diterapkan antara lain :
    - Lakukan analisis pada setiap produk, pada besaran berapa produk mulai rugi.
    - Setelah diketahui besaran diskon maksimal produk mulai rugi, tingkatkan frekuensi pemberian diskon dibawah besaran tersebut.
    - Sebagai contoh ContactMatcher mulai merugi pada besaran diskon 30%. Turunkan besaran diskon dibawah nilai tersebut dan tingkatkan frekuensi pemberian diskon pada rentang tersebut.
    - Perhatikan harga minimumnya dan cost dari setiap produk lalu naikkan harga minimumnya.
Rekomendasi ini dapat membantu perusahaan meningkatkan profitabilitasnya, mengoptimalkan strategi pemasaran, dan memfokuskan upaya pada segmen dan wilayah yang memiliki potensi pertumbuhan yang lebih besar.
