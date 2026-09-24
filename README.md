# Laporan Praktikum: Pemrograman C# dengan .NET

Laporan ini berisi dokumentasi dua latihan pemrograman C# yang dikerjakan pada mata kuliah Pemrograman Berbasis Kerangka Kerja (PBKK), yaitu latihan pengenalan project console pertama (**Hello World**) dan latihan pembuatan aplikasi **Sistem Data Mahasiswa**.

## Latihan 1: Hello World

Latihan pertama dilakukan saat membuat project console baru di Visual Studio. Tujuannya adalah memahami struktur dasar sebuah program C#, mulai dari `namespace`, `class`, hingga method `Main` sebagai titik masuk (*entry point*) program.

### Kode Program

```csharp
Console.WriteLine("Hello, World!");
```

### Penjelasan Kode

`Console.WriteLine("Hello, World!");` — perintah untuk mencetak teks `Hello, World!` ke layar console, diikuti baris baru.

### Hasil Program

Saat dijalankan, program ini menampilkan tulisan `Hello, World!` di jendela console.

<img width="175" height="47" alt="Screenshot 2026-09-24 161144" src="https://github.com/user-attachments/assets/67ae8162-c493-416c-941c-460287b5a9d2" />

---

## Latihan 2: Sistem Data Mahasiswa

Latihan kedua adalah membangun aplikasi console yang lebih kompleks: **Sistem Data Mahasiswa**. Program ini menerapkan konsep Object-Oriented Programming (OOP), koleksi data (`List`), perulangan, percabangan, dan validasi input.

### Fitur Program

1. **Tambah Mahasiswa** — menambahkan data mahasiswa baru (NIM, Nama, Program Studi, IPK).
2. **Tampilkan Mahasiswa** — menampilkan seluruh data mahasiswa dalam bentuk tabel.
3. **Cari Mahasiswa** — mencari data mahasiswa berdasarkan NIM.
4. **Hapus Mahasiswa** — menghapus data mahasiswa berdasarkan NIM.
5. **Keluar** — mengakhiri program.

### Struktur Program

#### 1. Class `Mahasiswa`

```csharp
class Mahasiswa
{
    public string NIM { get; set; }
    public string Nama { get; set; }
    public string Prodi { get; set; }
    public double IPK { get; set; }

    public Mahasiswa(string nim, string nama, string prodi, double ipk)
    {
        NIM = nim;
        Nama = nama;
        Prodi = prodi;
        IPK = ipk;
    }
}
```

Class ini berfungsi sebagai **blueprint** (cetakan) untuk merepresentasikan satu data mahasiswa. Setiap mahasiswa memiliki empat atribut: `NIM`, `Nama`, `Prodi`, dan `IPK`, yang disimpan menggunakan **property** (`get; set;`) agar nilainya dapat dibaca dan diubah dengan aman. Constructor digunakan untuk mengisi nilai-nilai tersebut saat objek `Mahasiswa` baru dibuat.

#### 2. Penyimpanan Data dengan `List<Mahasiswa>`

```csharp
static List<Mahasiswa> daftarMahasiswa = new List<Mahasiswa>();
```

Seluruh data mahasiswa yang diinput disimpan sementara di dalam sebuah `List`. List dipilih karena ukurannya dinamis — bisa bertambah atau berkurang sesuai jumlah data yang ditambah atau dihapus pengguna. Perlu dicatat, data ini hanya tersimpan **selama program berjalan** (di memori) dan akan hilang saat program ditutup, karena belum ada fitur penyimpanan ke file atau database.

#### 3. Menu Utama dan Perulangan `do-while`

```csharp
do
{
    TampilkanMenu();
    // ... ambil input pilihan ...
    switch (pilihan)
    {
        case 1: TambahMahasiswa(); break;
        case 2: TampilkanMahasiswa(); break;
        case 3: CariMahasiswa(); break;
        case 4: HapusMahasiswa(); break;
        case 5: /* keluar */ break;
        default: /* pilihan salah */ break;
    }
} while (pilihan != 5);
```

