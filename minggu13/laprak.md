# <h1 align="center">Laporan Praktikum Modul 13 <br> Multi Link List </h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori
1. Struktur Data Linked List

Linked list adalah struktur data dinamis yang tersusun dari sekumpulan node, di mana setiap node berisi data (info) dan pointer yang menunjuk ke node lain. Berbeda dengan array, linked list tidak membutuhkan alokasi memori secara berurutan dan memungkinkan penambahan serta penghapusan elemen dilakukan secara fleksibel tanpa harus menggeser data lainnya. Linked list banyak digunakan ketika ukuran data tidak tetap dan operasi penyisipan atau penghapusan sering dilakukan.

2. Circular Singly Linked List

Circular singly linked list merupakan variasi linked list di mana node terakhir tidak menunjuk ke NULL, melainkan menunjuk kembali ke node pertama sehingga membentuk struktur melingkar. Setiap node hanya memiliki satu pointer next. Struktur ini memungkinkan traversal dilakukan secara terus-menerus tanpa terputus dan sering digunakan pada kasus yang bersifat siklik, seperti penjadwalan bergilir atau antrian berputar. Pada program circular linked list yang dibuat, pengelolaan pointer difokuskan pada penjagaan hubungan melingkar saat proses insert, delete, dan traversal agar tidak terjadi infinite loop atau pointer terputus.

3. Multi Linked List

Multi Linked List adalah struktur data yang terdiri dari lebih dari satu jenis hubungan pointer dalam satu node atau lebih dari satu tingkat linked list. Umumnya, struktur ini digunakan untuk merepresentasikan relasi satu-ke-banyak (one-to-many), di mana satu data induk dapat memiliki banyak data turunan. Multi linked list cocok digunakan untuk memodelkan data hierarkis atau bertingkat, seperti struktur organisasi, kategori dan subkategori, atau data induk dan detailnya.

4. Multi Linked List dengan List Induk dan List Anak (ADT)

Pada implementasi Multi Linked List berbasis ADT, digunakan dua struktur utama yaitu list induk dan list anak. Setiap elemen pada list induk memiliki sebuah list anak yang dikelola secara terpisah. Baik list induk maupun list anak diimplementasikan menggunakan double linked list, sehingga setiap node memiliki pointer next dan prev. Penggunaan double linked list mempermudah proses traversal dua arah serta penghapusan node dari posisi manapun tanpa harus selalu mencari node sebelumnya. Konsep ADT diterapkan dengan memisahkan definisi struktur dan deklarasi fungsi (header file) dari implementasinya (source file).

5. Multi Linked List Parent–Child Sederhana

Implementasi multi linked list sederhana menggunakan pendekatan parent–child, di mana setiap parent node memiliki pointer yang menunjuk ke awal linked list anak. Struktur ini menggunakan single linked list baik pada parent maupun child, sehingga lebih sederhana namun tetap mampu merepresentasikan hubungan satu-ke-banyak. Program ini menekankan pada pemahaman relasi antar node dan cara menghubungkan list anak ke node induk secara langsung tanpa menggunakan ADT yang kompleks.

6. Alokasi dan Dealokasi Memori

Seluruh program menggunakan alokasi memori dinamis dengan new untuk membuat node baru dan delete untuk menghapus node. Pengelolaan memori ini penting untuk mencegah memory leak dan memastikan bahwa setiap node yang sudah tidak digunakan dapat dilepaskan dengan benar. Konsep ini menjadi dasar dalam implementasi struktur data dinamis di bahasa C++.

7. Traversal, Insert, dan Delete

Traversal merupakan proses menelusuri seluruh elemen dalam linked list menggunakan pointer. Operasi insert dan delete dilakukan dengan memanipulasi pointer antar node agar struktur list tetap konsisten. Pada circular linked list, traversal harus memperhatikan kondisi berhenti agar tidak terjadi perulangan tanpa akhir, sedangkan pada multi linked list, traversal dilakukan secara bertingkat antara list induk dan list anak.

