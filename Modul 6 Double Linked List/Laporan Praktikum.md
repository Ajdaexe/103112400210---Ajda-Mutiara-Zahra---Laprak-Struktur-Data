# <h1 align="center">Laporan Praktikum Modul 6 <br> Modul 6 Double Linked List </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Double linked list merupakan salah satu bentuk struktur data dinamis yang menggunakan dua pointer untuk menghubungkan setiap elemen (node) dalam dua arah, yaitu ke depan (next) dan ke belakang (prev). Setiap node pada doubly linked list terdiri dari tiga bagian utama, yaitu data (info), penunjuk ke node berikutnya, dan penunjuk ke node sebelumnya. Struktur ini menggunakan dua pointer utama — first (atau head) untuk menunjuk elemen pertama dan last (atau tail) untuk menunjuk elemen terakhir pada list. Operasi dasar yang dapat dilakukan meliputi penambahan elemen di awal, akhir, atau setelah elemen tertentu (insert), penghapusan elemen di berbagai posisi (delete), pembaruan data (update), serta penelusuran data dari depan maupun belakang (traversal). Kelebihan doubly linked list dibandingkan singly linked list adalah kemampuannya bergerak dua arah, sehingga mempermudah proses penghapusan atau penyisipan di tengah list tanpa perlu menelusuri dari awal.
## Guided

### 1. Double Linked List
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
> ![Screenshot bagian x](OUTPUT/OUTPUT1.png)

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
> ![Screenshot bagian x](OUTPUT/OUTPUT2.png)

Program di atas merupakan sistem pengelolaan data buku yang menggunakan konsep single linked list, di mana setiap node menyimpan informasi buku berupa ISBN, Judul, dan Penulis. Program ini memiliki beberapa fungsi utama. Fungsi tambahBuku() digunakan untuk menambahkan data buku baru ke bagian akhir daftar. Fungsi hapusISBN() berfungsi untuk menghapus data buku berdasarkan nomor ISBN yang dimasukkan pengguna. Fungsi perbaruiBuku() digunakan untuk memperbarui data buku (judul dan penulis) berdasarkan ISBN tertentu. Fungsi lihatBuku() menampilkan seluruh daftar buku yang tersimpan dalam linked list secara berurutan. Kemudian, fungsi cariBuku() berfungsi untuk mencari buku berdasarkan ISBN atau judul dengan bantuan fungsi sama() yang membandingkan dua string karakter satu per satu. Semua fitur ini dijalankan melalui menu utama di dalam fungsi main(), sehingga pengguna dapat menambah, menghapus, memperbarui, menampilkan, dan mencari buku dengan mudah.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://rtheunissen.github.io/bst/docs/references/2013_drozdek_delete.pdf
3. https://www.wscubetech.com/resources/dsa/doubly-linked-list-data-structure

