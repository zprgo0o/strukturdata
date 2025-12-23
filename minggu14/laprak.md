# <h1 align="center">Laporan Praktikum Modul 14 <br> Graph</h1>
<p align="center">Syahdan Awal Ramadhan - 103112430164</p>

## Dasar Teori
Graph merupakan himpunan tidak kosong dari node (vertec) dan garis penghubung (edge). Contoh
sederhana tentang graph, yaitu antara Tempat Kost Anda dengan Common Lab. Tempat Kost Anda
dan Common Lab merupakan node (vertec). Jalan yang menghubungkan tempat Kost dan Common
Lab merupakan garis penghubung antara keduanya (edge).

## Guided

### graf.h

```
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif

```
### graf.cpp
```
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

```
### main.cpp
```
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}

```

## Unguided

### Soal 1
Buatlah ADT Graph tidak berarah file “graph.h”.
### graph.h
```
#ifndef GRAPH_H
#define GRAPH_H

#include <iostream>
using namespace std;

/* ====== TYPE DEFINITION ====== */
typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

/* ====== ELEMEN EDGE ====== */
struct ElmEdge {
    adrNode Node;
    adrEdge Next;
};

/* ====== ELEMEN NODE ====== */
struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode Next;
};

/* ====== GRAPH ====== */
struct Graph {
    adrNode first;
};

/* ====== PROTOTYPE ====== */
void CreateGraph(Graph &G);
adrNode InsertNode(Graph &G, infoGraph x);
void ConnectNode(adrNode N1, adrNode N2);
void PrintInfoGraph(Graph G);

#endif

```
### graph.cpp
```
#include "graph.h"

/* ====== CREATE GRAPH ====== */
void CreateGraph(Graph &G) {
    G.first = NULL;
}

/* ====== INSERT NODE ====== */
adrNode InsertNode(Graph &G, infoGraph x) {
    adrNode P = new ElmNode;
    P->info = x;
    P->visited = 0;
    P->firstEdge = NULL;
    P->Next = G.first;
    G.first = P;
    return P;
}

/* ====== CONNECT NODE (UNDIRECTED) ====== */
void ConnectNode(adrNode N1, adrNode N2) {
    adrEdge E1 = new ElmEdge;
    E1->Node = N2;
    E1->Next = N1->firstEdge;
    N1->firstEdge = E1;

    adrEdge E2 = new ElmEdge;
    E2->Node = N1;
    E2->Next = N2->firstEdge;
    N2->firstEdge = E2;
}

/* ====== PRINT GRAPH ====== */
void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        cout << P->info << " : ";
        adrEdge E = P->firstEdge;
        while (E != NULL) {
            cout << E->Node->info << " ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}

```
### main.cpp
```
#include "graph.h"
#include "graph.cpp"

int main() {
    Graph G;
    CreateGraph(G);

    adrNode A = InsertNode(G, 'A');
    adrNode B = InsertNode(G, 'B');
    adrNode C = InsertNode(G, 'C');
    adrNode D = InsertNode(G, 'D');
    adrNode E = InsertNode(G, 'E');
    adrNode F = InsertNode(G, 'F');
    adrNode Gg = InsertNode(G, 'G');
    adrNode H = InsertNode(G, 'H');

    ConnectNode(A, B);
    ConnectNode(A, C);
    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, Gg);
    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(Gg, H);

    PrintInfoGraph(G);

    return 0;
}
```


### Soal 2
Buatlah prosedur untuk menampilkanhasil penelusuran DFS.

### tambahkan prototype DFS di bawah ini pada file graph.h
```
void ResetVisited(Graph &G);
void PrintDFS(Graph G, adrNode N);
```

### tambahkan source code di bawah ini pada file graph.cpp
```
void ResetVisited(Graph &G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    if (N == NULL || N->visited == 1)
        return;

    cout << N->info << " ";
    N->visited = 1;

    adrEdge E = N->firstEdge;
    while (E != NULL) {
        PrintDFS(G, E->Node);
        E = E->Next;
    }
}

```

### tambahkan pemanggilan DFS pada main.cpp

