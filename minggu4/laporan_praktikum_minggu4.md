
# <h1 align="center">Laporan Praktikum Modul 4 <br> SINGLY LINKED LIST </h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori

Linked list adalah struktur data linear yang terdiri dari serangkaian elemen yang disebut “node”, di mana setiap node terhubung ke node berikutnya dalam urutan tertentu. Setiap node terdiri dari dua bagian utama: data yang disimpan dan referensi ke node berikutnya dalam urutan. Ini memungkinkan alokasi memori yang dinamis dan tidak perlu alokasi memori yang bersifat statis seperti yang terjadi pada array.


## Guided

### guided 1
   ```c++
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer kepala (head)
Node* kepala = nullptr;

// Fungsi untuk membuat node baru
Node* buatNode(int data) {
    Node* nodeBaru = new Node();
    nodeBaru->data = data;
    nodeBaru->next = nullptr;
    return nodeBaru;
}

// Fungsi untuk menyisipkan node di depan
void sisipDepan(int data) {
    Node* nodeBaru = buatNode(data);
    nodeBaru->next = kepala; // Node baru menunjuk ke kepala lama
    kepala = nodeBaru;       // Kepala sekarang menunjuk ke node baru
    cout << "Data " << data << " berhasil disisipkan di depan.\n";
}

// Fungsi untuk menyisipkan node di belakang
void sisipBelakang(int data) {
    Node* nodeBaru = buatNode(data);
    if (kepala == nullptr) {
        kepala = nodeBaru;
    } else {
        Node* temp = kepala;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = nodeBaru;
    }
    cout << "Data " << data << " berhasil disisipkan di belakang.\n";
}

// Fungsi untuk menyisipkan node setelah node tertentu
void sisipSetelah(int target, int dataBaru) {
    Node* temp = kepala;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data target " << target << " tidak ditemukan!\n";
    } else {
        Node* nodeBaru = buatNode(dataBaru);
        nodeBaru->next = temp->next;
        temp->next = nodeBaru;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== FUNGSI HAPUS ==========
void hapusNode(int data) {
    if (kepala == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = kepala;
    Node* sebelumnya = nullptr;

    // Kasus 1: Jika data di node pertama (kepala)
    if (temp != nullptr && temp->data == data) {
        kepala = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Kasus 2: Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        sebelumnya = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    // Lepaskan node dari list dan bebaskan memori
    sebelumnya->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== FUNGSI PERBARUI ==========
void perbaruiNode(int dataLama, int dataBaru) {
    Node* temp = kepala;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diperbarui menjadi " << dataBaru << ".\n";
    }
}

// ========== FUNGSI TAMPILKAN ==========
void tampilkanList() {
    if (kepala == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = kepala;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// ========== PROGRAM UTAMA ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Sisip Depan\n";
        cout << "2. Sisip Belakang\n";
        cout << "3. Sisip Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Perbarui Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih opsi: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                sisipDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                sisipBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                sisipSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                perbaruiNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```

Program di atas merupakan implementasi Single Linked List dalam bahasa C++ yang menyediakan berbagai operasi dasar pada struktur data berantai. Program ini memungkinkan pengguna untuk menambahkan node di depan, di belakang, maupun setelah node tertentu, serta menghapus dan memperbarui data yang sudah ada dalam list. Selain itu, terdapat fitur untuk menampilkan seluruh isi linked list agar pengguna dapat melihat perubahan yang terjadi. Setiap operasi dilakukan secara dinamis menggunakan pointer, sehingga manajemen memori dilakukan langsung dengan alokasi dan dealokasi node. Program ini juga dilengkapi menu interaktif agar pengguna dapat memilih operasi yang diinginkan secara mudah.

## Unguided

### Soal 1