## Guided

### soal 1

```go
#include <iostream>
#include <string>
using namespace std;

struct child_node
{
   string info;
   child_node* next;
};

struct parent_node
{
   string info;
   child_node* child_head;
   parent_node* next;
};

parent_node *create_parent(string info)
{
   parent_node* new_node = new parent_node;
   new_node->info = info;
   new_node->child_head = NULL;
   new_node->next = NULL;
   return new_node;
};

child_node *create_child(string info)
{
   child_node* new_node = new child_node;
   new_node->info = info;
   new_node->next = NULL;
   return new_node;
};

void insert_parent(parent_node *&head, string info)
{
   parent_node* new_node = create_parent(info);
   if (head == NULL)
   {
      head = new_node;
   }
   else
   {
      parent_node* temporary = head;
      while (temporary->next != NULL)
      {
         temporary = temporary->next;
      }
      temporary->next = new_node;
   }
}

void insert_child(parent_node *head, string parent_info, string child_info)
{
   parent_node *parent_temp = head;
   while (parent_temp != NULL && parent_temp->info != parent_info)
   {
      parent_temp = parent_temp->next;
   }
   if (parent_temp != NULL)
   {
      child_node *new_child = create_child(child_info);
      if (parent_temp->child_head == NULL)
      {
         parent_temp->child_head = new_child;
      }
      else
      {
         child_node *child_temp = parent_temp->child_head;
         while (child_temp->next != NULL)
         {
            child_temp = child_temp->next;
         }
         child_temp->next = new_child;
      }
   }
}

void print_all(parent_node *head)
{
   parent_node *parent_temp = head;
   while (parent_temp != NULL)
   {
      cout << parent_temp->info;
      child_node *child_temp = parent_temp->child_head;
      if (child_temp != NULL)
      {
         while (child_temp != NULL)
         {
            cout << " -> " << child_temp->info;
            child_temp = child_temp->next;
         }
      }
      cout << endl;
      parent_temp = parent_temp->next;
   }
}

int main()
{
   parent_node *list = NULL;

   insert_parent(list, "parent node 1");
   insert_parent(list, "parent node 2");

   print_all(list);
   cout << "\n";

   insert_child(list, "parent node 1", "child node a");
   insert_child(list, "parent node 1", "child node b");
   insert_child(list, "parent node 2", "child node c");

   print_all(list);

   return 0;
}
```


## Unguided

### Soal 1
Perhatikan program 46 multilist.h, buat multilist.cpp untuk implementasi semua fungsi pada
multilist.h. Buat main.cpp untuk pemanggilan fungsi-fungsi tersebut.

### multilist.h
```go
#ifndef MULTILIST_H_INCLUDED
#define MULTILIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL

typedef int infotypeinduk;
typedef int infotypeanak;

typedef struct elemen_list_induk *address;
typedef struct elemen_list_anak *address_anak;

/* ====== STRUKTUR LIST ANAK ====== */
struct elemen_list_anak {
    infotypeanak info;
    address_anak next;
    address_anak prev;
};

struct listanak {
    address_anak first;
    address_anak last;
};

/* ====== STRUKTUR LIST INDUK ====== */
struct elemen_list_induk {
    infotypeinduk info;
    listanak lanak;
    address next;
    address prev;
};

struct listinduk {
    address first;
    address last;
};

/* ====== OPERASI LIST ====== */
bool ListEmpty(listinduk L);
bool ListEmptyAnak(listanak L);

void CreateList(listinduk &L);
void CreateListAnak(listanak &L);

address alokasi(infotypeinduk x);
address_anak alokasiAnak(infotypeanak x);

void dealokasi(address P);
void dealokasiAnak(address_anak P);

address findElm(listinduk L, infotypeinduk x);
address_anak findElm(listanak L, infotypeanak x);

void insertFirst(listinduk &L, address P);
void insertLast(listinduk &L, address P);

void insertLastAnak(listanak &L, address_anak P);

void printInfo(listinduk L);
void printInfoAnak(listanak L);

#endif

```

