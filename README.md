# data_wizards
Final Project Bootcamp Academy Batch 31 - Team 9

## EDA

![messageImage_1681052869138](https://user-images.githubusercontent.com/123848730/230780972-d9b43af5-c327-4e37-9630-8aa41dea72c2.jpg)

Insight:
- Jumlah nasabah yang mampu membayar pinjaman (PIF) lebih banyak dibandingkan yang tidak mampu membayar pinjaman (CHGOFF).
- Peningkatan jumlah pinjaman dimulai pada tahun 1998, dan frekuensi tertinggi berada kisaran tahun 2003-2007
- Pinjaman di Bank seluruh Amerika Serikat dari data SBA dimulai dari tahun 1984 hingga 2014, namun data > 2010 dihapus karena data didominasi oleh unfinished loans (data dengan DisbursementFY > 2010 dan Term > 48) sebanyak 80% atau pinjaman belum dapat diputuskan default atau tidak.
- Terjadi kenaikan jumlah pinjaman sebelum 2007 , namun terjadi penurunan yang signifikan jumlah pinjaman setelah Desember 2007, hal ini disebabkan oleh Great Recession (Desember 2007 - Juni 2009).
- Pada tahun 1998 dimulai era transformasi industri 3.0, sehingga banyak pinjaman yang dicairkan, namun pada 2007 terjadi resesi ekonomi di US sehingga terjadi penurunan dan puncak default pembayaran akibat resesi.


![messageImage_1681052911250](https://user-images.githubusercontent.com/123848730/230780967-1e86708d-38dd-4b06-8f55-e50edf30001a.jpg)

Insight:
- Secara keseluruhan, pengajuan pinjaman paling banyak berasal dari Negara Bagian CA (California).

Dilakukan analisis yang lebih spesifik untuk pinjaman pada tahun 2007-2009 (Great Recession) berdasarkan State:
Lima State dengan default (MIS_status = CHGOFF) terbanyak selama Great Recession:
- Florida, Arizona, Nevada, Georgia, dan Michigan
Lima State dengan default (MIS_status = CHGOFF) paling sedikit selama Great Recession:
- Wyowing, Montana, North Dakota, South Dakota, dan Vermont

![messageImage_1681053418014](https://user-images.githubusercontent.com/123848730/230781194-041a299a-f25e-4c95-a38c-e8bdd83371c4.jpg)


Selama Great Recession di Florida (State dengan default terbanyak), pinjaman yang default didominasi oleh: Retail Trade (512 pinjaman), Construction (423 pinjaman), Prof/Science/Tech (398 pinjaman), Wholesale Trade(319 pinjaman), dan other no pb (299 pinjaman). Dapat disimpulkan bahwa tipe Industri tersebut paling terdampak oleh Great Recession di Florida.


![messageImage_1681053433786](https://user-images.githubusercontent.com/123848730/230781294-c5aa7caa-d139-42cd-992f-a45694dfae6b.jpg)

Selama Great Recession di Wyoming (State dengan default paling sedikit), pinjaman yang default didominasi oleh: Constraction (8 pinjaman), Retail Trade (7 pinjaman), Wholesale Trade (3 pinjaman), Manufacturing (2 pinjaman), dan other no pub (2 pinjaman).

## Data Pre-processing

Intinya ini mau dibersihin datanya. Caranya ya bertahap:

1. Pertama melakukan pembersihan data, sesuai yang diajarkan di kelas, seperti:
- Handle missing values
- Handle duplicated data
- Handle outliers
- Feature transformation
- Feature encoding
- Handle class imbalance

2. Kedua mengecek feature yang ada sekarang, lalu lakukan:
- Feature selection (membuang feature yang kurang relevan atau redundan)
- Feature extraction (membuat feature baru dari feature yang sudah ada)
- Tuliskan minimal 4 feature tambahan (selain yang sudah tersedia di dataset) yang mungkin akan sangat membantu membuat performansi model semakin bagus.

Hasil Handle missing values dan duplicated data relatif aman, karena data yang hilang tinggal didrop aja. Terus 1 kolom yang datanya hampir 80% juga dihapus semua kolomnya. Tidak ada data duplikat juga disini.

Handle outliers menggunakan z-scoring dengan meng-keep data yang memiliki z-score dibawah 3. Hasilnya relatif baik untuk data numerik. Hasilnya yang dibuang akibat outlier sekitar 4%. Selanjutnya data finance seperti `DisbursementGross`, `BalanceGross`, `ChgOffPrinGr`, `GrAppv`, `SBA_Appv` dan data numerik lainnya seperti `ApprovalFY`, `Term`, `NoEmp`, `CreateJob`, `RetainedJob` akan ditransformasi logaritmik. Tujuan dari transformasi ini untuk merubah bentuk distribusi mendekati normal.

Feature encoding yang dilakukan yaitu:
- NewExist --> create 'New Business: 1/0
- FranchiseCode --> create 'IsFrenchise'
- RevLineCr --> boolean 0/1
- 'LowDoc'--> boolean 0/1
- 'MIS_Status' --> create 'Default'
- NAICS --> Industry

Feature extraction dan Feature selection dapat dilihat di codingnya aja yaa hehe