```c++
#include <iostream>
#include <string>
using namespace std;

struct Node {
    string nama, pesanan;
    Node* next;
};

Node* front = nullptr;
Node* rear = nullptr;

bool kosong() { return front == nullptr; }

void tambah(string nama, string pesanan) {
    Node* baru = new Node{nama, pesanan, nullptr};
    if (kosong()) front = rear = baru;
    else rear = rear->next = baru;
    cout << nama << " ditambahkan ke antrian.\n";
}

void layani() {
    if (kosong()) { cout << "Antrian kosong!\n"; return; }
    Node* hapus = front;
    cout << "Melayani " << hapus->nama << " - " << hapus->pesanan << endl;
    front = front->next;
    if (!front) rear = nullptr;
    delete hapus;
}

void tampil() {
    if (kosong()) { cout << "Antrian kosong!\n"; return; }
    Node* temp = front;
    cout << "\nDaftar Antrian:\n";
    while (temp) {
        cout << "- " << temp->nama << " : " << temp->pesanan << endl;
        temp = temp->next;
    }
}

int main() {
    int pil; string nama, pesanan;
    do {
        cout << "\n1. Tambah Antrian\n2. Layani Antrian\n3. Tampilkan Antrian\n0. Keluar\nPilih: ";
        cin >> pil; cin.ignore();
        if (pil == 1) { cout << "Nama: "; getline(cin, nama); cout << "Pesanan: "; getline(cin, pesanan); tambah(nama, pesanan); }
        else if (pil == 2) layani();
        else if (pil == 3) tampil();
    } while (pil != 0);
}

```
>

Program ini merupakan implementasi sederhana dari antrian pembeli menggunakan konsep Single Linked List dengan prinsip FIFO (First In, First Out). Setiap node menyimpan data nama pembeli dan pesanan. Program menyediakan tiga fitur utama, yaitu menambah pembeli ke dalam antrian, melayani pembeli pertama (menghapus dari depan), dan menampilkan seluruh antrian yang sedang menunggu. Dengan menggunakan pointer front dan rear, program dapat mengelola antrian secara dinamis sehingga data pembeli dapat bertambah dan berkurang tanpa batasan jumlah tetap.

### Soal 2

```c++
#include <iostream>
using namespace std;

// Struktur node
struct Node {
    int data;
    Node* next;
};

Node* head = nullptr;

// Fungsi menambah node di belakang
void tambahBelakang(int data) {
    Node* baru = new Node{data, nullptr};
    if (head == nullptr)
        head = baru;
    else {
        Node* temp = head;
        while (temp->next != nullptr)
            temp = temp->next;
        temp->next = baru;
    }
}

// Fungsi menampilkan isi linked list
void tampil() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }
    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// Fungsi membalik urutan linked list
void balikList() {
    Node *prev = nullptr, *curr = head, *next = nullptr;
    while (curr != nullptr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head = prev;
    cout << "Linked list berhasil dibalik!\n";
}

int main() {
    int n, data;

    cout << "Masukkan jumlah elemen linked list: ";
    cin >> n;

    for (int i = 0; i < n; i++) {
        cout << "Masukkan data ke-" << i + 1 << ": ";
        cin >> data;
        tambahBelakang(data);
    }

    cout << "\nLinked list sebelum dibalik:\n";
    tampil();

    balikList();

    cout << "\nLinked list setelah dibalik:\n";
    tampil();

    return 0;
}

```
>

Program ini merupakan implementasi Single Linked List dalam bahasa C++ yang memungkinkan pengguna memasukkan data secara interaktif, kemudian membalik urutan elemen di dalam list. Setiap data yang dimasukkan akan ditambahkan ke bagian belakang linked list menggunakan pointer, dan proses pembalikan dilakukan dengan mengubah arah pointer antar-node secara berurutan menggunakan tiga variabel bantu (prev, curr, dan next). Setelah proses pembalikan selesai, program menampilkan isi linked list sebelum dan sesudah dibalik sehingga pengguna dapat melihat perubahannya dengan jelas.

> referensi : https://rumahcoding.co.id/linked-list-pengertian-dan-implementasi-dasar/
