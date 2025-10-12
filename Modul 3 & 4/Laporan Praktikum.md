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
Program di atas untuk menyimpan lima angka dalam sebuah array dan kemudian menampilkannya satu per satu. Isi array adalah angka 1 sampai 5, dan melalui perulangan for, setiap elemen ditampilkan sesuai dengan indeksnya sehingga pengguna bisa melihat posisi serta nilai dari masing-masing elemen.

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

### 3. Pointer
```
#include <iostream>
using namespace std;

int main(){
    int umur = 25;
    int *p_umur;

    p_umur = &umur;

    cout << "nilai 'umur' : " << umur << endl;
    cout << "Alamat Memori 'umur' : " << umur << endl;
    cout << "nilai  'umur' : " << umur << endl;
    cout << "nilai 'umur' : " << umur << endl;
    cout << "nilai 'umur' : " << umur << endl;
}
```

Penjelasan Program :
Program di atas untuk menunjukkan cara penggunaan pointer dalam C++. Variabel umur diberikan nilai 25, lalu dibuat pointer yang menunjuk ke alamat memori variabel tersebut. Seharusnya, program bisa menampilkan nilai dan alamat memori, tetapi dalam kode ini yang tercetak masih berupa nilai variabel saja.

### 4. Array Pointer

```
#include <iostream>
using namespace std;

int main()
{
    int data[5] = {10, 20, 30, 40, 50};
    int *p_data = data;

    cout << "Mengakses elemen array cara normal:" << endl;
    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << data[i] << endl;
    }

    cout << "Mengakses elemen array menggunakan pointer:" << endl;
    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << *(p_data + i) << endl;
    }

    return 0;
}

```

Penjelasan Program :
Program di atas untuk menjelaskan dua cara mengakses elemen sebuah array, yaitu secara langsung dengan indeks dan melalui pointer. Dengan menggunakan indeks, elemen ditampilkan menggunakan data[i], sedangkan dengan pointer elemen diakses dengan operasi *(p_data + i). Keduanya menghasilkan tampilan nilai array yang sama.

### 5. String
```
#include <iostream>
using namespace std;

int main() {
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array: " << pesan_array << endl;
    cout << "String Pointer: " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}
```

Penjelasan Program :
Program di atas untuk memperlihatkan perbedaan antara string yang disimpan dalam array karakter dan string yang disimpan menggunakan pointer. String dalam array karakter dapat diubah isinya, misalnya huruf pertama diganti, sedangkan string pointer tidak dapat diubah isinya secara langsung, tetapi bisa diarahkan ke string lain.

### 6. Fungsi
```
#include <iostream>
using namespace std;

int tambah(int a, int b)
{
    return a + b;
}

void tampilkanHasil(int a, int b, int hasil)
{
    cout << "Hasil penjumlahan " << a << " + " << b << " adalah: " << hasil << endl;
}

int main()
{
    int angka1 = 10;
    int angka2 = 5;

    int hasilJumlah = tambah(angka1, angka2);

    tampilkanHasil(angka1, angka2, hasilJumlah);

    return 0;
}
```


Penjelasan Program :
Program di atas untuk melakukan penjumlahan dua bilangan dengan bantuan fungsi. Fungsi tambah digunakan untuk menghitung hasil penjumlahan, sementara fungsi tampilkanHasil bertugas menampilkan hasilnya. Dengan begitu, di fungsi utama angka 10 dan 5 dijumlahkan, lalu hasil penjumlahan tersebut ditulis ke layar.

### 7. Call By Pointer
```
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```


Penjelasan Program :
Program di atas untuk menukar nilai dua variabel dengan metode call by pointer. Variabel a bernilai 10 dan b bernilai 20, kemudian alamat keduanya dikirim ke fungsi tukar. Di dalam fungsi itu nilainya dipertukarkan, sehingga setelah proses selesai nilai a menjadi 20 dan b menjadi 10.

### 8. Call By Reference
```
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```


Penjelasan Program :
Program di atas untuk menukar nilai dua variabel dengan metode call by reference. Pada cara ini, parameter fungsi langsung berupa referensi variabel, sehingga proses penukaran menjadi lebih sederhana. Hasil akhirnya sama, nilai a dan b berhasil ditukar setelah fungsi dijalankan.


## Unguided

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:
1 2 3
4 5 6
7 8 9

Matriks Hasil Transpose:
1 4 7
2 5 8
3 6 9


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

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25


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
