# <h1 align="center">Laporan Praktikum Modul 14 Graph <br> Modul 14 Graph  </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Multi Linked List merupakan struktur data non-linear yang terdiri dari beberapa linked list yang saling berhubungan, umumnya membentuk relasi antara elemen induk (parent) dan elemen anak (child). Setiap elemen induk dapat memiliki satu atau lebih elemen anak yang terhubung melalui pointer, sehingga membentuk hubungan satu-ke-banyak. Struktur ini memanfaatkan manajemen memori dinamis dan banyak digunakan untuk merepresentasikan data hierarkis, seperti data pegawai dengan data anak atau kategori dengan subkategori.

## Guided

### 1. MLL
```
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```

Penjelasan Program :
Program di atas adalah program C++ yang digunakan untuk mengimplementasikan struktur data Binary Search Tree (BST) dengan operasi dasar seperti insert, search, update, delete, dan traversal. Program mendefinisikan node dengan dua anak (kiri dan kanan), kemudian menggunakan fungsi rekursif untuk menyisipkan data sesuai aturan BST, mencari data, menghapus node berdasarkan jumlah anaknya, serta memperbarui data dengan cara menghapus nilai lama dan menambahkan nilai baru.

## Unguided

### Soal 1
Buatlah ADT Multi Linked list sebagai berikut di dalam file “circularlist.h”:

Type infotype : mahasiswa <
Nama:string
Nim:string
Jenis_kelamin:char
Ipk:float>
Type address : pointer to ElmList
Type ElmList <
info : infotype
next :address>
Type List <
First : address>

• Terdapat 11 fungsi/prosedur untuk ADT circularlist
o procedure CreateList( input/output L : List )
o function alokasi( x : infotype ) → address
o procedure dealokasi( input/output t P : address )
o procedure insertFirst( input/output L : List, input P : address )
o procedure insertAfter( input/output L : List, input Prec : address, P : address)
o procedure insertLast( input/output L : List, input P : address )
o procedure deleteFirst( input/output L : List, input/output P : address )
o procedure deleteAfter( input/output L : List, input Prec : address,
input/output t P : address )
o procedure deleteLast( input/output L : List, P : address )
o function findElm( L : List, x : infotype ) → address
o procedure printInfo( input L : List )

Keterangan :
• fungsi findElm mencari elemen di dalam list L berdasarkan nim
o fungsi mengembalikan elemen dengan dengan info nim == x.nim jika ditemukan

STRUKTUR DATA 100
o fungsi mengembalikan NIL jika tidak ditemukan

Gambar 13-8 Ilustrasi data

Buatlah implementasi ADT Doubly Linked list pada file “circularlist.cpp”. Tambahkan fungsi/prosedur
berikut pada file “main.cpp”.
• fungsi create ( in nama, nim : string, jenis_kelamin : char, ipk : float)
o fungsi disediakan, ketik ulang code yang diberikan
o fungsi mengalokasikan sebuah elemen list dengan info sesuai input
address createData(string nama, string nim, char jenis_kelamin, float ipk)
{
/**
* PR : mengalokasikan sebuah elemen list dengan info dengan info sesuai input
* FS : address P menunjuk elemen dengan info sesuai input
*/
infotype x;
address P;
x.nama = nama;
x.nim = nim;
x.jenis_kelamin = jenis_kelamin;
x.ipk = ipk;
P = alokasi(x);
return P;
}

