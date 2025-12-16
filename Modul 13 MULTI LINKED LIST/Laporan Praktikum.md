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
Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file
“bstree.h”:
Type infotype: integer
Type address : pointer to Node
Type Node: <
info : infotype
left, right : address
>
function alokasi( x : infotype ) → address
procedure insertNode( input/output root : address,
input x : infotype )
function findNode( x : infotype, root : address )→address
procedure printInorder( input root : address )
Buatlah implementasi ADT Binary Search Tree pada file “bstree.cpp” dan cobalah hasil
implementasi ADT pada file “main.cpp”
#include <iostream>
#include "bstree.h"
using namespace std;
int main() {
cout << "Hello World" << endl;
address root = Nil;
insertNode(root,1);
insertNode(root,2);
insertNode(root,6);
insertNode(root,4);
insertNode(root,5);
insertNode(root,3);
insertNode(root,6);
insertNode(root,7);
InOrder(root);
return 0;

### Soal 2
Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.
➢ fungsi hitungJumlahNode( root:address ) : integer
/* fungsi mengembalikan integer banyak node yang ada di dalam BST*/
➢ fungsi hitungTotalInfo( root:address, start:integer ) : integer
/* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/
➢ fungsi hitungKedalaman( root:address, start:integer ) : integer
Gambar 10-15 Output

STRUKTUR DATA 89
/* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */
int main() {
cout << "Hello World" << endl;
address root = Nil;
insertNode(root,1);
insertNode(root,2);
insertNode(root,6);
insertNode(root,4);
insertNode(root,5);
insertNode(root,3);
insertNode(root,6);
insertNode(root,7);
InOrder(root);
cout<<"\n";
cout<<"kedalaman : "<<hitungKedalaman(root,0)<<endl;
cout<<"jumlah Node : "<<hitungNode(root)<<endl;
cout<<"total : "<<hitungTotal(root)<<endl;
return 0;
}

### Soal 3
Print tree secara pre-order dan post-order.

bstree.h
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