### multilist.cpp
```
#include "multilist.h"

/* ====== CEK LIST KOSONG ====== */
bool ListEmpty(listinduk L) {
    return (L.first == Nil);
}

bool ListEmptyAnak(listanak L) {
    return (L.first == Nil);
}

/* ====== CREATE LIST ====== */
void CreateList(listinduk &L) {
    L.first = Nil;
    L.last = Nil;
}

void CreateListAnak(listanak &L) {
    L.first = Nil;
    L.last = Nil;
}

/* ====== ALOKASI ====== */
address alokasi(infotypeinduk x) {
    address P = new elemen_list_induk;
    if (P != Nil) {
        P->info = x;
        CreateListAnak(P->lanak);
        P->next = Nil;
        P->prev = Nil;
    }
    return P;
}

address_anak alokasiAnak(infotypeanak x) {
    address_anak P = new elemen_list_anak;
    if (P != Nil) {
        P->info = x;
        P->next = Nil;
        P->prev = Nil;
    }
    return P;
}

void dealokasi(address P) {
    delete P;
}

void dealokasiAnak(address_anak P) {
    delete P;
}

/* ====== SEARCH ====== */
address findElm(listinduk L, infotypeinduk x) {
    address P = L.first;
    while (P != Nil) {
        if (P->info == x)
            return P;
        P = P->next;
    }
    return Nil;
}

address_anak findElm(listanak L, infotypeanak x) {
    address_anak P = L.first;
    while (P != Nil) {
        if (P->info == x)
            return P;
        P = P->next;
    }
    return Nil;
}

/* ====== INSERT INDUK ====== */
void insertFirst(listinduk &L, address P) {
    if (ListEmpty(L)) {
        L.first = P;
        L.last = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void insertLast(listinduk &L, address P) {
    if (ListEmpty(L)) {
        insertFirst(L, P);
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/* ====== INSERT ANAK ====== */
void insertLastAnak(listanak &L, address_anak P) {
    if (ListEmptyAnak(L)) {
        L.first = P;
        L.last = P;
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/* ====== PRINT ====== */
void printInfo(listinduk L) {
    address P = L.first;
    while (P != Nil) {
        cout << "Induk : " << P->info << " | Anak : ";
        printInfoAnak(P->lanak);
        cout << endl;
        P = P->next;
    }
}

void printInfoAnak(listanak L) {
    address_anak P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
}

```

### mainm.cpp
```
#include "multilist.h"

int main() {
    listinduk L;
    CreateList(L);

    address P1 = alokasi(1);
    address P2 = alokasi(2);

    insertLast(L, P1);
    insertLast(L, P2);

    insertLastAnak(P1->lanak, alokasiAnak(10));
    insertLastAnak(P1->lanak, alokasiAnak(20));
    insertLastAnak(P2->lanak, alokasiAnak(30));

    printInfo(L);

    return 0;
}
```
> program diatas adalah struktur data yang terdiri dari dua tingkat list, yaitu list induk dan list anak, di mana setiap elemen induk dapat memiliki sebuah list anak yang saling terhubung. Pada soal ini, Multi Linked List digunakan untuk merepresentasikan hubungan satu-ke-banyak, misalnya satu data induk yang memiliki beberapa data anak. Implementasi dilakukan dengan menggunakan pointer ganda (next dan prev) pada masing-masing list sehingga memungkinkan proses penambahan, pencarian, dan penampilan data induk beserta seluruh data anaknya secara terstruktur dan terorganisir.

### Soal 2
Buatlah ADT Multi Linked list sebagai berikut di dalam file “circularlist.h”

