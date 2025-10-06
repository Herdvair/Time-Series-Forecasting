# Time Series Forecasting: Analisis Penjualan Obat Menggunakan Model Auto ARIMA

Dataset : [Link dataset](https://raw.githubusercontent.com/selva86/datasets/master/a10.csv)

# 💡 Latar Belakang Proyek

Proyek ini menyajikan tahapan analisis dan melakukan peramalan (forecasting) time series melalui pengolahan data non-stasioner yang memiliki tren dan musiman yang jelas. Analisis ini mencakup EDA (Exploratory Data Analysis), pengujian stasioneritas, dekomposisi time series,  dan persiapan data sebelum penerapan model forecasting. 

Dataset ini mencakup:
  - Periode data dimulai pada bulan Juli 1991 hingga Juni 2008
  - Ukuran dimensi data yaitu 204 baris dan 2 kolom

# 🔬 Exploratory Data Analysis (EDA)

1. Tren (Trend)
    Data menunjukkan tren positif yang jelas, di mana nilai penjualan meningkat secara konsisten seiring waktu, menandakan adanya pertumbuhan permintaan.
2. Musiman (Seasonality)
   Terlihat adanya pola musiman yang berulang setiap tahun. Penjualan cenderung menurun di awal tahun dan perlahan-lahan meningkat hingga mencapai puncak di akhir tahun. Pengecekan menggunakan pustaka darts untuk mengidentifikasi periode musiman (seasonal period) sebesar 10.
3. Varian
   Grafik menunjukkan varians yang meningkat seiring dengan naiknya tren, yang menunjukkan bahwa amplitudo musiman bersifat proporsional terhadap tingkat tren.
4. Dekomposisi
   Pemisahan komponen time series menunjukkan bahwa data memiliki pola multiplikatif (Multiplicative Model).

# 📉 Stasioneritas Data
Data teridentifikasi tidak stasioner (non-stationer), yang merupakan tantangan utama untuk pemodelan forecasting tradisional. Hasil ini diperoleh melalui uji Dickey-Fuller
  - Tes Dickey-Fuller:
      - Nilai p-value = 1.000000 (lebih besar dari 0.05), yang menunjukkan data tidak stasioner.
      - Nilai Test Statistic (3.145186) lebih besar dari nilai-nilai kritis (misalnya, -3.465620 pada 1%), yang juga membuktikan kegagalan menolak hipotesis nol (H0) bahwa data tidak stasioner.

# 🛠️ Preprocessing dan Pemodelan
Untuk mengatasi masalah non-stasioneritas dan pola multiplikatif, dilakukan langkah-langkah berikut:
1. Differencing

  **Berdasarkan grafik "Stationary Test"**, data deret waktu yang sudah di-differencing (garis biru) menunjukkan bahwa tren dan musiman telah berhasil dihilangkan. Hal ini ditunjukkan oleh (rolling mean) yang konstan dan mendekati nol (garis hijau), serta (rolling standard deviation) yang stabil (garis merah), meskipun ada sedikit fluktuasi. Secara visual, ini mengonfirmasi bahwa data sudah memenuhi syarat stationer, yaitu rata-rata dan varians yang konstan.

**Hasil uji Dickey-Fuller secara statistik** juga mendukung kesimpulan tersebut. Nilai Test Statistic (-3.799575) lebih kecil dari semua Critical Value pada tingkat 1%, 5%, dan 10%. Selain itu, p-value (0.002912) yang jauh di bawah ambang batas 0.05 memungkinkan kita untuk menolak hipotesis nol, yang menyatakan bahwa data tidak stasioner. Dengan demikian, kedua hasil, baik visual maupun statistik, secara konsisten membuktikan bahwa data Anda telah berhasil menjadi stasioner dan siap untuk pemodelan forecasting.

2. Log Transformation

  **Berdasarkan grafik "Stationary Test", menunjukkan bahwa data tidak stasioner**. Garis biru (Original) dan hijau (Rolling Mean) menunjukkan tren naik yang jelas, artinya rata-rata data tidak konstan seiring waktu. Meskipun garis merah (Rolling Std) terlihat relatif stabil, adanya tren pada rata-rata sudah cukup untuk menyimpulkan bahwa data ini tidak stasioner. 
  
  **Hasil uji Dickey-Fuller** secara statistik juga mengonfirmasi bahwa data tidak stasioner. Nilai Test Statistic (-0.988733) lebih besar dari semua Critical Value , dan p-value (0.757351) jauh lebih besar dari ambang batas 0.05. Ini berarti kita gagal menolak hipotesis nol, yang menyatakan bahwa data tidak stasioner. Oleh karena itu, data ini perlu melalui proses preprocessing seperti differencing combination pada metode moving average.
  
3. Moving Average

  **Berdasarkan grafik "Stationary Test"**, data original (garis biru) menunjukkan rolling mean (garis hijau) yang stabil di sekitar nol, mengindikasikan bahwa tren telah berhasil dihilangkan. Begitu juga dengan rolling standar deviasi (garis merah) yang konstan. Secara visual, grafik ini memperlihatkan bahwa data ini telah memenuhi kriteria stasioner, yaitu rata-rata dan varians yang konstan dari waktu ke waktu.

  **Hasil uji Dickey-Fuller** secara statistik juga mendukung kesimpulan tersebut. Nilai Test Statistic (-4.090266) lebih kecil dari Critical Value pada tingkat 1%, 5%, dan 10%, yang memungkinkan kita untuk menolak hipotesis nol (bahwa data tidak stasioner). Selain itu, p-value (0.001005) yang sangat kecil (jauh di bawah 0.05) memberikan bukti kuat bahwa data ini sudah stasioner. Oleh karena itu, data ini sudah siap untuk digunakan dalam pemodelan forecasting lebih lanjut.

# 🤖 Pemodelan & Hasil
![Model Auto Arima](https://github.com/Herdvair/Time-Series-Forecasting/blob/main/AUTO-ARIMA.png)
Wawasan : 
Model AutoARIMA telah berhasil memprediksi data dengan akurat. Grafik "Original Data" dan "Full Forecast" menunjukkan bahwa garis prediksi (biru) secara ketat mengikuti pola data asli (hitam), termasuk fluktuasi naik-turun yang kompleks. Korelasi ini diperkuat oleh nilai RMSE (Root Mean Squared Error) sebesar 0.1651. Angka ini menunjukkan rata-rata kesalahan prediksi model autoARIMA adalah sekitar 0.1651. Berdasarkan skala asli pada data original antara 2.8 hingga 29.6, RMSE 0.1651 merupakan nilai yang sangat rendah, membuktikan bahwa model ini memiliki akurasi baik dalam forecasting time series ini.





