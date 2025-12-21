# <h1 align="center">Laporan Praktikum Modul 8 <br>QUEUE</h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori
Queue, atau antrian, adalah struktur data linear fundamental yang beroperasi berdasarkan prinsip FIFO (First-In, First-Out), di mana elemen yang pertama kali dimasukkan (melalui operasi Enqueue di bagian Rear/Tail) adalah yang pertama kali akan dikeluarkan (melalui operasi Dequeue di bagian Front/Head), persis seperti antrian di dunia nyata; implementasinya sering menggunakan array, linked list, atau circular array, dan sangat vital dalam aplikasi seperti penjadwalan proses pada sistem operasi dan algoritma pencarian Breadth-First Search (BFS).


## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

// ukuran maksimal queue
#define MAX 5

// struktur queue
struct Queue {
   // datanya pake array yaa, bukan linked list
   int data[MAX];
   int head;
   int tail;
};

// membuat antrian kosong
void buat_queue (Queue &Q) {
   Q.head = -1;
   Q.tail = -1;
   // kenapa head dan tail-nya -1?
   // karena index array mulai dari 0
}

// cek queueu-nya kosong ngga?
bool cek_kosong (Queue Q) {
   return (Q.head == -1 && Q.tail == -1);
}

// cek queue-nya penuh ngga?
bool cek_penuh (Queue Q) {
   return (Q.tail == MAX - 1);
}

// menampilkan isi queue
void print_queue (Queue Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong" << endl;
   } else {
      cout << "queue : ";
      for (int i = Q.head; i <= Q.tail; i++) {
         cout << Q.data[i] << " -> ";
      }
      cout << endl;
   }
}

// menambahkan elemen (enqueue)
void enqueue (Queue &Q, int x) {
// x itu data yang mau dimasukin ke dalam queue
// kenapa namanya x? itu sih terserah, mau pake nama apa aja boleh
// mau dinamain ayam_bakar_haji_ismail juga gapapa
   if (cek_penuh(Q)) {
      cout << "queue sudah penuh, tidak bisa menambah data" << endl;
   } else {
      if (cek_kosong(Q)) {
         Q.head = Q.tail = 0;
      } else {
         Q.tail++;
      }

      Q.data[Q.tail] = x;
      cout << "menambahkan " << x << " ke dalam queue" << endl;
   }
}

// menghapus elemen (dequeue)
void dequeue (Queue &Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong, tidak ada yang bisa dihapus" << endl;
   } else {
      cout << "dequeue " << Q.data[Q.head] << " dari dalam queue" << endl;

      // jika hanya ada 1 elemen
      if (Q.head == Q.tail) {
         Q.head = Q.tail = -1;
      } else {
         // geser semua elemen ke depan/kiri
         // biar tempat kosong di depan dipenuhin
         // dan tempat di belakang bisa dikosongin
         for (int i = Q.head; i < Q.tail; i++) {
            Q.data[i] = Q.data[i + 1];
         }

         Q.tail--;
      }
   }
}

// eksekutor
int main() {
   Queue Q;
   buat_queue(Q);

   enqueue(Q, 5);
   enqueue(Q, 2);
   enqueue(Q, 7);
   print_queue(Q);

   dequeue(Q);
   print_queue(Q);

   enqueue(Q, 4);
   enqueue(Q, 9);
   print_queue(Q);

   dequeue(Q);
   dequeue(Q);
   print_queue(Q);

   return 0;
}
```

>Program ini mengimplementasikan struktur data Queue (antrean) statis menggunakan array berukuran tetap (MAX = 5) dengan dua penunjuk, yaitu head dan tail. Queue dimulai dalam kondisi kosong (head dan tail = −1), lalu mendukung operasi dasar seperti enqueue untuk menambahkan data di bagian belakang antrean, dequeue untuk menghapus data dari bagian depan dengan menggeser elemen ke kiri, isEmpty dan isFull untuk pengecekan kondisi antrean, serta printQueue untuk menampilkan isi antrean. Pada fungsi main, program mendemonstrasikan proses penambahan dan penghapusan elemen secara berurutan sehingga memperlihatkan cara kerja antrean dengan prinsip FIFO (First In First Out).


## UNGUIDED

### Soal 1


#### queue.h
```c++
#ifndef QUEUE_H
#define QUEUE_H

const int MAX_SIZE = 5;
typedef int ElementType;

struct Queue {
    ElementType data[MAX_SIZE];
    int front, rear;
};

