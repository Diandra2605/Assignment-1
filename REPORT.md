# Laporan Programming Assignment 1 : Basic C++

# Program Perhitungan Umur dan Hari (C++)

### Diandra Alea Eshan | 5024251057

## Deskripsi
Tugas ini bertujuan untuk membuat program C++ yang dapat menghitung usia pengguna dalam satuan tahun dan bulan, serta menentukan hari lahir (Nama Hari) berdasarkan input tanggal tertentu. Program ini memanfaatkan pustaka waktu standar untuk melakukan sinkronisasi dengan tanggal saat ini di sistem.

## Penjelasan Fungsi
Beberapa komponen teknis utama yang diimplementasikan dalam kode ini adalah:
- Library `<ctime>` & `<sstream>`: Digunakan untuk mengolah data waktu sistem dan memproses string input tanggal menjadi format angka (integer).
- Struktur `tm`: Menggunakan pointer `tm` untuk menyimpan dan memanipulasi detail tanggal seperti tahun, bulan, dan hari.
- Fungsi `yearsOld`: Menghitung selisih tahun antara tanggal input dan tanggal sekarang, dengan pengecekan logika apakah bulan/hari ulang tahun di tahun berjalan sudah terlewati atau belum.
- Fungsi `monthsOld`: Menghitung total akumulasi bulan sejak tanggal lahir hingga saat ini.
- Fungsi `dayOfDate`: Menggunakan fungsi mktime untuk menormalisasi data tanggal dan mengambil indeks hari (tm_wday) guna menentukan nama hari dalam bahasa Indonesia.

## Implementasi Kode Program
```cpp
int yearsOld(tm* inputTgl, tm* currentTgl)
{
    int year = currentTgl->tm_year - inputTgl->tm_year;

    if (currentTgl->tm_mon < inputTgl->tm_mon ||
       (currentTgl->tm_mon == inputTgl->tm_mon && currentTgl->tm_mday < inputTgl->tm_mday))
    {
        year--;
    }

    return year;
}

int monthsOld(tm* inputTgl, tm* currentTgl)
{
    int months = (currentTgl->tm_year - inputTgl->tm_year) * 12;
    months += (currentTgl->tm_mon - inputTgl->tm_mon);

    if (currentTgl->tm_mday < inputTgl->tm_mday)
    {
        months--;
    }

    return months;
}

string dayOfDate(tm* inputTgl)
{
    mktime(inputTgl);

    string days[] = {
        "Minggu", "Senin", "Selasa", "Rabu",
        "Kamis", "Jumat", "Sabtu"
    };

    return days[inputTgl->tm_wday];
}
```

## Contoh

# Input
```
26/05/2007
```
# Output
```
18 226 Sabtu
```

## Kesimpulan
Program ini berhasil menghitung umur dan bulan secara akurat, menentukan hari dari tanggal lahir, dan menggunakan struktur waktu (tm) dalm C++ dengan benar.
