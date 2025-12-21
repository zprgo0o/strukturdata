# <h1 align="center">Laporan Praktikum Modul 10 <br> Tree </h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori
Binary Search Tree merupakan struktur data non-linear berbentuk pohon biner di mana setiap node memiliki paling banyak dua anak, yaitu anak kiri dan anak kanan, dengan aturan utama bahwa nilai pada subtree kiri selalu lebih kecil dari nilai node induk, sedangkan nilai pada subtree kanan selalu lebih besar. Aturan ini memungkinkan proses pencarian, penyisipan, dan penghapusan data dilakukan secara efisien karena setiap keputusan traversal mengurangi ruang pencarian.

## Guided

### soal 1


```
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

// fungsi buat node baru
Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru -> data = nilai;
    baru -> kiri = baru->kanan = NULL;
    return baru;
}

// 1. insert (menyisipkan data)
Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);

    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai); // masuk kiri jika lebih kecil
    else if (nilai > root->data)
        root->kanan  = insert(root->kanan, nilai); // masuk kanan jika lebih besar
    
    return root;
}

//2, search (mencari data)
Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root; // ketemu atau tidak ada

    if (nilai < root-> data)
        return search(root->kiri, nilai); // cari ke kiri

    return search(root->kanan, nilai); // cari ke kanan
}

// helper: cari nilai terkecil (untuk proses hapus)
Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;
    return current;
}

//3. delete (menghapus data - diperlukan untuk update)
Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        //jika data ketemu
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL)
        {
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        //jika punya 2 anak: ambil terkecil dari kanan
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data); 
    }
    return root;
}

//4, update(ubah data)
Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama); // hapus yang lama
        root = insert(root, baru); // masukkan yang baru
        cout << "Data " << Lama << "diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "data " << Lama << "tidak ditemukan!" << endl;
    }
    return root;
}

//5, treversal (menampilkan data)
void preOrder(Node *root)
{// akar -> kiri ->kanan
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{// kiri -> akar _>kanan
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{ // kiri-> kanan -> akar
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << " Data berhasil dimasukkan.\n"
        << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVERSAL) ===" << endl;
    cout << "PreOrder   : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder    : "; 
    inOrder(root);
    cout << endl;
    cout << "PostOrder  : ";
    postOrder(root);
    cout << "\n"
        << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "cari " << cari1 << "; " << (search(root, cari1) ? "ketemu" : "tidak ada") << endl;
    cout << "cari " << cari2 << "; " << (search(root, cari2) ? "ketemu" : "tidak ada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    // mengubah 5 angka menjadi 8
    root = update(root, 5, 8);
    cout << "hasil InOrder setelah update: ";
    cout << endl;
    cout << endl;

    cout << "preOrder   : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder    : "; 
    inOrder(root);
    cout << endl;
    cout << "PostOrder  : ";
    postOrder(root);
    cout << "\n"
        << endl;
    
    cout << "===5. TEST DELETE ===" << endl;
    // menghapus angka 20(node yang punya anak)
    cout << "menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "preOrder   : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder    : "; 
    inOrder(root);
    cout << endl;
    cout << "PostOrder  : ";
    postOrder(root);
    cout << "\n"
        << endl;

    return 0;    
}        

```
>Program di atas merupakan implementasi Binary Search Tree (BST) yang mendukung operasi utama yaitu insert, search, delete, update, dan traversal. Struktur Node menyimpan data serta pointer ke anak kiri dan kanan, sedangkan fungsi buatNode digunakan untuk membuat node baru. Proses insert menempatkan data sesuai aturan BST (lebih kecil ke kiri, lebih besar ke kanan), search mencari data secara rekursif berdasarkan perbandingan nilai, dan hapus menghilangkan node dengan mempertimbangkan tiga kondisi (node tanpa anak, satu anak, atau dua anak dengan mengganti nilai menggunakan node terkecil di subtree kanan). Fungsi update dilakukan dengan cara menghapus data lama lalu menyisipkan data baru. Untuk menampilkan isi tree, disediakan traversal preorder, inorder, dan postorder. Pada main, program mendemonstrasikan seluruh operasi tersebut sehingga pengguna dapat melihat perubahan struktur tree sebelum dan sesudah update maupun delete.


## Unguided

### Soal 1
Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file
“bstree.h”.
### bstree.h
```go
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

// ADT BST
typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

// deklarasi fungsi
address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void InOrder(address root);

#endif

```

### bstree.cpp
```
#include "bstree.h"

// alokasi node baru
address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

// insert node ke BST
void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
    // jika sama, tidak dimasukkan (BST unik)
}

// mencari node
address findNode(infotype x, address root) {
    if (root == NULL || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

// traversal inorder
void InOrder(address root) {
    if (root != NULL) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}

```

### mainb.cpp
```
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); // duplikat, tidak dimasukkan
    insertNode(root, 7);

    InOrder(root);
    cout << endl;

    return 0;
}

```