Program menggunakan perulangan `do-while` agar menu terus muncul berulang kali sampai pengguna memilih opsi keluar (angka 5). Struktur `switch-case` digunakan untuk mengarahkan program ke method yang sesuai berdasarkan pilihan pengguna. Validasi `int.TryParse` dipakai supaya program tidak crash jika pengguna memasukkan input yang bukan angka.

#### 4. Method `TambahMahasiswa()`

Method ini meminta input NIM, Nama, Program Studi, dan IPK dari pengguna. Untuk IPK, terdapat validasi menggunakan perulangan `while (true)` yang memastikan nilai yang dimasukkan berupa angka antara 0 sampai 4 — jika tidak valid, pengguna akan diminta memasukkan ulang. Setelah semua data valid, objek `Mahasiswa` baru dibuat dan ditambahkan ke `daftarMahasiswa` menggunakan `.Add()`.

#### 5. Method `TampilkanMahasiswa()`

Method ini menampilkan seluruh isi `daftarMahasiswa` dalam format tabel menggunakan `foreach`. Format tampilan diatur dengan *string formatting* (`{0,-12}`, `{3,5:F2}`, dsb.) agar setiap kolom rapi sejajar. Jika belum ada data yang tersimpan, program menampilkan pesan "Belum ada data mahasiswa."

#### 6. Method `CariMahasiswa()`

Program mencari mahasiswa berdasarkan NIM yang diinput menggunakan `foreach` dan perbandingan string `.Equals(..., StringComparison.OrdinalIgnoreCase)`, yang membuat pencarian tidak sensitif terhadap huruf besar/kecil. Jika ditemukan, seluruh data mahasiswa tersebut ditampilkan; jika tidak, muncul pesan bahwa data tidak ditemukan.

#### 7. Method `HapusMahasiswa()`

Mirip dengan pencarian, method ini mencari mahasiswa berdasarkan NIM, kemudian jika ditemukan, data tersebut dihapus dari `daftarMahasiswa` menggunakan `.Remove()`.

### Hasil Program

Berikut adalah tangkapan layar hasil menjalankan setiap fitur program:

**1. Tampilan Menu Utama**

<img width="507" height="251" alt="Screenshot 2026-09-24 161529" src="https://github.com/user-attachments/assets/69d6d674-4287-48be-890a-6864dd7a76b0" />

**2. Tambah Mahasiswa**

<img width="507" height="290" alt="Screenshot 2026-09-24 161656" src="https://github.com/user-attachments/assets/41501843-cad0-4ee0-817f-5247f7714fec" />

**3. Tampilkan Data Mahasiswa**

<img width="752" height="275" alt="Screenshot 2026-09-24 161742" src="https://github.com/user-attachments/assets/a00bae3f-c1b5-478a-a531-1b71bdb37480" />

**4. Cari Mahasiswa**

<img width="510" height="313" alt="Screenshot 2026-09-24 161809" src="https://github.com/user-attachments/assets/78487c2e-557e-4798-be3b-4a883ee4ec6e" />

**5. Hapus Mahasiswa**

<img width="513" height="231" alt="Screenshot 2026-09-24 161839" src="https://github.com/user-attachments/assets/8f2f212a-15f5-496d-a1c8-af05e4d92625" />

**6. Keluar**

<img width="511" height="300" alt="Screenshot 2026-09-24 161936" src="https://github.com/user-attachments/assets/65ca6474-a949-46c5-a462-e939c29182b5" />

---

## Kesimpulan

Melalui dua latihan ini, dapat dipahami alur dasar pengembangan aplikasi console dengan C#, mulai dari struktur program paling sederhana (Hello World) hingga aplikasi yang lebih kompleks dengan konsep OOP (class dan object), koleksi data (`List`), validasi input, serta operasi dasar pengelolaan data (tambah, tampil, cari, hapus) yang menjadi fondasi penting sebelum mempelajari penyimpanan data permanen (file/database) dan pengembangan antarmuka yang lebih interaktif.
