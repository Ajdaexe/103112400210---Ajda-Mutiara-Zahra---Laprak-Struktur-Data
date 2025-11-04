# <h1 align="center">Laporan Praktikum Modul 7 <br> Modul 7 Stack </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Stack merupakan salah satu bentuk struktur data dinamis yang menggunakan prinsip LIFO (Last In First Out), artinya data yang terakhir dimasukkan akan menjadi data yang pertama dikeluarkan. Struktur stack bekerja seperti tumpukan benda di mana elemen yang paling atas adalah yang pertama bisa diambil. Dalam implementasinya, stack dapat direpresentasikan dengan pointer (linked list) maupun tabel (array). Komponen utama stack adalah TOP, yaitu penunjuk ke elemen paling atas yang menjadi satu-satunya titik akses untuk melakukan operasi. Dua operasi dasar pada stack adalah push dan pop. Operasi push digunakan untuk menambah elemen baru ke bagian atas stack, sedangkan pop digunakan untuk menghapus elemen teratas dari stack. Selain itu, terdapat juga fungsi tambahan seperti isEmpty() untuk memeriksa apakah stack kosong, createStack() untuk membuat stack baru, serta fungsi pencarian atau tampilan isi stack. Representasi stack dengan pointer bersifat dinamis karena memanfaatkan alokasi memori saat program berjalan, sedangkan representasi tabel bersifat statis dengan ukuran tertentu yang sudah ditentukan sebelumnya. Konsep stack ini banyak digunakan dalam pemrograman, seperti dalam proses pemanggilan fungsi (function call), pengelolaan memori, serta proses undo-redo pada aplikasi komputer.

## Guided

### 1. Double Linked List
```
//pop hapus data
//top hrus di depan antara stack
//newnode -> next = akses var, node baru selaku jadi top
//pakai library stack gpp
//fungsi size, buuat ukuran stack

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

void push(Node *&top, int data)
{
    Node *newNode = new Node();
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop (Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    Node *temp = top;
    top = top -> next;

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
        cout << temp -> data << "->";
        temp = temp -> next;
    }

    cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan Isi Stack" << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: "<< endl;
    show(stack);

    return 0;
}
```

Penjelasan Program :
Program di atas menggunakan double linked list, yaitu struktur data yang tiap elemennya (node) punya dua pengait: satu ke depan (next) dan satu ke belakang (prev). Dengan dua arah ini, program bisa menambah, menghapus, mengubah, atau menampilkan data baik dari depan maupun belakang dengan mudah. Dua pointer utama, head dan tail, dipakai untuk menandai awal dan akhir dari list. Kelebihan double linked list dibandingkan single linked list adalah bisa bergerak bolak-balik, sehingga cocok untuk fitur seperti undo dan redo.Program di atas untuk membuat dan mengelola struktur data stack menggunakan pointer dan linked list di C++. Stack bekerja dengan prinsip LIFO (Last In, First Out), di mana data yang terakhir masuk akan keluar lebih dulu (Rosen, 2012). Fungsi isEmpty() dipakai untuk mengecek apakah stack kosong, push() untuk menambah data baru di bagian atas stack, pop() untuk menghapus data teratas dan mengembalikannya, sedangkan show() digunakan untuk menampilkan semua isi stack dari atas ke bawah. Di fungsi main(), program membuat stack kosong, lalu menambahkan data 10, 20, dan 30 ke dalamnya, menampilkan hasilnya, menghapus satu data paling atas dengan pop(), dan akhirnya menampilkan sisa isi stack setelah penghapusan tersebut.


## Unguided

### Soal 1

Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:
Type infotype : kendaraan <
 nopol : string
 warna : string
 thnBuat : integer
>
Type address : pointer to ElmList
Type ElmList <
 info : infotype
 next :address
 prev : address
>
Type List <
 First : address
 Last : address
>
procedure CreateList( input/output L : List )
function alokasi( x : infotype ) → address
procedure dealokasi(input/output P : address )
procedure printInfo( input L : List )
procedure insertLast(input/output L : List,
 input P : address )
Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil
implementasi ADT pada file “main.cpp”.

Carilah elemen dengan nomor polisi D001 dengan membuat fungsi baru.
fungsi findElm( L : List, x : infotype ) : address

Hapus elemen dengan nomor polisi D003 dengan procedure delete.
- procedure deleteFirst( input/output L : List,
 P : address )
- procedure deleteLast( input/output L : List,
 P : address )
- procedure deleteAfter( input Prec : address,
 input/output P : address )

doublylist.h
```
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>

using namespace std;

#define Nil NULL

typedef struct {
    string nopol;
    string warna;
    int thnBuat;
} infotype;

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertLast(List &L, address P);
void printInfo(List L);
address findElm(List L, string nopol);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);

#endif
```

