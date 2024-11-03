# Konfigurasi timesync di OpenWRT

Panduan ini menjelaskan langkah-langkah untuk meng-upload dan menjalankan skrip `timesync` di OpenWRT.

## Fungsi
script ini berfungsi untuk mengambil data jam dan tanggal dari perangkat modem Android untuk set Jam dan tanggal di OpenWRT.

## Prasyarat

- Memiliki perangkat OpenWRT baik router atau STB.
- Sumber internet hanya untuk modem HP yang sudah Auto ADB.
- File `timesync` yang sudah siap di-upload.
- Aplikasi SCP atau FTP untuk transfer file.
- Bisa juga upload langsung melalui web ui OpenWRT.

## Langkah-langkah

1. **Upload File ke OpenWRT**
   - Upload file `timesync` ke direktori `/usr/bin` di OpenWRT.

2. **Set Permission**
   - Buka terminal dan jalankan perintah berikut untuk memberikan hak eksekusi pada file:
     ```bash
     chmod +x /usr/bin/timesync
     ```

3. **Test Program**
   - Ketik perintah berikut di terminal untuk melihat apakah muncul data tanggal dan jam atau error `timesync`:
     ```bash
     timesync
     ```

4. **Periksa Error**
   - Jika terdapat error, segera laporkan issue.
   - Jika tidak ada error dan muncul pemeriksaan jaringan, lanjut ke langkah berikutnya.

5. **Masuk ke Local Startup**
   - Akses menu `System > Startup > Local Startup` di antarmuka web OpenWRT.

6. **Tambahkan Perintah**
   - Di Local Startup biasanya terdapat perintah:
     ```bash
     sleep 3
     /usr/bin/bled -r
     ```

7. **Tambahkan Baris Berikut**
   - Setelahnya, tambahkan:
     ```bash
     sleep 3
     /usr/bin/bled -r
     sleep 3 &&
     timesync &&
     sleep 5 &&
     flymode && (jika anda memilikinya)
     ```

8. **Simpan dan Terapkan**
   - Simpan perubahan dan reboot perangkat.
   - Scriptnya akan berjalan auto di layar belakang.

## Catatan

Pastikan untuk memeriksa semua langkah dengan seksama. Jika Anda mengalami masalah, jangan ragu untuk menghubungi support.