>Program di atas merupakan program yang mengimplementasikan Binary Search Tree (BST) menggunakan struktur linked list. Program ini mendefinisikan struktur Node yang memiliki data dan dua pointer anak (kiri dan kanan), serta menyediakan fungsi dasar seperti alokasi node, penyisipan data sesuai aturan BST, pencarian data, dan traversal InOrder untuk menampilkan data secara terurut. Implementasi dipisahkan ke dalam file header dan source agar kode lebih terstruktur, modular, dan mudah digunakan kembali.

### Soal 2
Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.
➢ fungsi hitungJumlahNode( root:address ) : integer
/* fungsi mengembalikan integer banyak node yang ada di dalam BST*/
➢ fungsi hitungTotalInfo( root:address, start:integer ) : integer
/* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/
➢ fungsi hitungKedalaman( root:address, start:integer ) : integer
/* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */

### update bstree.h
```
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void InOrder(address root);

// nomor 2
int hitungJumlahNode(address root);
int hitungTotal(address root);
int hitungKedalaman(address root, int start);

#endif

```

### update bstree.cpp

```

#include "bstree.h"

// alokasi node baru
address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

// insert node ke BST
void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
    // jika sama, tidak dimasukkan (BST unik)
}

// mencari node
address findNode(infotype x, address root) {
    if (root == NULL || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

// traversal inorder
void InOrder(address root) {
    if (root != NULL) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}

//no2

// menghitung jumlah node
int hitungJumlahNode(address root) {
    if (root == NULL)
        return 0;
    return 1 + hitungJumlahNode(root->left)
             + hitungJumlahNode(root->right);
}

// menghitung total nilai seluruh node
int hitungTotal(address root) {
    if (root == NULL)
        return 0;
    return root->info + hitungTotal(root->left)
                       + hitungTotal(root->right);
}

// menghitung kedalaman maksimum (height)
int hitungKedalaman(address root, int start) {
    if (root == NULL)
        return start - 1;

    int kiri  = hitungKedalaman(root->left, start + 1);
    int kanan = hitungKedalaman(root->right, start + 1);

    return (kiri > kanan) ? kiri : kanan;
}

```

### update main.cpp

```
#include <iostream>
#include "bstree.h"
#include "bstree.cpp"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    InOrder(root);
    cout << endl;

    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah node : " << hitungJumlahNode(root) << endl;
    cout << "total : " << hitungTotal(root) << endl;

    return 0;
}

```

>Kita tambahkan fungsi rekursif untuk melakukan perhitungan pada BST, yaitu menghitung jumlah node (hitungJumlahNode), menghitung total nilai seluruh node (hitungTotal), dan menghitung kedalaman maksimum pohon (hitungKedalaman). Setiap fungsi memanfaatkan sifat rekursif BST dengan cara mengunjungi subtree kiri dan kanan hingga mencapai node kosong (NULL). Hasil perhitungan ini memberikan informasi penting tentang ukuran, isi, dan tinggi struktur tree yang telah dibentuk.

### Soal 3
Print tree secara pre-order dan post-order.

### tambahkan deklarasi berikut pada bstree.h
```
void InOrder(address root);
void PreOrder(address root);
void PostOrder(address root);

```
### Tambahkan implementasi fungsi traversal

```
// traversal PreOrder: root -> left -> right
void PreOrder(address root) {
    if (root != NULL) {
        cout << root->info << " - ";
        PreOrder(root->left);
        PreOrder(root->right);
    }
}

// traversal PostOrder: left -> right -> root
void PostOrder(address root) {
    if (root != NULL) {
        PostOrder(root->left);
        PostOrder(root->right);
        cout << root->info << " - ";
    }
}

```
### Tambahkan pemanggilan traversal sesuai ilustrasi soal
```
#include <iostream>
#include "bstree.h"
#include "bstree.cpp"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;

    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 7);
    insertNode(root, 2);
    insertNode(root, 5);
    insertNode(root, 1);
    insertNode(root, 3);

    cout << "InOrder   : ";
    InOrder(root);
    cout << endl;

    cout << "PreOrder  : ";
    PreOrder(root);
    cout << endl;

    cout << "PostOrder : ";
    PostOrder(root);
    cout << endl;

    return 0;
}

```
>Kita tambahkan operasi traversal PreOrder dan PostOrder untuk menampilkan isi BST dengan urutan yang berbeda. Traversal PreOrder menampilkan data dengan urutan akar–kiri–kanan, sedangkan PostOrder menggunakan urutan kiri–kanan–akar. Kedua traversal ini berguna untuk memahami struktur tree secara hierarkis serta sering digunakan dalam proses penyimpanan atau penghapusan tree. Dengan tambahan traversal ini, BST memiliki fasilitas tampilan yang lengkap selain InOrder.

## Referensi
https://www.w3schools.com/go/index.php
