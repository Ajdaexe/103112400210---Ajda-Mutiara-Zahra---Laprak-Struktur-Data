# <h1 align="center">Laporan Praktikum Modul 13 Multi Linked List <br> Modul 13 Multi Linked List  </h1>
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
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node *address;

struct Node {
    infotype info;
    address left;
    address right;
};

// LATIHAN 1
address alokasi(infotype x);
void insertNode(address &root, infotype x);
void printInorder(address root);

// LATIHAN 2
int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root, int start);

// LATIHAN 3
void printPreOrder(address root);
void printPostOrder(address root);

#endif
```

bstree.cpp
```
#include "bstree.h"

// LATIHAN 1
address alokasi(infotype x) {
    address newNode = new Node;
    newNode->info = x;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

void printInorder(address root) {
    if (root != NULL) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}

// LATIHAN 2
int hitungJumlahNode(address root) {
    if (root == NULL) {
        return 0;
    }
    return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
}

int hitungTotalInfo(address root) {
    if (root == NULL) {
        return 0;
    }
    return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
}

int hitungKedalaman(address root, int start) {
    if (root == NULL) {
        return start;
    }
    int kiri = hitungKedalaman(root->left, start + 1);
    int kanan = hitungKedalaman(root->right, start + 1);

    if (kiri > kanan) {
        return kiri;
    } else {
        return kanan;
    }
}

// LATIHAN 3
void printPreOrder(address root) {
    if (root != NULL) {
        cout << root->info << " - ";
        printPreOrder(root->left);
        printPreOrder(root->right);
    }
}

void printPostOrder(address root) {
    if (root != NULL) {
        printPostOrder(root->left);
        printPostOrder(root->right);
        cout << root->info << " - ";
    }
}
```

main.cpp
```
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;
    
    address root = NULL;

    // LATIHAN 1
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    cout << "InOrder   : ";
    printInorder(root);
    cout << endl;

    // LATIHAN 2
    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah node : " << hitungJumlahNode(root) << endl;
    cout << "total : " << hitungTotalInfo(root) << endl;

    // LATIHAN 3
    cout << "\nPreOrder  : ";
    printPreOrder(root);
    cout << endl;

    cout << "PostOrder : ";
    printPostOrder(root);
    cout << endl;

    return 0;
}
```
> Output
> ![Screenshot bagian 1](OUTPUT/OUPUT123.PNG)


Soal 1 Program di atas digunakan untuk membuat dan mengimplementasikan Binary Search Tree menggunakan linked list, yang mencakup proses alokasi node, penyisipan data ke dalam tree sesuai aturan BST, serta penampilan data menggunakan traversal inorder sehingga data ditampilkan dalam urutan terurut.

Soal 2 Program di atas digunakan untuk menghitung karakteristik dari Binary Search Tree, yaitu jumlah node, total nilai seluruh node, dan kedalaman maksimum tree dengan memanfaatkan fungsi rekursif pada setiap subtree.

Soal 3 Program di atas digunakan untuk menampilkan isi Binary Search Tree menggunakan traversal preorder dan postorder untuk menunjukkan perbedaan urutan kunjungan node dalam struktur tree.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://www.neliti.com/publications/224902/keamanan-database-menggunakan-metode-enkripsi