doublylist.cpp
```
#include "doublylist.h"

int main() {
    List L;
    CreateList(L);
    
    infotype data;
    address P, P_deleted;
    string nopol_cari, nopol_hapus;

    cout << "--- SOAL 1: PROSES INSERT DATA ---" << endl;
    cout << "(Program akan meminta input 4 kali)" << endl;

    for (int i = 0; i < 4; i++) {
        cout << "\n--- Data ke-" << (i + 1) << " ---" << endl;
        cout << "masukkan nomor polisi: ";
        cin >> data.nopol;
        cout << "masukkan warna kendaraan: ";
        cin >> data.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> data.thnBuat;

        if (findElm(L, data.nopol) != Nil) {
            cout << "nomor polisi sudah terdaftar" << endl; 
        } else {
            P = alokasi(data);
            insertLast(L, P);
            cout << "Data " << data.nopol << " berhasil ditambahkan." << endl;
        }
    }

    cout << "\nDATA LIST 1" << endl; 
    printInfo(L);
    cout << "------------------------------------" << endl << endl;

    
    cout << "--- SOAL 2: CARI DATA ---" << endl;
    cout << "Masukkan Nomor Polisi yang dicari : "; 
    cin >> nopol_cari; 

    P = findElm(L, nopol_cari);
    if (P != Nil) {
        cout << "Data Ditemukan:" << endl;
        cout << "Nomor Polisi: " << P->info.nopol << endl; 
        cout << "Warna         : " << P->info.warna << endl; 
        cout << "Tahun         : " << P->info.thnBuat << endl; 
    } else {
        cout << "Data tidak ditemukan." << endl;
    }
    cout << "------------------------------------" << endl << endl;


    cout << "--- SOAL 3: HAPUS DATA ---" << endl;
    cout << "Masukkan Nomor Polisi yang akan dihapus : "; 
    cin >> nopol_hapus; 

    P = findElm(L, nopol_hapus);
    if (P != Nil) {
        if (P == L.First) {
            deleteFirst(L, P_deleted);
        } else if (P == L.Last) {
            deleteLast(L, P_deleted);
        } else {
            address Prec = P->prev;
            deleteAfter(L, Prec, P_deleted);
        }
        cout << "Data dengan nomor polisi " << nopol_hapus << " berhasil dihapus." << endl; 
        dealokasi(P_deleted);
    } else {
        cout << "Data tidak ditemukan, tidak ada yang dihapus." << endl;
    }

    cout << "\nDATA LIST 1 (Setelah Hapus)" << endl; 
    printInfo(L);
    cout << "------------------------------------" << endl;

    return 0;
}
```
MAIN.cpp
```
#include "doublylist.h"

void CreateList(List &L) {
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    P->prev = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
}

void insertLast(List &L, address P) {
    if (L.First == Nil) {
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

void printInfo(List L) {
    address P = L.Last;
    if (P == Nil) {
        cout << "List Kosong" << endl;
    } else {
        while (P != Nil) {
            cout << "no polisi : " << P->info.nopol << endl;
            cout << "warna     : " << P->info.warna << endl;
            cout << "tahun     : " << P->info.thnBuat << endl;
            P = P->prev;
        }
    }
}

address findElm(List L, string nopol) {
    address P = L.First;
    while (P != Nil) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return Nil;
}

void deleteFirst(List &L, address &P) {
    P = L.First;
    if (L.First == L.Last) {
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.First = P->next;
        L.First->prev = Nil;
        P->next = Nil;
    }
}

void deleteLast(List &L, address &P) {
    P = L.Last;
    if (L.First == L.Last) {
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.Last = P->prev;
        L.Last->next = Nil;
        P->prev = Nil;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    P = Prec->next;
    Prec->next = P->next;
    (P->next)->prev = Prec;
    P->next = Nil;
    P->prev = Nil;
}
```

> Output
> ![Screenshot bagian x](OUTPUT/OUTPUT1.PNG)
> ![Screenshot bagian x](OUTPUT/OUTPUT2.PNG)

Program di atas merupakan sistem antrian pembeli yang dibuat menggunakan konsep single linked list. Program ini memiliki beberapa fungsi utama, yaitu tambahAntrian() untuk menambah data pembeli baru ke bagian akhir antrian, layaniAntrian() untuk melayani dan menghapus pembeli yang berada di urutan pertama, tampilkanAntrian() untuk menampilkan seluruh data pembeli yang sedang mengantri, serta cariPembeli() untuk mencari pembeli berdasarkan nama atau pesanan dengan bantuan fungsi pembanding sama(). Semua fungsi tersebut dijalankan melalui menu utama di dalam main(), sehingga pengguna dapat dengan mudah menambah, mencari, melayani, dan melihat daftar antrian pembeli sesuai prinsip FIFO (First In First Out).


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://jurnal.stkippersada.ac.id/jurnal/index.php/jutech/article/view/4263
3. https://www.irjet.net/archives/V5/i3/IRJET-V5I3434.pdf
