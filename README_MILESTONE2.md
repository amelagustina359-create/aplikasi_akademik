# LAPORAN PRAKTIK MILESTONE 2 – CRUD APLIKASI AKADEMIK

**Nama / NIM :** Amelia Agustina / 701240083
**Tautan GitHub :** (isi link repositori)
**AI Tools Dipakai :** Claude
**Fitur Kustomisasi :** [ ] Opsi 1 (Live Search)  [ ] Opsi 2 (Ringkasan)  [x] Opsi 3 (Undo)

## 1. Jejak Prompt AI (Minimal 3 Prompt)

1. **Prompt 1 (Model/Struktur):** "Bagaimana membuat struktur folder ini di proyek Flutter?" (models, services, widgets, screens di dalam lib)
   → Penyesuaian yang dilakukan sendiri: Folder sempat terbuat di luar `lib` karena perintah `cd lib` gagal. Saya hapus, membuat proyek Flutter dengan benar, lalu membuat ulang keempat folder di dalam `lib`. Saya juga menambahkan properti `ipk` pada model Mahasiswa dan `dosenPengampu` pada model MataKuliah, menambah seed data menjadi 3 mahasiswa dan 3 mata kuliah, serta membuat validator IPK (0.0 sampai 4.0).

2. **Prompt 2 (Form Dual-Mode / CRUD):** Saya mengirim log error kompilasi dari `dashboard_screen.dart` (Type 'Mahasiswa' not found, Undefined name 'setState', 'context', 'Navigator') dan meminta bantuan memperbaikinya.
   → Penyesuaian yang dilakukan sendiri: Saya memahami bahwa fungsi CRUD harus berada di dalam class `_DashboardScreenState`, bukan di luar class. Saya lalu membangun Dashboard dengan NavigationBar 2 tab (Mahasiswa dan Mata Kuliah), halaman Detail Mahasiswa, form dual-mode untuk mahasiswa dan mata kuliah, SnackBar setelah tambah/edit/hapus, serta Empty State.

3. **Prompt 3 (Debugging / Fitur Tambahan):** "Because aplikasi_akademik requires SDK version ^3.13.4, version solving failed."
   → Error yang sempat muncul & solusinya: Versi Dart di laptop saya 3.13.2, sedangkan `pubspec.yaml` meminta ^3.13.4. Solusinya mengubah `sdk: ^3.13.4` menjadi `sdk: ^3.13.2` di `pubspec.yaml`. Untuk fitur Undo, saya menambahkan pengecekan `if (!mounted) return;` pada tombol URUNGKAN agar aman jika halaman sudah tidak aktif.

## 2. Pertanyaan Verifikasi Pemahaman

**1. Mengapa pada mode Edit kita mengisi nilai awal TextEditingController di dalam initState(), bukan di dalam build()?**

`initState()` hanya dipanggil satu kali, yaitu saat halaman form pertama kali dibuat, jadi data lama cukup dimasukkan ke kolom sekali saja. Sedangkan `build()` dipanggil berulang kali setiap ada `setState()` atau layar digambar ulang. Kalau data lama diisi di `build()`, teks yang sedang diketik pengguna akan tertimpa data lama lagi setiap layar dibangun ulang.

**2. Bagaimana kode di DashboardScreen membedakan apakah data dari Form harus ditambahkan (Create) atau menimpa data lama (Update)?**

Dibedakan lewat parameter `mhsEdit` (untuk mata kuliah `mkEdit`). Kalau nilainya `null`, berarti form dibuka lewat tombol Tambah, sehingga data hasil form dimasukkan dengan `.add()`. Kalau nilainya berisi data, berarti mode Edit, sehingga posisi data lama dicari dengan `indexWhere` berdasarkan `id`, lalu ditimpa di posisi yang sama dengan `_daftar[idx] = hasil`. Karena `id` tidak berubah dan data menimpa posisi lama, tidak muncul kartu ganda.

**3. Apa yang terjadi jika pada AlertDialog hapus, pengguna mengetuk area gelap di luar kotak dialog?**

Dialog akan tertutup dan `showDialog<bool>` mengembalikan `null`, bukan `true` atau `false`. Di kode saya hasilnya dicek dengan `return yakin == true`, sehingga `null` dianggap `false`. Artinya hasilnya sama dengan menekan tombol Batal: dialog tertutup dan tidak ada data yang dihapus.

## 3. Hasil Code Review Sejawat

**Nama Reviewer:** Zahratul Diniah
**Catatan/Saran:** (isi catatan dari Zahratul setelah dia mencoba aplikasimu)