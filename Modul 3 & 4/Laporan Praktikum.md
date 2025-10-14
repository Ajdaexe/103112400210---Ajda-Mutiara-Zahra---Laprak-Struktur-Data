# <h1 align="center">Laporan Praktikum Modul 2 <br> Modul 2 Pengenalan Bahasa C++ (Bagian Dua) </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Abstract Data Type (ADT) merupakan konsep dasar dalam pemrograman yang digunakan untuk membuat tipe data baru yang memiliki struktur dan operasi tertentu sesuai kebutuhan. Salah satu penerapan dari ADT adalah Singly Linked List, yaitu struktur data dinamis yang tersusun dari simpul-simpul (node) yang saling terhubung melalui pointer. Setiap node terdiri dari dua bagian, yaitu data dan pointer yang menunjuk ke node berikutnya. Singly Linked List bersifat fleksibel karena ukurannya dapat bertambah atau berkurang selama program berjalan, berbeda dengan array yang bersifat statis. Operasi dasar yang dapat dilakukan pada struktur ini meliputi pembuatan list (create list), penambahan elemen (insert), penghapusan elemen (delete), penelusuran (view), pencarian data (search), dan pembaruan data (update). Dengan menerapkan konsep ADT pada Singly Linked List, pengelolaan data menjadi lebih efisien, terstruktur, dan mudah dikembangkan dalam pemrograman.

## Guided

### 1. Compile
*mahasiswa.h*
```
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif 
```
*mahasiswa.cpp*
```
#include "mahasiswa.h" 
#include <iostream> 
using namespace std; 

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m).nim;
    cout << "input nilai = ";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
```
*main.cpp*
```
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main()
{
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata - rata = " << rata2(mhs);
    return 0;
}
```

Penjelasan Program :
Program ini adalah contoh sederhana bagaimana kode C++ dapat dipecah menjadi beberapa file untuk meningkatkan keterbacaan dan pengelolaan proyek. File mahasiswa.h bertindak sebagai "header" yang berisi deklarasi atau "cetak biru" untuk struktur data mahasiswa dan prototipe (penjelasan singkat) dari fungsi-fungsi inputMhs serta rata2. Kemudian, file mahasiswa.cpp berfungsi sebagai "implementasi" di mana kode dari fungsi-fungsi tersebut ditulis secara lengkap. Terakhir, file main.cpp adalah program utama yang menyertakan (#include) file mahasiswa.h untuk dapat menggunakan struct dan fungsi yang telah didefinisikan, sehingga program dapat berjalan dengan menginput data mahasiswa dan menampilkan rata-rata nilainya. Konsep ini membuat kode lebih terstruktur dan mudah diatur, terutama untuk proyek yang lebih besar.

### 2. Linked List
```
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode -> next = head;
    head = newNode;
    cout << "Data " << data << " berhasil di tambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
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
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
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
                updateNode(data, dataBaru);
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

Penjelasan Program :
Program di atas adalah implementasi Single Linked List dalam bahasa C++. . Struktur data ini terdiri dari node-node yang saling terhubung, di mana setiap node berisi data dan pointer yang menunjuk ke node berikutnya. Fungsi insertDepan dan insertBelakang digunakan untuk menambah node di awal dan di akhir list, sementara insertSetelah menyisipkan node di posisi tertentu. Untuk menghapus node, ada fungsi hapusNode yang mencari dan menghapus data yang diinginkan, dan updateNode digunakan untuk mengubah nilai data. Seluruh fungsi ini bekerja sama dengan tampilkanList yang bertugas menampilkan seluruh isi list, sehingga program ini menyediakan operasi dasar untuk mengelola data secara dinamis.

## Unguided

### Soal 1

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani
```
#include <iostream>
using namespace std;

struct pembeli {
    char nama[30];
    char pesanan[50];
    pembeli *next;
};

pembeli *antrianPertama = NULL;
pembeli *antrianTerakhir = NULL;

void tambahAntrian() {
    pembeli *baru = new pembeli;
    cout << "Masukkan nama pembeli  : ";
    cin >> baru->nama;
    cout << "Masukkan pesanan       : ";
    cin >> baru->pesanan;
    baru->next = NULL;

    if (antrianPertama == NULL) {
        antrianPertama = antrianTerakhir = baru;
    } else {
        antrianTerakhir->next = baru;
        antrianTerakhir = baru;
    }

    cout << "Pembeli " << baru->nama << " berhasil ditambahkan ke antrian.\n";
}

void layaniAntrian() {
    if (antrianPertama == NULL) {
        cout << "Antrian kosong, tidak ada yang dilayani.\n";
        return;
    }

    pembeli *hapus = antrianPertama;
    cout << "Melayani pembeli: " << hapus->nama << " (Pesanan: " << hapus->pesanan << ")\n";
    antrianPertama = antrianPertama->next;
    delete hapus;

    if (antrianPertama == NULL) {
        antrianTerakhir = NULL;
    }
}

void tampilkanAntrian() {
    if (antrianPertama == NULL) {
        cout << "Antrian kosong.\n";
        return;
    }

    pembeli *bantu = antrianPertama;
    int nomor = 1;

    cout << "\n=== DAFTAR ANTRIAN PEMBELI ===\n";
    while (bantu != NULL) {
        cout << nomor << ". Nama: " << bantu->nama << ", Pesanan: " << bantu->pesanan << endl;
        bantu = bantu->next;
        nomor++;
    }
    cout << "==============================\n";
}

int main() {
    int pilihan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                tambahAntrian();
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilkanAntrian();
                break;
            case 4:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 4);

    return 0;
}

