# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack </h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori

Stack (tumpukan) adalah struktur data yang meniru bagaimana proses menyimpan dan mengambil suatu buku pada suatu tumpukan buku yang ada di lantai. Apabila diperhatikan dengan seksama maka proses menyimpa buku (disebut push) dan proses mengambil buku (disebut pop) dari suatu tumpukan selalu dilakukan pada bagian atas tumpukan (top of the stack ) sehingga terjadi urutan yang disebut LIFO (Last In First Out).
## Guided

```
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}
void push (Node *&top, int data)
{
    Node *newNode = new Node();
    newNode-> data = data;
    newNode-> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }
    int poppedData = top-> data;
    Node *temp = top;
    top = top-> next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
{
    cout << "Stack Kosong." << endl;
    return;
}
cout << "TOP ->";
Node *temp = top;

while (temp != nullptr)
{
    cout << temp-> data << " ->";
    temp = temp-> next;
}
cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push (stack, 10);
    push (stack, 20);
    push (stack, 30);

    cout << "Menampilkan isi stack: " << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: " << endl;
    show(stack);
    
    return 0;
}
```


## Unguided

### Soal no 1
stack.h

```
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

// Deklarasi fungsi/prosedur
void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(const Stack &S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);

#endif

```

stack.cpp

```
#include <iostream>
#include "stack.h"
using namespace std;

// Membuat stack kosong
void createStack(Stack &S) {
    S.top = -1;
}

// Mengecek apakah stack penuh
bool isFull(const Stack &S) {
    return S.top == MAX - 1;
}

// Mengecek apakah stack kosong
bool isEmpty(const Stack &S) {
    return S.top == -1;
}

// Push biasa
void push(Stack &S, infotype x) {
    if (!isFull(S)) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

// Pop
infotype pop(Stack &S) {
    if (!isEmpty(S)) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

// Menampilkan isi stack
void printInfo(const Stack &S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

// Membalik isi stack
void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (!isEmpty(S)) {
        push(temp, pop(S));
    }
    S = temp;
}

// Push Ascending: memastikan data dalam urutan menaik (dari bawah ke atas)
void pushAscending(Stack &S, infotype x) {
    if (isFull(S)) {
        cout << "Stack penuh!" << endl;
        return;
    }

    Stack temp;
    createStack(temp);

    // Pindahkan elemen yang lebih besar dari x
    while (!isEmpty(S) && S.info[S.top] < x) {
        push(temp, pop(S));
    }

    // Masukkan elemen baru
    push(S, x);

    // Kembalikan elemen dari temp
    while (!isEmpty(temp)) {
        push(S, pop(temp));
    }
}

// Membaca input user sampai Enter
void getInputStream(Stack &S) {
    cout << "Masukkan angka (tanpa spasi, akhiri dengan Enter): ";
    char c;
    while (cin.get(c) && c != '\n') {
        if (isdigit(c)) {
            push(S, c - '0');
        }
    }
}

```

main.cpp

```
#include <iostream>
#include "stack.h"
#include "stack.cpp"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    Stack S;
    createStack(S);
    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}

```

### soal no 2
pushAscending

```

#include <iostream>
#include "stack.h"
#include "stack.cpp"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    Stack S;
    createStack(S);
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}

```

### soal no 3
getInputStream

```

#include <iostream>
#include "stack.h"
#include "stack.cpp"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    Stack S;
    createStack(S);
    getInputStream(S);
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}


```


Program ADT **Stack menggunakan Array** ini terdiri dari tiga file utama: **`stack.h`**, **`stack.cpp`**, dan **`main.cpp`**. File `stack.h` berfungsi sebagai **header file** yang berisi definisi struktur data `Stack`, konstanta kapasitas, serta deklarasi seluruh prosedur dan fungsi yang akan digunakan. File `stack.cpp` berisi **implementasi logika dari semua operasi stack**, seperti `createStack`, `push`, `pop`, `printInfo`, `balikStack`, `pushAscending`, dan `getInputStream`, yang masing-masing menangani pembuatan stack, penambahan, penghapusan, penampilan, pembalikan, penyisipan berurutan, dan input data dari pengguna. Sementara itu, file `main.cpp` berfungsi sebagai **program utama** untuk menguji dan menjalankan ADT tersebut — memanggil prosedur-prosedur dari stack untuk menampilkan hasil kerja program sesuai contoh output yang diharapkan.


## Referensi
1. https://www.teachmesoft.com/2019/03/tumpukan-stack-dan-antrian-queue-c.html
2. https://www.w3schools.com/cpp/cpp_stacks.asp
