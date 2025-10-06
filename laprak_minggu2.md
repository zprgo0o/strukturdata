# <h1 align="center">Laporan Praktikum Modul 2 <br> PENGENALAN C++ </h1>
<p align="center">SYAHDAN AWAL RAMADHAN - 103112430164</p>

## Dasar Teori

C++ merupakan bahasa pemrograman yang dikembangkan oleh Bjarne Stroustrup pada awal tahun 1980-an pada Bell Laboratories. C++ merupakan pengembangan dari bahasa C menggunakan penambahan konsep pemrograman berorientasi objek (Object-Oriented Programming / OOP), sehingga dapat digunakan untuk membangun perangkat lunak dari skala kecil hingga besar dengan lebih efisien.C++ tetap menjadi salah satu bahasa pemrograman penting yang digunakan untuk pengembangan berbagai jenis perangkat lunak sampai saat ini.
## Guided

### guided 1 (call by pointer)
```c++
#include <iostream>
using namespace std;

void tukar(int *px, int *py)  // definisi fungsi
{
    int temp = *px;
    *px = *py;
    *py = temp;
}

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}
```
> Program di atas merupakan contoh penggunaan **call by pointer** untuk menukar nilai dua variabel. Variabel a dan b diinisialisasi dengan nilai 10 dan 20, lalu alamat keduanya dikirim ke fungsi tukar() menggunakan operator &. Di dalam fungsi tukar(), pointer px dan py digunakan untuk mengakses dan menukar nilai yang disimpan pada alamat memori a dan b dengan bantuan variabel sementara temp. Akibatnya, setelah fungsi dijalankan, nilai a dan b saling bertukar tanpa perlu mengembalikan nilai dari fungsi.
### guided 2 (call by reference)
```c++
#include <iostream>
using namespace std;


void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}
```
Program di atas merupakan contoh penggunaan call by reference untuk menukar nilai dua variabel tanpa menggunakan pointer. Variabel a dan b diinisialisasi dengan nilai 10 dan 20, lalu dikirim ke fungsi tukar() yang memiliki parameter referensi int &x dan int &y. Karena parameter tersebut merupakan referensi langsung ke variabel asli, setiap perubahan pada x dan y di dalam fungsi akan langsung memengaruhi a dan b di fungsi main(). Akibatnya, setelah fungsi dijalankan, nilai a dan b berhasil saling bertukar.
## Unguided

### Soal 1

```c++
#include <iostream>
#include <iomanip>
using namespace std;

float tambah(float a, float b) { return a + b; }
float kurang(float a, float b) { return a - b; }
float kali(float a, float b) { return a * b; }
float bagi(float a, float b) { return (b != 0) ? a / b : 0; }

int main() {
    float bil1, bil2;

    cout << "Masukkan bilangan pertama (float): ";
    cin >> bil1;

    cout << "Masukkan bilangan kedua (float): ";
    cin >> bil2;

    cout << "\n--- Hasil Operasi Aritmatika ---" << endl;
    cout << fixed << setprecision(2);

    cout << "Penjumlahan : " << tambah(bil1, bil2) << endl;
    cout << "Pengurangan : " << kurang(bil1, bil2) << endl;
    cout << "Perkalian   : " << kali(bil1, bil2) << endl;

    if (bil2 != 0) {
        cout << "Pembagian   : " << bagi(bil1, bil2) << endl;
    } else {
        cout << "Pembagian   : Tidak dapat dilakukan (pembagian dengan nol)" << endl;
    }

    return 0;
}

```
> Output
> ![Screenshot bagian x](output/ss_Unguided1.png)

Program tersebut menerima dua bilangan desimal (float) dari user melalui input. Setelah itu, program melakukan empat operasi aritmatika dasar: penjumlahan, pengurangan, perkalian, dan pembagian.
Untuk menampilkan hasil program menggunakan fungsi terpisah (tambah, kurang, kali, dan bagi) agar kode lebih terstruktur. Hasil setiap operasi ditampilkan dengan format dua angka di belakang koma menggunakan fixed << setprecision(2) sehingga output terlihat rapi dan konsisten.
Selain itu, pada operasi pembagian, program memeriksa apakah bilangan kedua bernilai nol. Jika tidak nol, hasil pembagian ditampilkan. Namun jika bernilai nol, program menampilkan pesan khusus “Tidak dapat dilakukan (pembagian dengan nol)” agar tidak terjadi error.


