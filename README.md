# Admin Warehouse Chatbot Workflow

## Deskripsi Proyek
Workflow ini dirancang untuk mengelola interaksi chatbot admin warehouse melalui Telegram menggunakan platform n8n. Sistem ini memproses input dari Telegram untuk dua fungsi utama: membuat laporan dan menambah data ke database, dengan memanfaatkan kemampuan Google Gemini Chat (Large Language Model) dan Google Sheets.

<img width="1540" height="546" alt="image" src="https://github.com/user-attachments/assets/30ee147b-2dbe-4d40-ab3c-6f7e11952969" />

---

## Cara Kerja Setiap Node

### 1. Telegram Trigger
- Memulai workflow saat ada pesan masuk di Telegram.
- Mengirim data pesan ke node selanjutnya untuk diproses.

### 2. If
- Menyeleksi jalur proses berdasarkan isi pesan.
- Jika pesan sesuai kriteria tertentu, lanjut ke node LLM Report; jika tidak, ke LLM Append Data.

### 3. LLM Report
- Menggunakan Google Gemini Chat untuk membuat laporan dari pesan.
- Menghasilkan output berupa laporan yang akan diproses lebih lanjut.

### 4. Prepare Filter
- Mengolah hasil output menjadi format yang bisa dipakai untuk query data.
- Menyaring data laporan untuk kelancaran proses berikutnya.

### 5. Get Data
- Membaca data dari Google Sheets sesuai filter yang sudah disiapkan.

### 6. Create CSV
- Mengubah data hasil baca menjadi format CSV.
- Memudahkan pengiriman data sebagai file.

### 7. Send a document
- Mengirim file CSV hasil laporan melalui Telegram ke pengguna.

### 8. LLM Append Data
- Memproses input pesan yang berisi data tambahan menggunakan Google Gemini Chat.
- Mempersiapkan data untuk disimpan ke database.

### 9. Validate Data
- Mengecek validitas data hasil proses LLM Append Data.
- Menentukan apakah data sudah sesuai format dan ketentuan.

### 10. Is data valid?
- Memberi cabang alur workflow berdasarkan validitas data.
- Data valid lanjut ke append row, data tidak valid kirim pesan error.

### 11. Append row in sheet
- Menambahkan baris baru dengan data yang valid ke spreadsheet Google Sheets.

### 12. Send Detail Data Added
- Memberi notifikasi di Telegram bahwa data berhasil ditambahkan.

### 13. Send Invalid Format Message
- Mengirim pesan peringatan jika data tidak valid atau format salah.

<img width="376" height="176" alt="image" src="https://github.com/user-attachments/assets/591e51a4-64ef-40d9-9a35-527da300009a" />

---

## Ringkasan Alur Workflow
1. Pesan Telegram diterima di `Telegram Trigger`.
2. `If` memisahkan alur untuk laporan atau penambahan data.
3. Jika laporan: laporan dibuat oleh LLM, data diambil, diubah CSV, dan dikirim sebagai dokumen.
4. Jika tambah data: data diproses, divalidasi, jika valid disimpan dan konfirmasi dikirim, jika tidak valid pesan error dikirim.

---

## Catatan
Dokumentasi ini dibuat untuk memudahkan pengembangan dan pemeliharaan workflow chatbot admin warehouse. Jika ada perubahan dalam alur atau penambahan fitur, README ini perlu diperbarui.

---

Dokumen ini dapat langsung digunakan pada repositori GitHub sebagai panduan bagi developer dan tim.

---

Terima kasih sudah menggunakan workflow ini! 🚀
