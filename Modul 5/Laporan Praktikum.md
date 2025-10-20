# <h1 align="center">Laporan Praktikum Modul 5 <br> Modul 5 Singly Linked List </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
linked list merupakan salah satu struktur data dinamis yang menggunakan pointer untuk menghubungkan elemen-elemen (node) secara berurutan. Setiap node terdiri dari dua bagian, yaitu data (info) dan penunjuk ke node berikutnya (next). Operasi dasar yang dapat dilakukan pada singly linked list meliputi pembuatan list kosong, penambahan elemen di awal, tengah, atau akhir, penghapusan elemen, serta pencarian data tertentu melalui proses searching yang dilakukan dengan menelusuri setiap node hingga data yang dicari ditemukan. Proses ini juga mendukung penerapan operasi lain seperti insert after, delete after, dan update dengan lebih mudah. Selain itu, manajemen memori dilakukan secara manual menggunakan fungsi alokasi dan dealokasi agar ruang penyimpanan digunakan secara efisien. Implementasi konsep ini biasanya dibagi dalam dua file utama, yaitu file header (.h) yang berisi deklarasi struktur dan prototipe fungsi, serta file implementasi (.cpp) yang berisi kode program pelaksanaannya

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

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya  \*antrian pertama harus yang pertama dilayani
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

bool sama(char a[], char b[]) {
    int i = 0;
    while (a[i] != '\0' && b[i] != '\0') {
        if (a[i] != b[i]) {
            return false;
        }
        i++;
    }
    return a[i] == b[i]; // kalau dua-duanya udah habis berarti sama
}

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

void cariPembeli() {
    if (antrianPertama == NULL) {
        cout << "Antrian kosong, tidak ada data untuk dicari.\n";
        return;
    }

    int pilihan;
    char cari[50];
    bool ditemukan = false;

    cout << "\n=== PENCARIAN PEMBELI ===\n";
    cout << "Cari berdasarkan:\n";
    cout << "1. Nama Pembeli\n";
    cout << "2. Pesanan\n";
    cout << "Pilih: ";
    cin >> pilihan;

    if (pilihan == 1) {
        cout << "Masukkan nama yang dicari: ";
        cin >> cari;

        pembeli *bantu = antrianPertama;
        int posisi = 1;

        while (bantu != NULL) {
            if (sama(bantu->nama, cari)) {
                cout << "Ditemukan di posisi " << posisi << ":\n";
                cout << "Nama: " << bantu->nama << ", Pesanan: " << bantu->pesanan << endl;
                ditemukan = true;
            }
            bantu = bantu->next;
            posisi++;
        }

    } else if (pilihan == 2) {
        cout << "Masukkan pesanan yang dicari: ";
        cin >> cari;

        pembeli *bantu = antrianPertama;
        int posisi = 1;

        while (bantu != NULL) {
            if (sama(bantu->pesanan, cari)) {
                cout << "Ditemukan di posisi " << posisi << ":\n";
                cout << "Nama: " << bantu->nama << ", Pesanan: " << bantu->pesanan << endl;
                ditemukan = true;
            }
            bantu = bantu->next;
            posisi++;
        }

    } else {
        cout << "Pilihan tidak valid.\n";
        return;
    }

    if (!ditemukan) {
        cout << "Data tidak ditemukan dalam antrian.\n";
    }
}