### Soal 2

```c++
#include <iostream>
#include <string>
using namespace std;

string satuanBelasan[] = {
    "nol", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan",
    "sepuluh", "sebelas", "dua belas", "tiga belas", "empat belas", "lima belas",
    "enam belas", "tujuh belas", "delapan belas", "sembilan belas"
};

string puluhanText[] = {
    "", "", "dua puluh", "tiga puluh", "empat puluh", "lima puluh",
    "enam puluh", "tujuh puluh", "delapan puluh", "sembilan puluh"
};

string angkaKeTulisan(int n) {
    if (n < 0 || n > 100) {
        return "Angka di luar rentang.";
    }

    if (n < 20) {
        return satuanBelasan[n];
    }
    if (n < 100) {
        int p = n / 10;
        int s = n % 10;
        if (s == 0) {
            return puluhanText[p];
        }
        return puluhanText[p] + " " + satuanBelasan[s];
    }
    return "seratus";
}

int main() {
    int n;
    cout << "Masukkan bilangan (0 s.d 100): ";
    if (!(cin >> n)) {
        cerr << "Input tidak valid." << endl;
        return 1;
    }

    cout << "\n" << n << " : " << angkaKeTulisan(n) << endl;
    cout << "(Contoh: 79 : tujuh puluh sembilan)" << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](output/ss_unguided2.png)

penjelasan kode

Program ini meminta sebuah bilangan bulat (0–100) dari pengguna lewat input. Setelah itu, program akan mengubah angka tersebut menjadi tulisan sederhana dalam bahasa Indonesia. Supaya lebih rapi dan mudah dipahami, proses konversi dibuat dalam fungsi terpisah (angkaKeTulisan). Di dalam fungsi ini, angka diproses dengan beberapa kondisi: Jika angka kurang dari 20, langsung diambil dari daftar khusus (0–19). Jika angka antara 20 sampai 99, angka dipisahkan menjadi puluhan dan satuan, lalu digabungkan dalam bentuk tulisan. Jika angka tepat 100, hasilnya langsung dituliskan sebagai “seratus”. Dengan cara ini, kode program lebih terstruktur dan mudah dikembangkan. Selain itu, program juga memeriksa input pengguna agar tetap berada dalam rentang yang benar (0–100). Jika input tidak valid atau di luar batas, program menampilkan pesan khusus agar tidak terjadi error.

### Soal 3
```c++
#include <iostream>
using namespace std;

void cetakSpasi(int jumlah) {
    for (int i = 0; i < jumlah; i++) {
        cout << " ";
    }
}
void cetakAngkaMenurun(int batas) {
    for (int i = batas; i >= 1; i--) {
        cout << i;
        if (i > 1) cout << " ";
    }
}
void cetakAngkaNaik(int batas) {
    for (int i = 1; i <= batas; i++) {
        cout << i;
        if (i < batas) cout << " ";
    }
}

void cetakPolaMirror(int N) {
    if (N <= 0) {
        cout << "Input harus bilangan bulat positif." << endl;
        return;
    }

    for (int i = N; i >= 1; i--) {
        cetakSpasi(N - i);
        cetakAngkaMenurun(i);
        cout << " * ";
        cetakAngkaNaik(i);
        cout << endl;
    }
    cetakSpasi(N);
    cout << "*" << endl;
}

int main() {
    int N;
    cout << "Masukkan bilangan bulat untuk pola (N): ";
    if (!(cin >> N)) {
        cerr << "Input tidak valid. Harap masukkan angka." << endl;
        return 1;
    }

    cout << "\nOutput:\n";
    cetakPolaMirror(N);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/ss_unguided3.png)

Program ini meminta dua bilangan desimal (float) dari pengguna lewat input. Setelah itu, program menjalankan empat operasi aritmatika dasar, yaitu penjumlahan, pengurangan, perkalian, dan pembagian.
Supaya lebih rapi dan mudah dipahami, setiap operasi dibuat dalam fungsi terpisah (tambah, kurang, kali, dan bagi). Jadi, kode programnya lebih terstruktur dan gampang kalau mau dikembangkan lagi.
Hasil perhitungan ditampilkan dengan format dua angka di belakang koma menggunakan fixed << setprecision(2). Dengan cara ini, output terlihat konsisten dan tidak berantakan, meskipun hasil perhitungannya berupa angka desimal panjang.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