Terdapat 11 fungsi/prosedur untuk ADT circularlist
- procedure CreateList( input/output L : List )
- function alokasi( x : infotype ) → address
- procedure dealokasi( input/output t P : address )
- procedure insertFirst( input/output L : List, input P : address )
- procedure insertAfter( input/output L : List, input Prec : address, P : address)
- procedure insertLast( input/output L : List, input P : address )
- procedure deleteFirst( input/output L : List, input/output P : address )
- procedure deleteAfter( input/output L : List, input Prec : address, input/output t P : address )
- procedure deleteLast( input/output L : List, P : address )
- function findElm( L : List, x : infotype ) → address
- procedure printInfo( input L : List )

Keterangan :
- fungsi findElm mencari elemen di dalam list L berdasarkan nim
- fungsi mengembalikan elemen dengan dengan info nim == x.nim jika ditemukan
- fungsi mengembalikan NIL jika tidak ditemukan

Buatlah implementasi ADT Doubly Linked list pada file “circularlist.cpp”. Tambahkan fungsi/prosedur
berikut pada file “main.cpp”.
- fungsi create ( in nama, nim : string, jenis_kelamin : char, ipk : float)
- fungsi disediakan, ketik ulang code yang diberikan
- fungsi mengalokasikan sebuah elemen list dengan info sesuai input

Cobalah hasil implementasi ADT pada file “main.cpp”

### circularlist.h
```
#ifndef CIRCULARLIST_H_INCLUDED
#define CIRCULARLIST_H_INCLUDED

#include <string>
using namespace std;

#define Nil NULL

/* ====== TIPE DATA ====== */
struct mahasiswa {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
};

typedef mahasiswa infotype;
typedef struct ElmList *address;

/* ====== STRUKTUR NODE ====== */
struct ElmList {
    infotype info;
    address next;
};

/* ====== STRUKTUR LIST ====== */
struct List {
    address first;
};

/* ====== PROTOTYPE ====== */
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address P);

void insertFirst(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void insertLast(List &L, address P);

void deleteFirst(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteLast(List &L, address &P);

address findElm(List L, infotype x);
void printInfo(List L);

#endif

```

### circularlist.cpp
```
#include "circularlist.h"
#include <iostream>
using namespace std;

void createList(List &L) {
    L.first = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address P) {
    delete P;
}

/* ====== INSERT ====== */
void insertFirst(List &L, address P) {
    if (L.first == Nil) {
        L.first = P;
        P->next = P;
    } else {
        address last = L.first;
        while (last->next != L.first)
            last = last->next;
        P->next = L.first;
        last->next = P;
        L.first = P;
    }
}

void insertAfter(List &L, address Prec, address P) {
    if (Prec != Nil) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void insertLast(List &L, address P) {
    if (L.first == Nil)
        insertFirst(L, P);
    else {
        address last = L.first;
        while (last->next != L.first)
            last = last->next;
        last->next = P;
        P->next = L.first;
    }
}

/* ====== DELETE ====== */
void deleteFirst(List &L, address &P) {
    if (L.first != Nil) {
        address last = L.first;
        while (last->next != L.first)
            last = last->next;

        P = L.first;
        if (P->next == P) {
            L.first = Nil;
        } else {
            L.first = P->next;
            last->next = L.first;
        }
        P->next = Nil;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != Nil && Prec->next != L.first) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    }
}

void deleteLast(List &L, address &P) {
    if (L.first != Nil) {
        address prev = Nil;
        address curr = L.first;
        while (curr->next != L.first) {
            prev = curr;
            curr = curr->next;
        }
        P = curr;
        if (prev == Nil) {
            L.first = Nil;
        } else {
            prev->next = L.first;
        }
        P->next = Nil;
    }
}

/* ====== SEARCH ====== */
address findElm(List L, infotype x) {
    if (L.first == Nil) return Nil;

    address P = L.first;
    do {
        if (P->info.nim == x.nim)
            return P;
        P = P->next;
    } while (P != L.first);

    return Nil;
}

/* ====== PRINT ====== */
void printInfo(List L) {
    if (L.first == Nil) {
        cout << "List kosong\n";
        return;
    }

    address P = L.first;
    do {
        cout << "Nama : " << P->info.nama << endl;
        cout << "NIM  : " << P->info.nim << endl;
        cout << "JK   : " << P->info.jenis_kelamin << endl;
        cout << "IPK  : " << P->info.ipk << endl;
        cout << "--------------------------\n";
        P = P->next;
    } while (P != L.first);
}
```

