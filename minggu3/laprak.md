# <h1 align="center">Laporan Praktikum Modul 3 <br> Abstract Data Type </h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori

Abstract Data Type (ADT), atau Tipe Data Abstrak, adalah konsep fundamental dalam ilmu komputer yang mendefinisikan sebuah tipe data dari sudut pandang logis atau matematis, bukan dari sudut pandang implementasi fisiknya. ADT adalah spesifikasi tentang apa yang dilakukan oleh suatu tipe data, yang terdiri dari dua komponen utama: koleksi data yang akan disimpan, dan set operasi (fungsi atau metode) yang dapat diterapkan pada data tersebut. . Inti dari ADT adalah abstraksi, di mana kita memisahkan definisi fungsional (antarmuka publik) dari detail implementasi internal (struktur data yang mendasarinya dan kode algoritmik). Misalnya, kita mendefinisikan ADT Stack dengan operasi push (tambah) dan pop (ambil), tanpa peduli apakah Stack tersebut nantinya akan diimplementasikan menggunakan array atau linked list.


## Guided

### guided 1
   ```c++
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);

#endif

```

File MAHASISWA_H_INCLUDED berfungsi sebagai kontrak (interface) untuk modul mahasiswa dalam program C++, dilindungi oleh header guard untuk mencegah pendefinisian ganda. File ini mendefinisikan struktur data mahasiswa yang terdiri dari NIM (char nim[10]), dan dua nilai integer (nilai1 dan nilai2). Selain struktur, file ini mendeklarasikan dua prototipe fungsi: void inputMhs(mahasiswa &m) yang memungkinkan pengguna mengisi data mahasiswa (menggunakan referensi untuk memodifikasi objek), dan float rata2(mahasiswa m) yang bertugas menghitung dan mengembalikan hasil rata-rata dari kedua nilai tersebut dalam tipe data floating point.

### guided 2
   ```c++
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m) .nim;
    cout << "input nilai = ";
    cin >> (m) .nilai1;
    cout << "input niali2 = ";
    cin >> m .nilai2;

}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}

```

Kode  ini mengimplementasikan dua fungsi inti untuk mengelola data mahasiswa yang didefinisikan dalam header mahasiswa.h. Fungsi inputMhs bertugas menerima input dari pengguna (NIM, nilai pertama, dan nilai kedua) dan menyimpannya ke objek mahasiswa melalui referensi. Sementara itu, fungsi rata2 menghitung nilai rata-rata dari kedua nilai tersebut dan mengembalikan hasilnya dalam tipe floating point untuk memastikan presisi desimal.



### guided 3


```c++
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata rata = " << rata2(mhs);
    return 0;
}
```
Kode ini adalah program utama (main) yang memanfaatkan struktur dan fungsi yang dideklarasikan di file header mahasiswa.h dan diimplementasikan di file .cpp lain. Pertama, ia mendeklarasikan objek mhs dari tipe mahasiswa. Selanjutnya, fungsi inputMhs(mhs) dipanggil untuk meminta pengguna memasukkan NIM dan dua nilai (nilai1 dan nilai2) ke dalam objek tersebut. Terakhir, program menghitung dan langsung mencetak hasil rata-rata kedua nilai tersebut menggunakan fungsi rata2(mhs), lalu program diakhiri.




## Unguided

### Soal 1

```c++
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

void inputMahasiswa(Mahasiswa &mhs) {
    cout << "Masukkan Nama       : ";
    getline(cin, mhs.nama);
    cout << "Masukkan NIM        : ";
    getline(cin, mhs.nim);
    cout << "Masukkan Nilai UTS  : ";
    cin >> mhs.uts;
    cout << "Masukkan Nilai UAS  : ";
    cin >> mhs.uas;
    cout << "Masukkan Nilai Tugas: ";
    cin >> mhs.tugas;
    cin.ignore();
    mhs.nilaiAkhir = hitungNilaiAkhir(mhs.uts, mhs.uas, mhs.tugas);
}

void tampilMahasiswa(Mahasiswa mhs[], int jumlah) {
    cout << "Daftar Data Mahasiswa\n";
    cout << "==============================================\n";
    for (int i = 0; i < jumlah; i++) {
        cout << "Mahasiswa ke-" << i + 1 << endl;
        cout << "Nama         : " << mhs[i].nama << endl;
        cout << "NIM          : " << mhs[i].nim << endl;
        cout << "UTS          : " << mhs[i].uts << endl;
        cout << "UAS          : " << mhs[i].uas << endl;
        cout << "Tugas        : " << mhs[i].tugas << endl;
        cout << "Nilai Akhir  : " << mhs[i].nilaiAkhir << endl;
    }
}

int main() {
    Mahasiswa daftarMhs[10];
    int jumlah;

    cout << "Masukkan jumlah mahasiswa (max 10): ";
    cin >> jumlah;
    cin.ignore();

    if (jumlah > 10) {
        cout << "Jumlah melebihi batas maksimum (10)!" << endl;
        return 0;
    }

    for (int i = 0; i < jumlah; i++) {
        cout << "\nInput data mahasiswa ke-" << i + 1 << endl;
        inputMahasiswa(daftarMhs[i]);
    }

    tampilMahasiswa(daftarMhs, jumlah);

    return 0;
}
```
>