Gambar 13-9 Fungsi create
Cobalah hasil implementasi ADT pada file “main.cpp”
int main()
{
List L, A, B, L2;
address P1 = Nil;
address P2 = Nil;
infotype x;
createList(L);
cout<<"coba insert first, last, dan after"<<endl;
P1 = createData("Danu", "04", 'l', 4.0);
insertFirst(L,P1);
P1 = createData("Fahmi", "06", 'l',3.45);
insertLast(L,P1);
P1 = createData("Bobi", "02", 'l',3.71);

STRUKTUR DATA 101
insertFirst(L,P1);
P1 = createData("Ali", "01", 'l', 3.3);
insertFirst(L,P1);
P1 = createData("Gita", "07", 'p', 3.75);
insertLast(L,P1);
x.nim = "07";
P1 = findElm(L,x);
P2 = createData("Cindi", "03", 'p', 3.5);
insertAfter(L, P1, P2);
x.nim = "02";
P1 = findElm(L,x);
P2 = createData("Hilmi", "08", 'p', 3.3);
insertAfter(L, P1, P2);
x.nim = "04";
P1 = findElm(L,x);
P2 = createData("Eli", "05", 'p', 3.4);
insertAfter(L, P1, P2);
printInfo(L);
return 0;


circularlist.h
```
#ifndef CIRCULARLIST_H
#define CIRCULARLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
};

typedef Mahasiswa infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address P);

void insertFirst(List &L, address P);
void insertLast(List &L, address P);
void insertAfter(List &L, address Prec, address P);

void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);

address findElm(List L, string nim);
void printInfo(List L);

#endif
```

circularlist.cpp
```
#include "circularlist.h"

void createList(List &L) {
    L.first = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    return P;
}

void dealokasi(address P) {
    delete P;
}

void insertFirst(List &L, address P) {
    if (L.first == NULL) {
        L.first = P;
        P->next = L.first;
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        P->next = L.first;
        last->next = P;
        L.first = P;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        insertFirst(L, P);
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        last->next = P;
        P->next = L.first;
    }
}

void insertAfter(List &L, address Prec, address P) {
    if (Prec != NULL) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.first == NULL) {
        P = NULL;
    } else if (L.first->next == L.first) {
        P = L.first;
        L.first = NULL;
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        P = L.first;
        L.first = L.first->next;
        last->next = L.first;
        P->next = NULL;
    }
}

void deleteLast(List &L, address &P) {
    if (L.first == NULL) {
        P = NULL;
    } else if (L.first->next == L.first) {
        deleteFirst(L, P);
    } else {
        address last = L.first;
        address prevLast = NULL;
        while (last->next != L.first) {
            prevLast = last;
            last = last->next;
        }
        P = last;
        prevLast->next = L.first;
        P->next = NULL;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != NULL && Prec->next != L.first) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = NULL;
    } else if (Prec->next == L.first) {
        deleteFirst(L, P);
    }
}

address findElm(List L, string nim) {
    if (L.first == NULL) return NULL;
    
    address P = L.first;
    do {
        if (P->info.nim == nim) {
            return P;
        }
        P = P->next;
    } while (P != L.first);
    
    return NULL;
}

void printInfo(List L) {
    if (L.first == NULL) {
        cout << "List Kosong" << endl;
    } else {
        address P = L.first;
        do {
            cout << "Nama : " << P->info.nama << endl;
            cout << "NIM  : " << P->info.nim << endl;
            cout << "L/P  : " << P->info.jenis_kelamin << endl;
            cout << "IPK  : " << P->info.ipk << endl;
            cout << "-----------------------" << endl;
            P = P->next;
        } while (P != L.first);
    }
}
```

main.cpp
```
#include <iostream>
#include "circularlist.h"

using namespace std;

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}

int main() {
    List L;
    address P1 = NULL;
    address P2 = NULL;
    
    createList(L);

    cout << "coba insert first, last, dan after" << endl;
    
    P1 = createData("Danu", "04", 'L', 4.0);
    insertFirst(L, P1);
    
    P1 = createData("Ali", "01", 'L', 3.3);
    insertFirst(L, P1);
    
    P1 = createData("Bobi", "02", 'L', 3.71);
    insertLast(L, P1);
    
    P1 = createData("Gita", "07", 'P', 3.75);
    insertLast(L, P1);

    address cari = findElm(L, "07");
    if (cari != NULL) {
        P2 = createData("Cindi", "03", 'P', 3.5);
        insertAfter(L, cari, P2);
    }

    cari = findElm(L, "02");
    if (cari != NULL) {
        P2 = createData("Hilmi", "08", 'L', 3.3);
        insertAfter(L, cari, P2);
    }

    cari = findElm(L, "04");
    if (cari != NULL) {
        P2 = createData("Eli", "05", 'P', 3.4);
        insertAfter(L, cari, P2);
    }
    
    P1 = createData("Fahmi", "06", 'L', 3.45);
    insertLast(L, P1);

    printInfo(L);

    return 0;
}
```
> Output
> ![Screenshot bagian 1](ouput/Screenshot 2025-12-16 122924.png)


Soal 1 Program di atas adalah program C++ yang mengimplementasikan Circular Linked List untuk menyimpan data mahasiswa. Program ini menggunakan pointer dan memori dinamis untuk melakukan operasi insert, pencarian data, dan penampilan isi list secara melingkar.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://www.neliti.com/publications/224902/keamanan-database-menggunakan-metode-enkripsi