### mainc.cpp
```
#include "circularlist.h"
#include "circularlist.cpp"
#include <iostream>
using namespace std;

/* ====== FUNGSI CREATE DATA (sesuai modul) ====== */
address createData() {
    infotype x;

    cout << "Nama           : ";
    cin.ignore();
    getline(cin, x.nama);

    cout << "NIM            : ";
    cin >> x.nim;

    cout << "Jenis Kelamin  : ";
    cin >> x.jenis_kelamin;

    cout << "IPK            : ";
    cin >> x.ipk;

    return alokasi(x);
}

/* ====== MENU ====== */
void menu() {
    cout << "\n===== MENU CIRCULAR LINKED LIST =====\n";
    cout << "1. Insert First\n";
    cout << "2. Insert Last\n";
    cout << "3. Insert After (berdasarkan NIM)\n";
    cout << "4. Delete First\n";
    cout << "5. Delete Last\n";
    cout << "6. Cari Data (berdasarkan NIM)\n";
    cout << "7. Tampilkan Data\n";
    cout << "0. Keluar\n";
    cout << "Pilih menu : ";
}

int main() {
    List L;
    createList(L);

    int pilih;
    address P, Prec;
    infotype x;

    do {
        menu();
        cin >> pilih;

        switch (pilih) {
        case 1:
            cout << "\nInsert First\n";
            P = createData();
            insertFirst(L, P);
            break;

        case 2:
            cout << "\nInsert Last\n";
            P = createData();
            insertLast(L, P);
            break;

        case 3:
            cout << "\nInsert After\n";
            cout << "Masukkan NIM acuan : ";
            cin >> x.nim;
            Prec = findElm(L, x);
            if (Prec != Nil) {
                P = createData();
                insertAfter(L, Prec, P);
            } else {
                cout << "Data tidak ditemukan!\n";
            }
            break;

        case 4:
            cout << "\nDelete First\n";
            deleteFirst(L, P);
            if (P != Nil) {
                dealokasi(P);
                cout << "Data pertama berhasil dihapus\n";
            }
            break;

        case 5:
            cout << "\nDelete Last\n";
            deleteLast(L, P);
            if (P != Nil) {
                dealokasi(P);
                cout << "Data terakhir berhasil dihapus\n";
            }
            break;

        case 6:
            cout << "\nCari Data\n";
            cout << "Masukkan NIM : ";
            cin >> x.nim;
            P = findElm(L, x);
            if (P != Nil) {
                cout << "Data ditemukan:\n";
                cout << P->info.nama << " | "
                     << P->info.nim << " | "
                     << P->info.jenis_kelamin << " | "
                     << P->info.ipk << endl;
            } else {
                cout << "Data tidak ditemukan\n";
            }
            break;

        case 7:
            cout << "\nData Mahasiswa:\n";
            printInfo(L);
            break;

        case 0:
            cout << "Program selesai\n";
            break;

        default:
            cout << "Pilihan tidak valid!\n";
        }
    } while (pilih != 0);

    return 0;
}
```

> Program diatas adalah struktur data linked list di mana elemen terakhir menunjuk kembali ke elemen pertama, sehingga membentuk sebuah lingkaran. Pada soal ini, Circular Linked List digunakan untuk menyimpan data mahasiswa yang terdiri dari nama, NIM, jenis kelamin, dan IPK. Implementasi mencakup operasi dasar seperti insert first, insert last, insert after berdasarkan NIM, pencarian data, serta penampilan data secara berurutan. Struktur circular memungkinkan traversal data tanpa batas akhir selama kondisi berhenti ditentukan dengan tepat.
## Referensi
1. https://www.w3schools.com/go/index.php
