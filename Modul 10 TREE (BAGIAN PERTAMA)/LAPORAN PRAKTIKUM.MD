# <h1 align="center">Laporan Praktikum Modul 10 Tree (Bagian Pertama) <br> Modul 10 Tree (Bagian Pertama)  </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Tree merupakan struktur data non-linear yang digunakan untuk merepresentasikan data secara hierarkis, di mana setiap elemen disebut node dan saling terhubung melalui relasi parent dan child, dengan satu node utama sebagai root. Salah satu jenis tree yang sering digunakan adalah Binary Search Tree (BST), yaitu binary tree yang memiliki aturan bahwa nilai pada subtree kiri harus lebih kecil dari node induk, sedangkan nilai pada subtree kanan harus lebih besar, sehingga memudahkan proses pencarian, penyisipan, dan pengolahan data. Implementasi tree sangat erat kaitannya dengan konsep rekursif, karena setiap subtree memiliki struktur yang sama dengan tree utama, sehingga operasi seperti insert, traversal, perhitungan jumlah node, dan kedalaman tree dapat dilakukan dengan fungsi yang memanggil dirinya sendiri sampai mencapai kondisi dasar (base case). Traversal pada tree merupakan proses mengunjungi seluruh node dengan urutan tertentu, seperti inorder, preorder, dan postorder, yang masing-masing memiliki kegunaan berbeda dalam pengolahan dan penampilan data.

## Guided

### 1. Tree
```
#include <iostream>
using namespace std;

#define MAX 5

struct Queue {
    int data [MAX];
    int head;
    int tail;
};

void createQueue (Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q){
    return (Q.tail == MAX - 1);
}

void printQueue (Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue Kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x){
    if (isFull(Q)){
        cout << " Queue penuh! tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueu: "<< x << endl;
    }
}

void dequeue (Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue Kosong! tidak ada data yang di hapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head]<< endl;
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            for (int i = Q.head; i < Q.tail; i++){
                Q.data[i] = Q.data[i+1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    createQueue;

    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

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
> ![Screenshot bagian 1](OUTPUT/output1.png)
> ![Screenshot bagian 2](OUTPUT/output2.png)
> ![Screenshot bagian 3](OUTPUT/output3.png)

Soal 1 Program di atas digunakan untuk membuat dan mengimplementasikan Binary Search Tree menggunakan linked list, yang mencakup proses alokasi node, penyisipan data ke dalam tree sesuai aturan BST, serta penampilan data menggunakan traversal inorder sehingga data ditampilkan dalam urutan terurut.

Soal 2 Program di atas digunakan untuk menghitung karakteristik dari Binary Search Tree, yaitu jumlah node, total nilai seluruh node, dan kedalaman maksimum tree dengan memanfaatkan fungsi rekursif pada setiap subtree.

Soal 3 Program di atas digunakan untuk menampilkan isi Binary Search Tree menggunakan traversal preorder dan postorder untuk menunjukkan perbedaan urutan kunjungan node dalam struktur tree.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://www.neliti.com/publications/224902/keamanan-database-menggunakan-metode-enkripsi