Program ini adalah aplikasi sederhana berbasis C++ yang digunakan untuk mengolah data mahasiswa. Pengguna dapat memasukkan informasi seperti nama, NIM, serta nilai UTS, UAS, dan tugas. Data tersebut kemudian diolah untuk menghitung nilai akhir mahasiswa dengan pembobotan 30% untuk UTS, 40% untuk UAS, dan 30% untuk tugas. Setelah semua data dimasukkan, program menampilkan daftar mahasiswa lengkap dengan hasil perhitungan nilai akhirnya. Struktur data struct digunakan untuk menyimpan data tiap mahasiswa, sementara proses input, perhitungan, dan penampilan data dipisahkan ke dalam beberapa fungsi agar program lebih rapi dan mudah dipahami.

### Soal 2

Pelajaran.h
```c++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED

#include <string>

struct pelajaran {
    std::string namaMapel; 
    std::string kodeMapel; 
};

pelajaran create_pelajaran(std::string nama, std::string kode);

void tampil_pelajaran(pelajaran pel);

#endif 
```

Pelajaran.cpp
```c++
#include "pelajaran.h"
#include <iostream>
#include <string>

pelajaran create_pelajaran(std::string nama, std::string kode) {
    pelajaran pelBaru;
    pelBaru.namaMapel = nama;
    pelBaru.kodeMapel = kode;
    return pelBaru;
}

void tampil_pelajaran(pelajaran pel) {
    std::cout << "nama pelajaran : " << pel.namaMapel << std::endl;
    std::cout << "nilai : " << pel.kodeMapel << std::endl; 
} 
```

main.cpp
```c++
#include "pelajaran.h"
#include <iostream>
#include <string>

using namespace std;

int main() {
    string namaMapel = "Struktur Data";
    string kodeMapel = "STD";
    
    pelajaran pel = create_pelajaran(namaMapel, kodeMapel);
    
    tampil_pelajaran(pel);

    return 0;
}
```
Kode ini berfungsi sebagai program utama (main) yang menguji implementasi Abstract Data Type (ADT) pelajaran, yang didefinisikan dalam file header pelajaran.h. Program dimulai dengan menginisialisasi dua variabel string, namaMapel dengan nilai "Struktur Data" dan kodeMapel dengan nilai "STD". Selanjutnya, ia memanggil fungsi create_pelajaran untuk membuat dan menginisialisasi sebuah objek pelajaran baru (pel) menggunakan dua string tersebut, yang menunjukkan penggunaan dari fungsi konstruksi ADT. Terakhir, program memanggil prosedur tampil_pelajaran untuk mencetak data yang disimpan dalam objek pel ke konsol, yang merupakan demonstrasi dari fungsi akses atau display ADT tersebut.

### Soal 3

Pelajaran.h
```c++
#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

void tukarNilai(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

void tukarPosisi(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int ArrayA[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int ArrayB[3][3] = {
        {10, 11, 12},
        {13, 14, 15},
        {16, 17, 18}
    };

    cout << "Array A sebelum ditukar:\n";
    tampilArray(ArrayA);
    cout << "\nArray B sebelum ditukar:\n";
    tampilArray(ArrayB);

    tukarPosisi(ArrayA, ArrayB, 1, 1);

    cout << "\nSetelah menukar elemen pada posisi [1][1]:\n";
    cout << "Array A:\n";
    tampilArray(ArrayA);
    cout << "\nArray B:\n";
    tampilArray(ArrayB);

    int nilaiX = 50, nilaiY = 100;
    int *ptr1 = &nilaiX;
    int *ptr2 = &nilaiY;

    cout << "\nNilai sebelum ditukar melalui pointer:\n";
    cout << "nilaiX = " << nilaiX << ", nilaiY = " << nilaiY << endl;

    tukarPointer(ptr1, ptr2);

    cout << "Nilai setelah ditukar melalui pointer:\n";
    cout << "nilaiX = " << nilaiX << ", nilaiY = " << nilaiY << endl;

    return 0;
}
```

Kode ini mendemonstrasikan berbagai mekanisme pertukaran nilai menggunakan fungsi dan array dua dimensi berukuran 3x3. Fungsi tampilArray digunakan untuk mencetak isi array 2D; tukarNilai menukar dua nilai integer melalui reference (digunakan untuk pemahaman konsep, meskipun tidak dipanggil di main); tukarPosisi menukar elemen pada indeks tertentu ([1][1]) antara dua array (ArrayA dan ArrayB). Di main, setelah pertukaran posisi, nilai [1][1] pada ArrayA menjadi 14 dan pada ArrayB menjadi 5. Selain itu, fungsi tukarPointer menunjukkan pertukaran nilai antara dua variabel (nilaiX dan nilaiY) secara tidak langsung menggunakan pointer (ptr1 dan ptr2), di mana nilai akhir nilaiX menjadi 100 dan nilaiY menjadi 50, membuktikan bahwa fungsi berhasil memanipulasi data yang ditunjuk oleh pointer.

>referensi : https://www.geeksforgeeks.org/dsa/abstract-data-types/
