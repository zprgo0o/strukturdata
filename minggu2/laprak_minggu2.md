# <h1 align="center">Laporan Praktikum Modul 2 <br> PENGENALAN C++ </h1>
<p align="center">SYAHDAN AWAL RAMADHAN - 103112430164</p>

## Dasar Teori

Dokumen ini menjelaskan konsep dasar pointer dan referensi dalam bahasa C++.
Pointer adalah variabel yang menyimpan alamat memori dari variabel lain, sedangkan referensi adalah nama lain (alias) dari variabel yang sudah ada.
Pointer menggunakan operator `&` untuk mengambil alamat variabel, sementara referensi secara langsung terhubung dengan variabel aslinya tanpa perlu simbol tambahan.
Keduanya digunakan agar fungsi dapat mengubah nilai asli variabel yang dikirimkan dari luar fungsi, bukan hanya salinannya.
Dalam praktiknya, call by pointer memakai alamat variabel `(&)`, sedangkan call by reference menggunakan referensi langsung (`&` di parameter fungsi)
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
> Program di atas merupakan contoh penggunaan call by reference untuk menukar nilai dua variabel tanpa menggunakan pointer. Variabel a dan b diinisialisasi dengan nilai 10 dan 20, lalu dikirim ke fungsi tukar() yang memiliki parameter referensi int &x dan int &y. Karena parameter tersebut merupakan referensi langsung ke variabel asli, setiap perubahan pada x dan y di dalam fungsi akan langsung memengaruhi a dan b di fungsi main(). Akibatnya, setelah fungsi dijalankan, nilai a dan b berhasil saling bertukar.
## Unguided

### Unguided 1

```c++
#include <iostream>
using namespace std;

int main(){
    int matriks[3][3] = {
        {1, 2, 3,},
        {4, 5, 6,},
        {7, 8, 9,}
    };

    int transpose[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matriks[i][j];  
        }
    }

    cout << "matriks awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }
    cout << "matriks hasil tranpose" << endl;
    for (int i = 0; i<3; i++){
        for (int j = 0; j<3; j++){
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}
```
> Program ini membuat matriks 3×3, lalu menukar baris dan kolomnya menggunakan `transpose[j][i]` = `matriks[i][j]`. Hasilnya kemudian ditampilkan dalam bentuk matriks baru.


### Unguided 2

```c++
#include <iostream>
using namespace std;

void kuadratkan(int &x) {
    x = x*x;
}

int main() {
    int nilai = 5;
    cout << "nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "nilai setelah dikuadratkan: " << nilai << endl;
    return 0;
}
```
> Program pada soal nomor 2 merupakan contoh penggunaan **call by reference** di C++. Program ini memiliki fungsi `kuadratkan(int &x)` yang menerima parameter berupa referensi ke variabel asli, sehingga setiap perubahan nilai pada `x` akan langsung memengaruhi variabel yang dikirim dari fungsi `main()`. Di dalam `main()`, variabel `nilai` diinisialisasi dengan angka 5, lalu dipanggil fungsi `kuadratkan(nilai)` yang mengubah nilai tersebut menjadi hasil kuadratnya, yaitu 25. Program ini kemudian menampilkan nilai sebelum dan sesudah pemanggilan fungsi untuk menunjukkan bahwa perubahan terjadi secara langsung pada variabel asli.

## Referensi

1. https://www.scribd.com/document/788845901/Kuliah-07-Referensi-Pointer-Dan-Dereferensi