```

> Output
> ![Screenshot bagian x](OUTPUT/TRANSPOSE2.PNG)

Program di atas untuk membuat sistem antrian pembeli menggunakan konsep single linked list. Program ini menyimpan data pembeli berupa nama dan pesanan, lalu menyediakan menu untuk menambah pembeli baru ke dalam antrian, melayani pembeli yang berada di urutan pertama, dan menampilkan seluruh daftar antrian yang sedang menunggu. Setiap kali pembeli baru ditambahkan, datanya akan ditempatkan di bagian akhir antrian, sedangkan pembeli yang dilayani adalah yang paling awal datang (sesuai prinsip FIFO atau First In First Out). Dengan cara ini, program dapat meniru proses antrian seperti di kasir atau tempat pelayanan pada umumnya.

### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 


```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

Node *head = NULL;

void tambahDepan(int data) {
    Node *baru = new Node;
    baru->data = data;
    baru->next = head;
    head = baru;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

void tambahBelakang(int data) {
    Node *baru = new Node;
    baru->data = data;
    baru->next = NULL;
    if (head == NULL) {
        head = baru;
    } else {
        Node *bantu = head;
        while (bantu->next != NULL) {
            bantu = bantu->next;
        }
        bantu->next = baru;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void tampilkanList() {
    if (head == NULL) {
        cout << "List kosong.\n";
        return;
    }
    Node *bantu = head;
    cout << "Isi Linked List: ";
    while (bantu != NULL) {
        cout << bantu->data << " -> ";
        bantu = bantu->next;
    }
    cout << "NULL\n";
}

void reverseList() {
    if (head == NULL) {
        cout << "List kosong, tidak bisa dibalik.\n";
        return;
    }
    Node *prev = NULL;
    Node *current = head;
    Node *next = NULL;
    while (current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    head = prev;
    cout << "Linked list berhasil dibalik.\n";
}

int main() {
    int pilihan, data;
    do {
        cout << "1. Tambah Depan\n";
        cout << "2. Tambah Belakang\n";
        cout << "3. Tampilkan List\n";
        cout << "4. Balik (Reverse) List\n";
        cout << "5. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                tambahDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                tambahBelakang(data);
                break;
            case 3:
                tampilkanList();
                break;
            case 4:
                reverseList();
                break;
            case 5:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 5);

    return 0;
}

```

> Output
> ![Screenshot bagian x](OUTPUT/CALLBYREF.PNG)

Program di atas untuk membuat dan memanipulasi data pada single linked list dengan beberapa fitur dasar. Program ini bisa menambahkan data di bagian depan atau belakang list, menampilkan seluruh isi list, serta membalik urutan data dalam list (reverse). Saat data dimasukkan ke depan, elemen baru menjadi head atau node pertama, sedangkan saat dimasukkan ke belakang, elemen ditambahkan di akhir list. Fitur tampil digunakan untuk menelusuri dan menampilkan semua data dari awal hingga akhir, sementara fitur reverse membalik arah hubungan antar node sehingga urutan datanya menjadi terbalik. Program ini berjalan menggunakan menu pilihan agar pengguna bisa mengatur data secara interaktif.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://osf.io/preprints/vyech/
3. https://repository.penerbitwidina.com/media/publications/557434-algoritma-dan-struktur-data-39398749.pdf
