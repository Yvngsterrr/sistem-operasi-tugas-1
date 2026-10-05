# Laporan Praktikum 1 - Sistem Operasi

**Nama**: NIK ISA BIN NIK HAZIM  
**NIM**: 03041382631180  
**Mata Kuliah**: SISTEM OPERASI  

---

## 1. Proses Instalasi Ubuntu di Komputer Mahasiswa

### Langkah-langkah Instalasi:
1. **Memulai Instalasi**: Membuka Oracle VM VirtualBox dan memuat ISO Ubuntu 14.04 LTS. Memilih opsi bahasa "English" dan memilih **Install Ubuntu**.
   ![Welcome](images/step1_welcome.png)

2. **Memilih Tipe Partisi**: Memilih opsi **"Something else"** untuk melakukan partisi manual terhadap hard disk virtual.
   ![Partition Type](images/step2_something_else.png)

3. **Skema Partisi**:
   - `/dev/sda1`: `swap` (1023 MB)
   - `/dev/sda2`: `ext4` dengan mount point `/home` (5291 MB)
   - `/dev/sda3`: `ext4` dengan mount point `/` (Root) (20526 MB)
   ![Partition Table](images/step3_partitions.png)

4. **Konfigurasi Akun Pengguna**: Mengatur nama pengguna (`mahasiswa`), nama komputer (`mahasiswa-VirtualBox`), dan sandi pengguna.
   ![User Account](images/step4_user.png)

5. **Instalasi Selesai**: Menjalankan sistem operasi Ubuntu 14.04 LTS yang telah berhasil dipasang di VirtualBox.
   ![Desktop](images/step5_desktop.png)

---

## 2. Analisis Mount Point `/` (Root)

**Pertanyaan:** Analisislah kenapa saat instalasi perlu dipilih `/` pada opsi Mount Point?

**Jawaban:**  
Simbol `/` merepresentasikan direktori akar (root directory) dalam hirarki sistem berkas Linux. Tidak seperti Windows yang membagi partisi menjadi drive letter terpisah (`C:`, `D:`, dsb.), Linux mengorganisasi seluruh direktori dan partisi ke dalam satu struktur hierarki pohon tunggal. Direktori `/` bertindak sebagai batang utama (base of the tree). Seluruh berkas sistem operasi esensial, pustaka (libraries), konfigurasi sistem, dan titik kait direktori lainnya harus berada di bawah `/`. Tanpa partisi yang diarahkan ke `/`, sistem Linux tidak memiliki landasan untuk menyimpan sistem operasi dan tidak akan dapat melakukan proses booting.

---

## 3. Penjelasan Jenis Sistem Berkas (Filesystem)

- **ext4 (Extended Filesystem 4)**:  
  Sistem berkas standar dan default pada distribusi modern Linux/Ubuntu. Memiliki performa cepat, stabil, dan menggunakan mekanisme *journaling* (pencatatan transaksi aktif) untuk mencegah kerusakan berkas jika terjadi mati listrik secara tiba-tiba.
- **ext3 (Extended Filesystem 3)**:  
  Generasi pendahulu dari ext4. Merupakan versi pertama keluarga ext yang memperkenalkan fitur *journaling*, namun memiliki batasan ukuran berkas/partisi yang lebih kecil serta kecepatan transaksi yang lebih lambat dibanding ext4.
- **swap (Swap Space)**:  
  Ruang cadangan pada media penyimpanan (hard drive/SSD) yang difungsikan sebagai memori virtual. Jika memori fisik (RAM) penuh, Linux memindahkan data atau proses yang tidak aktif ke dalam swap agar sistem terhindar dari kondisi *out-of-memory* atau freeze.
- **NTFS (New Technology File System)**:  
  Sistem berkas standar utama sistem operasi Microsoft Windows. Mendukung partisi berkapasitas besar, pengaturan hak akses berkas (ACL), enkripsi, dan kompresi berkas.
- **FAT32 (File Allocation Table 32)**:  
  Sistem berkas universal yang didukung secara luas oleh Windows, macOS, Linux, televisi, maupun konsol game. Batasan utamanya adalah tidak mendukung ukuran satu berkas lebih dari 4 GB.
- **btrfs (B-Tree File System)**:  
  Sistem berkas modern berbasis *copy-on-write* (CoW) untuk Linux. Mendukung fitur canggih seperti *snapshot* (pencadangan instan titik waktu), *subvolume*, *pooling* media penyimpanan, serta kemampuan *self-healing* untuk mendeteksi dan memperbaiki data yang korup.