```
#include "graph.h"
#include "graph.cpp"

int main() {
    Graph G;
    CreateGraph(G);

    adrNode A = InsertNode(G, 'A');
    adrNode B = InsertNode(G, 'B');
    adrNode C = InsertNode(G, 'C');
    adrNode D = InsertNode(G, 'D');
    adrNode E = InsertNode(G, 'E');
    adrNode F = InsertNode(G, 'F');
    adrNode Gg = InsertNode(G, 'G');
    adrNode H = InsertNode(G, 'H');

    ConnectNode(A, B);
    ConnectNode(A, C);
    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, Gg);
    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(Gg, H);

    cout << "DFS mulai dari node A : ";
    ResetVisited(G);
    PrintDFS(G, A);

    return 0;
}

```


### Soal 3
Buatlah prosedur untuk menampilkanhasil penelusuran DFS.

### tambahkan prosedur BFS di bawah ini pada file graph.h
```
void PrintBFS(Graph G, adrNode N);

```

### tambahkan source code dibawah ini pada file graph.cpp
```
#include <queue>

/* ====== BFS ====== */
void PrintBFS(Graph G, adrNode N) {
    if (N == NULL) return;

    queue<adrNode> Q;
    N->visited = 1;
    Q.push(N);

    while (!Q.empty()) {
        adrNode P = Q.front();
        Q.pop();
        cout << P->info << " ";

        adrEdge E = P->firstEdge;
        while (E != NULL) {
            if (E->Node->visited == 0) {
                E->Node->visited = 1;
                Q.push(E->Node);
            }
            E = E->Next;
        }
    }
}
```

### edit file main.cpp menjadi seperti dibawah ini

```
#include "graph.h"
#include "graph.cpp"
#include <iostream>
using namespace std;

/* ====== MENU ====== */
void menu() {
    cout << "\n===== MENU GRAPH =====\n";
    cout << "1. Tambah Node\n";
    cout << "2. Hubungkan Dua Node\n";
    cout << "3. Tampilkan Graph\n";
    cout << "4. DFS (Mulai dari Node)\n";
    cout << "5. BFS (Mulai dari Node)\n";
    cout << "0. Keluar\n";
    cout << "Pilih menu : ";
}

/* ====== CARI NODE BERDASARKAN INFO ====== */
adrNode findNode(Graph G, infoGraph x) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == x)
            return P;
        P = P->Next;
    }
    return NULL;
}

int main() {
    Graph G;
    CreateGraph(G);

    int pilih;
    infoGraph x, y;
    adrNode N1, N2;

    do {
        menu();
        cin >> pilih;

        switch (pilih) {
        case 1:
            cout << "Masukkan nama node (char) : ";
            cin >> x;
            InsertNode(G, x);
            cout << "Node berhasil ditambahkan\n";
            break;

        case 2:
            cout << "Masukkan node pertama : ";
            cin >> x;
            cout << "Masukkan node kedua   : ";
            cin >> y;

            N1 = findNode(G, x);
            N2 = findNode(G, y);

            if (N1 != NULL && N2 != NULL) {
                ConnectNode(N1, N2);
                cout << "Node berhasil dihubungkan\n";
            } else {
                cout << "Salah satu node tidak ditemukan!\n";
            }
            break;

        case 3:
            cout << "\nAdjacency List Graph:\n";
            PrintInfoGraph(G);
            break;

        case 4:
            cout << "Mulai DFS dari node : ";
            cin >> x;
            N1 = findNode(G, x);
            if (N1 != NULL) {
                ResetVisited(G);
                cout << "Hasil DFS : ";
                PrintDFS(G, N1);
                cout << endl;
            } else {
                cout << "Node tidak ditemukan!\n";
            }
            break;

        case 5:
            cout << "Mulai BFS dari node : ";
            cin >> x;
            N1 = findNode(G, x);
            if (N1 != NULL) {
                ResetVisited(G);
                cout << "Hasil BFS : ";
                PrintBFS(G, N1);
                cout << endl;
            } else {
                cout << "Node tidak ditemukan!\n";
            }
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
## Referensi
1. https://www.w3schools.com/go/index.php