int main() {
    int pilihan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Cari Pembeli\n";
        cout << "5. Keluar\n";
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
                cariPembeli();
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
> ![Screenshot bagian x](OUTPUT/OUPUT1.png)

Program di atas merupakan sistem antrian pembeli yang dibuat menggunakan konsep single linked list. Program ini memiliki beberapa fungsi utama, yaitu tambahAntrian() untuk menambah data pembeli baru ke bagian akhir antrian, layaniAntrian() untuk melayani dan menghapus pembeli yang berada di urutan pertama, tampilkanAntrian() untuk menampilkan seluruh data pembeli yang sedang mengantri, serta cariPembeli() untuk mencari pembeli berdasarkan nama atau pesanan dengan bantuan fungsi pembanding sama(). Semua fungsi tersebut dijalankan melalui menu utama di dalam main(), sehingga pengguna dapat dengan mudah menambah, mencari, melayani, dan melihat daftar antrian pembeli sesuai prinsip FIFO (First In First Out).

### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN


```
//single link listed data buku, menyimpan
// (ISBN, JUDUL, PENULIS)
//1. FUNGSI TAMBAH BUKU(BUKU BARU BERAdA SETELAH BUKU LAMA) .
//2. FUNGSI UNTUK MENGHAPUS BERDASAR ISBN .
//3. FUNGSI MEMPERBARUI BUKU 
//4. FUNGSI MELIHAT BUKU
//+ laprak + searching

#include <iostream>
using namespace std;

struct buku {
    int ISBN;
    char Judul[30];
    char Penulis[30];
    buku *next;
};

buku *head = NULL;
buku *tail = NULL;

bool sama(char a[], char b[]) {
    int i = 0;
    while (a[i] != '\0' && b[i] != '\0'){
    if (a[i] != b[i]){
        return false;
    }
    i ++;
  }
  return a[i] == b[i];
}

void tambahBuku(){
    buku *baru = new buku;
    cout << "Masukkan Nomor ISBN :";
    cin >> baru->ISBN;
    cout << "Masukkan Judul Buku : ";
    cin >> baru->Judul;
    cout << "Masukkan Nama Penulis : ";
    cin >> baru->Penulis;
    baru->next = NULL;
    
    if (head == NULL){
        head = tail = baru;
    } else {
        tail->next = baru;
        tail = baru;
    }

    cout << "Buku Baru " << baru->ISBN << " berhasil ditambahkan.\n"; 

} 

void hapusISBN() {
    if (head == NULL) {
        cout << "Tidak Ada Buku.\n";
        return;
    }

    int targetISBN;
    cout << "Masukkan ISBN yang ingin dihapus: ";
    cin >> targetISBN;
    buku *hapus = head;
    buku *sebelum = NULL;

   while (hapus != NULL && hapus->ISBN != targetISBN) {
        sebelum = hapus;
        hapus = hapus->next;
    }

    if (hapus == NULL) {
        cout << "Buku dengan ISBN " << targetISBN << " tidak ditemukan.\n";
        return;
    }

    if (hapus == head) {
        head = head->next;
    } else {
        sebelum->next = hapus->next;
    }

    if (hapus == tail) {
        tail = sebelum;
    }

    cout << "Buku dengan ISBN " << targetISBN << " berhasil dihapus.\n";
    delete hapus;

}

void perbaruiBuku() {
    if (head == NULL) {
        cout << "Tidak ada buku untuk diperbarui.\n";
        return;
    }

    int cariISBN;
    cout << "Masukkan ISBN buku yang ingin diperbarui: ";
    cin >> cariISBN;

    buku *bantu = head;
    while (bantu != NULL && bantu->ISBN != cariISBN) {
        bantu = bantu->next;
    }

    if (bantu == NULL) {
        cout << "Buku dengan ISBN " << cariISBN << " tidak ditemukan.\n";
        return;
    }

    cout << "Masukkan judul baru: ";
    cin >> bantu->Judul;
    cout << "Masukkan penulis baru: ";
    cin >> bantu->Penulis;

    cout << "Data buku berhasil diperbarui!\n";
}

void lihatBuku() {
    if (head == NULL) {
        cout << "Tidak ada buku yang tersimpan.\n";
        return;
    }

    buku *bantu = head;
    int nomor = 1;
    cout << "\n=== DAFTAR BUKU ===\n";
    while (bantu != NULL) {
        cout << nomor << ". ISBN: " << bantu->ISBN
             << ", Judul: " << bantu->Judul
             << ", Penulis: " << bantu->Penulis << endl;
        bantu = bantu->next;
        nomor++;
    }
    cout << "===================\n";
}

void cariBuku() {
    if (head == NULL) {
        cout << "Tidak ada data buku.\n";
        return;
    }

    int pilihan;
    cout << "\n=== PENCARIAN BUKU ===\n";
    cout << "Cari berdasarkan:\n";
    cout << "1. ISBN\n";
    cout << "2. Judul Buku\n";
    cout << "Pilih: ";
    cin >> pilihan;

    if (pilihan == 1) {
        int cariISBN;
        cout << "Masukkan ISBN yang dicari: ";
        cin >> cariISBN;

        buku *bantu = head;
        bool ditemukan = false;

        while (bantu != NULL) {
            if (bantu->ISBN == cariISBN) {
                cout << "Buku ditemukan!\n";
                cout << "ISBN: " << bantu->ISBN
                     << ", Judul: " << bantu->Judul
                     << ", Penulis: " << bantu->Penulis << endl;
                ditemukan = true;
            }
            bantu = bantu->next;
        }

        if (!ditemukan) {
            cout << "Buku dengan ISBN tersebut tidak ditemukan.\n";
        }

    } else if (pilihan == 2) {
        char cariJudul[30];
        cout << "Masukkan Judul Buku yang dicari: ";
        cin >> cariJudul;

        buku *bantu = head;
        bool ditemukan = false;

        while (bantu != NULL) {
            if (sama(bantu->Judul, cariJudul)) {
                cout << "Buku ditemukan!\n";
                cout << "ISBN: " << bantu->ISBN
                     << ", Judul: " << bantu->Judul
                     << ", Penulis: " << bantu->Penulis << endl;
                ditemukan = true;
            }
            bantu = bantu->next;
        }

        if (!ditemukan) {
            cout << "Buku dengan judul tersebut tidak ditemukan.\n";
        }

    } else {
        cout << "Pilihan tidak valid.\n";
    }
}

int main() {
    int pilihan;
    do {
        cout << "\n=== MENU DATA BUKU ===\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku (berdasar ISBN)\n";
        cout << "3. Perbarui Buku\n";
        cout << "4. Lihat Buku\n";
        cout << "5. Cari Buku\n";
        cout << "6. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                tambahBuku();
                break;
            case 2:
                hapusISBN();
                break;
            case 3:
                perbaruiBuku();
                break;
            case 4:
                lihatBuku();
                break;
            case 5:
                cariBuku();
                break;
            case 6:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 6);

    return 0;
}


```

> Output
> ![Screenshot bagian x](OUTPUT/OUPUT2.png)

Program di atas merupakan sistem pengelolaan data buku yang menggunakan konsep single linked list, di mana setiap node menyimpan informasi buku berupa ISBN, Judul, dan Penulis. Program ini memiliki beberapa fungsi utama. Fungsi tambahBuku() digunakan untuk menambahkan data buku baru ke bagian akhir daftar. Fungsi hapusISBN() berfungsi untuk menghapus data buku berdasarkan nomor ISBN yang dimasukkan pengguna. Fungsi perbaruiBuku() digunakan untuk memperbarui data buku (judul dan penulis) berdasarkan ISBN tertentu. Fungsi lihatBuku() menampilkan seluruh daftar buku yang tersimpan dalam linked list secara berurutan. Kemudian, fungsi cariBuku() berfungsi untuk mencari buku berdasarkan ISBN atau judul dengan bantuan fungsi sama() yang membandingkan dua string karakter satu per satu. Semua fitur ini dijalankan melalui menu utama di dalam fungsi main(), sehingga pengguna dapat menambah, menghapus, memperbarui, menampilkan, dan mencari buku dengan mudah.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://jurnalmahasiswa.com/index.php/jriin/article/view/1060/678
3. https://jurnalmahasiswa.com/index.php/jriin/article/view/957/756

