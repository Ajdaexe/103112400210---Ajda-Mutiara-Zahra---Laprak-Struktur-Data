# <h1 align="center">Laporan Praktikum Modul 2 <br> Modul 2 Pengenalan Bahasa C++ (Bagian Dua) </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Array adalah kumpulan data dengan tipe yang sama yang disimpan dalam satu variabel, sehingga memudahkan pengolahan data yang jumlahnya banyak. Matriks adalah bentuk lanjutan dari array, di mana data disusun dalam baris dan kolom layaknya tabel, dan bisa dipakai untuk berbagai operasi matematika, misalnya transpose. Pointer adalah variabel khusus yang menyimpan alamat memori dari variabel lain, sehingga kita bisa mengakses atau mengubah data secara langsung lewat alamat tersebut. Sedangkan call by reference adalah cara agar sebuah variabel bisa diproses lewat alamatnya, sehingga perubahan yang dilakukan di dalam fungsi atau blok program akan langsung memengaruhi nilai variabel aslinya.

## Guided

### 1. Array
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

int main ()


{
    int matriks [3][3];
    int transpose [3][3];

    cout << "Input Matriks : " << endl;
    for (int i = 0; i < 3; i++)

    {
        for (int j = 0; j < 3; j++)
        {
            cout << "Elemen [" << i << "][" << j << "] :";
            cin >> matriks [i][j];
        }
    }

    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)

        {
            transpose [j][i] = matriks [i][j];
        }
    }

    cout << "\nMatriks Awal : " << endl;
    for (int i = 0; i < 3; i++)

    {
        for (int j = 0; j < 3; j++)
        {
            cout << matriks [i][j] << " ";
        }
        cout << endl;
    }
    cout << "\nMatriks Transpose : " << endl;
    for (int i = 0; i< 3; i++)
    {
        for (int j = 0; j <  3; j++) 
        {
            cout << transpose [i][j] << " ";
        }
        cout << endl;
    }

    return 0;

}
```

> Output
> ![Screenshot bagian x](OUTPUT/TRANSPOSE2.PNG)

Program di atas untuk menampilkan matriks awal dan hasil transpose. User menginput elemen matriks 3x3, lalu program membuat transpose dengan menukar baris jadi kolom. Setelah itu, program menampilkan matriks asli dan matriks hasil transpose.


### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 


```
#include <iostream>
using namespace std; 

int main ()
{
    int angka;
    cout << "Masukkan Angka : ";
    cin >> angka;

    cout << "Nilai Awal : " << angka << endl;

    int &ref = angka;
    ref = ref * ref;
    cout << "Nilai Setelah Di Kuadratkan : " << angka << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](OUTPUT/CALLBYREF.PNG)

Program di atas untuk mengkuadratkan angka dengan reference. Pertama user memasukkan angka, lalu ditampilkan nilainya. Reference `ref` menunjuk ke variabel `angka`, jadi saat `ref` dikalikan dengan dirinya sendiri, nilai `angka` ikut berubah. Terakhir program menampilkan hasil angka setelah dikuadratkan.


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://osf.io/preprints/vyech/
3. https://repository.penerbitwidina.com/media/publications/557434-algoritma-dan-struktur-data-39398749.pdf
