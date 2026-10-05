# -Perbedaan-Synchronous-dan-Asynchronous

Synchronous vs Asynchronous

Synchronous (atau sinkronus) adalah segala sesuatu yang terjadi secara bersamaan (real-time) atau pada waktu yang sama, meskipun orang-orangnya berada di tempat yang berbeda

Asynchronous (atau asinkron) adalah suatu proses, komunikasi, atau eksekusi yang tidak terjadi secara bersamaan atau tidak membutuhkan waktu yang sama (memiliki jeda waktu)

Perbedaan utama antara sinkronus dan asinkronus terletak pada waktu interaksi: sinkronus terjadi secara langsung (real-time), sedangkan asinkronus bersifat tertunda atau fleksibel 




contoh nya

Synchronous (Sinkron)
Proses ini berjalan secara berurutan dan real-time. Kamu harus menunggu satu tugas selesai sepenuhnya sebelum bisa melanjutkan ke tugas berikutnya.

Kehidupan Sehari-hari: Menelepon teman. Saat kamu bertanya, kamu berhenti dan menunggu temanmu menjawab saat itu juga sebelum kamu berbicara lagi.

Belajar/Kerja: Rapat lewat Zoom atau kelas tatap muka, di mana semua orang harus hadir di waktu yang sama dan berinteraksi secara langsung.

Teknologi: Menggunakan mesin ATM. Kamu memasukkan kartu, pin, dan nominal, lalu mesin memprosesnya. Kamu tidak bisa melakukan transaksi lain di mesin tersebut sampai uang dan kartumu keluar.

Asynchronous (Asinkron)
Proses ini berjalan secara mandiri dan tidak mengharuskanmu menunggu balasan langsung. Kamu bisa memulai satu tugas, lalu lanjut mengerjakan hal lain sambil menunggu tugas pertama selesai di latar belakang.

Kehidupan Sehari-hari: Mengirim pesan WhatsApp atau Email. Kamu mengirim pesan, lalu bisa pergi makan atau mengerjakan hal lain. Penerima pesan bebas membalasnya kapan saja.

Belajar/Kerja: Mengerjakan tugas kelompok menggunakan Google Docs di waktu yang berbeda-beda, atau menonton rekaman video pelajaran yang bisa diputar kapan saja.

Teknologi: Mengunduh file besar dari internet. Kamu menekan tombol download, lalu sistem akan mengunduhnya di latar belakang sementara kamu tetap bebas membuka tab baru dan menonton YouTube.




Tiga Cara Menulis Kode Asynchronous di JavaScript

1. **Callbacks**
Cara paling awal dalam menangani operasi asinkron. Sebuah fungsi disisipkan sebagai argumen ke fungsi lain untuk dieksekusi (di-*call back*) setelah tugas utama selesai. Kelemahan utamanya adalah risiko *callback hell*—kode bersarang yang sulit dibaca ketika ada banyak operasi yang berurutan.

```javascript
function ambilData(id, callback) {
  setTimeout(() => {
    const data = { id: id, status: "Berhasil" };
    callback(data); // Fungsi dipanggil setelah 1 detik
  }, 1000);
}

// Penggunaan
ambilData(1, (hasil) => {
  console.log(hasil); 
});

```

2. **Promises**
Diperkenalkan pada ES6 untuk membungkus nilai yang mungkin belum tersedia sekarang, tetapi akan *resolved* (berhasil) atau *rejected* (gagal) di masa depan. Promise mengatasi *callback hell* dengan merangkai logika menggunakan metode `.then()` dan `.catch()`.

```javascript
function ambilDataPromise(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ id: id, status: "Berhasil" });
    }, 1000);
  });
}

// Penggunaan
ambilDataPromise(1)
  .then((hasil) => console.log(hasil))
  .catch((error) => console.error(error));

```

3. **Async / Await**
Sintaks modern yang dibangun di atas Promise agar kode asinkron lebih mudah dibaca, layaknya kode sinkron yang berjalan berurutan. Gunakan blok `try...catch` untuk menangani *error*.

```javascript
function ambilDataPromise(id) {
  return new Promise((resolve) => {
    setTimeout(() => resolve({ id: id, status: "Berhasil" }), 1000);
  });
}

// Penggunaan
async function jalankanProses() {
  try {
    // Eksekusi akan "menunggu" sampai Promise selesai
    const hasil = await ambilDataPromise(1);
    console.log(hasil);
  } catch (error) {
    console.error(error);
  }
}

jalankanProses();

```


