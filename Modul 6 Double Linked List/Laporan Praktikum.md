# <h1 align="center">Laporan Praktikum Modul 6 <br> Modul 6 Double Linked List </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Double linked list merupakan salah satu bentuk struktur data dinamis yang menggunakan dua pointer untuk menghubungkan setiap elemen (node) dalam dua arah, yaitu ke depan (next) dan ke belakang (prev). Setiap node pada doubly linked list terdiri dari tiga bagian utama, yaitu data (info), penunjuk ke node berikutnya, dan penunjuk ke node sebelumnya. Struktur ini menggunakan dua pointer utama — first (atau head) untuk menunjuk elemen pertama dan last (atau tail) untuk menunjuk elemen terakhir pada list. Operasi dasar yang dapat dilakukan meliputi penambahan elemen di awal, akhir, atau setelah elemen tertentu (insert), penghapusan elemen di berbagai posisi (delete), pembaruan data (update), serta penelusuran data dari depan maupun belakang (traversal). Kelebihan doubly linked list dibandingkan singly linked list adalah kemampuannya bergerak dua arah, sehingga mempermudah proses penghapusan atau penyisipan di tengah list tanpa perlu menelusuri dari awal.
## Guided

### 1. Double Linked List
```
//double linked list untuk undo reundo, lebih kcil singly karena single atau cm menunjuk 1
//prev pengait belakang
//next pengait depan
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;


void insertDepan(int data) {
    Node* newNode = new Node(); //datanglah andi
    newNode -> data = data; 
    newNode -> prev  = nullptr; //ngisi yg sebelumnya, tangan andi kosong
    newNode -> next = head;

    if (head != nullptr)
        head -> prev = newNode; 
    else
        tail = newNode;

    head = newNode;
    cout << "Data " << data << "Berhasil di tambahkan di depan.\n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode -> data = data;
    newNode -> next = nullptr;
    newNode -> prev = tail;

    if (tail != nullptr)
        tail -> next = newNode;
    else 
        head = newNode;

    tail = newNode;
    cout << "Data " << data << "Berhasil di tambahkan di belakang.\n";
}

void insertSetelah(int target, int data){
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current -> next;

    if (current == nullptr){
        cout << "Data " << target << "Tidak Ditemukan.\n";
        return;
    } 

    Node* newNode = new Node();
    newNode -> data = data;
    newNode -> next = current -> next;
    newNode -> prev = current;

    if (current -> next != nullptr)
        current -> next -> prev = newNode;
    else 
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << "Berhasil di sisipkan setelah.\n" << target << ".\n";
}

void hapusDepan(){
    if (head == nullptr){
        cout << "List Kosong.\n";
        return; //ngecek
    }

    Node* temp = head; 
    head = head->next; //mengganti kedudukan
 
    if (head != nullptr) 
        head->prev = nullptr; //ngecek headnya
    else
        tail = nullptr;

    cout << "Data " << temp->data << "dihapus dari depan.\n";
    delete temp; //menghapus
}

void hapusBelakang(){
    if (tail == nullptr){
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail -> prev;

    if (tail != nullptr)
        tail -> next = nullptr;
    else
        head = nullptr;


    cout << "Data" << temp -> data << "dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    if (head == nullptr) {
        cout << "List Kosong.\n";
        return;
    }
     Node* current = head;
     while (current != nullptr && current->data != target)
        current = current -> next;

    if (current == nullptr){
        cout << "Data" << target << "Tidak Ditemukan.\n";
        return;
    }

    if (current == head){
        hapusDepan();
    } else if (current == tail){
        hapusBelakang();
    } else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        
        cout << "Data " << current->data << " telah dihapus dari tengah list.\n";
        delete current; 
    }
}
void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}
void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}


```

Penjelasan Program :
Program di atas menggunakan double linked list, yaitu struktur data yang tiap elemennya (node) punya dua pengait: satu ke depan (next) dan satu ke belakang (prev). Dengan dua arah ini, program bisa menambah, menghapus, mengubah, atau menampilkan data baik dari depan maupun belakang dengan mudah. Dua pointer utama, head dan tail, dipakai untuk menandai awal dan akhir dari list. Kelebihan double linked list dibandingkan single linked list adalah bisa bergerak bolak-balik, sehingga cocok untuk fitur seperti undo dan redo.


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
> ![Screenshot bagian x](OUTPUT/OUTPUT1.png)

Program di atas merupakan sistem antrian pembeli yang dibuat menggunakan konsep single linked list. Program ini memiliki beberapa fungsi utama, yaitu tambahAntrian() untuk menambah data pembeli baru ke bagian akhir antrian, layaniAntrian() untuk melayani dan menghapus pembeli yang berada di urutan pertama, tampilkanAntrian() untuk menampilkan seluruh data pembeli yang sedang mengantri, serta cariPembeli() untuk mencari pembeli berdasarkan nama atau pesanan dengan bantuan fungsi pembanding sama(). Semua fungsi tersebut dijalankan melalui menu utama di dalam main(), sehingga pengguna dapat dengan mudah menambah, mencari, melayani, dan melihat daftar antrian pembeli sesuai prinsip FIFO (First In First Out).


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://rtheunissen.github.io/bst/docs/references/2013_drozdek_delete.pdf
3. https://www.wscubetech.com/resources/dsa/doubly-linked-list-data-structure