void initQueue(Queue &Q);

bool isEmpty(const Queue &Q);

bool isFull(const Queue &Q);

void enqueue(Queue &Q, ElementType value);

ElementType dequeue(Queue &Q);

void displayQueue(const Queue &Q);

#endif

```
#### queue.cpp
```c++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh" << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x;

    if (isEmptyQueue(Q)) {
        cout << "Queue kosong" << endl;
        return -1;
    } else {
        x = Q.info[Q.head];

        for (int i = Q.head; i < Q.tail; i++) {
            Q.info[i] = Q.info[i + 1];
        }
        Q.tail--;

        if (Q.tail < 0) {
            Q.head = -1;
            Q.tail = -1;
        }
        return x;
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " | ";

    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```

#### main.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    Queue Q;
    initQueue(Q);

    int pilihan, nilai;

    do {
        cout << "\n=== MENU QUEUE ===" << endl;
        cout << "1. Enqueue (Tambah data)" << endl;
        cout << "2. Dequeue (Hapus data)" << endl;
        cout << "3. Tampilkan Queue" << endl;
        cout << "4. Keluar" << endl;
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan nilai: ";
                cin >> nilai;
                enqueue(Q, nilai);
                break;

            case 2:
                dequeue(Q);
                break;

            case 3:
                displayQueue(Q);
                break;

            case 4:
                cout << "Program selesai." << endl;
                break;

            default:
                cout << "Pilihan tidak valid!" << endl;
        }

    } while (pilihan != 4);

    return 0;
}

```
>Pada alternatif 1, queue diimplementasikan menggunakan array dengan kondisi head selalu berada di indeks awal (0) dan tail bergerak mengikuti penambahan atau penghapusan elemen. Operasi enqueue dilakukan dengan menambahkan data di posisi tail + 1, sedangkan dequeue dilakukan dengan mengambil elemen di head lalu menggeser seluruh elemen di belakangnya ke kiri agar head tetap di posisi awal. Queue dianggap kosong jika head dan tail bernilai -1, dan penuh jika tail mencapai indeks maksimum array. Mekanisme ini sederhana namun kurang efisien karena membutuhkan proses penggeseran data setiap kali dequeue.

### Soal 2
Buatlah implementasi ADT Queue pada file "queue.cpp" dengan menerapkan mekanisme queue Alternatif 2 (head bergerak, tail bergerak).

#### queue.cpp
```c++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 || Q.head > Q.tail);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh" << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong" << endl;
        return -1;
    } else {
        infotype x = Q.info[Q.head];
        Q.head++;

        // jika habis, reset queue
        if (Q.head > Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        }
        return x;
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " | ";

    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}

```
 
>Pada alternatif 2, baik head maupun tail bergerak seiring operasi queue, sehingga tidak diperlukan penggeseran data saat dequeue. Elemen dihapus dengan cara menaikkan nilai head, sedangkan elemen baru ditambahkan dengan menaikkan nilai tail. Queue kosong ketika head lebih besar dari tail atau keduanya bernilai -1, dan penuh ketika tail mencapai batas akhir array. Cara ini lebih efisien dibanding alternatif 1, tetapi memiliki kelemahan karena ruang array di bagian awal tidak dapat digunakan kembali setelah beberapa kali dequeue.

### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

#### queue.cpp
```c++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh" << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail = (Q.tail + 1) % MAX;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong" << endl;
        return -1;
    } else {
        infotype x = Q.info[Q.head];

        // jika hanya 1 elemen
        if (Q.head == Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        } else {
            Q.head = (Q.head + 1) % MAX;
        }
        return x;
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " | ";

    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        int i = Q.head;
        while (true) {
            cout << Q.info[i] << " ";
            if (i == Q.tail) break;
            i = (i + 1) % MAX;
        }
    }
    cout << endl;
}

```
>Pada alternatif 3, queue menggunakan konsep circular queue di mana head dan tail bergerak secara melingkar menggunakan operasi modulo terhadap ukuran array. Elemen yang dihapus atau ditambahkan tidak menyebabkan penggeseran data, dan ruang array yang telah dilewati dapat digunakan kembali. Queue dinyatakan kosong jika head bernilai -1, dan penuh jika posisi (tail + 1) % MAX sama dengan head. Mekanisme ini merupakan yang paling efisien karena memanfaatkan seluruh kapasitas array secara optimal dan menghindari pemborosan memori.

## Referensi
https://www.w3schools.com/go/index.php
