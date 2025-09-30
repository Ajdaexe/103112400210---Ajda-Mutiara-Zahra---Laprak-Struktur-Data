# <h1 align="center">Laporan Praktikum Modul 1 <br> Modul 1 Code Block IDE & Pengenalan Bahasa C++ </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Bahasa C++ merupakan bahasa pemrograman yang mendukung paradigma prosedural dan berorientasi objek. Dalam praktikum ini, konsep dasar yang digunakan meliputi:

1. **Operator Aritmatika**  
   Digunakan untuk melakukan perhitungan matematis, misalnya penjumlahan (+), pengurangan (-), perkalian (*), dan pembagian (/).
   
2. **Fungsi dan Prosedur**  
   - Fungsi adalah blok kode yang mengembalikan nilai.  
   - Prosedur adalah blok kode yang tidak mengembalikan nilai, hanya menampilkan hasil.
     
3. **Kondisi (if, else, switch)**  
   Kondisi digunakan untuk mengambil keputusan dalam program. Contohnya `switch-case` untuk menentukan hari kerja/libur.

4. **Perulangan (for, while, do-while)**  
   Perulangan digunakan untuk menjalankan instruksi berulang kali. `do-while` menjamin perintah dijalankan minimal sekali.

5. **Struct**  
   `struct` digunakan untuk mengelompokkan variabel dengan tipe berbeda menjadi satu kesatuan, misalnya data mahasiswa.

6. **Input Karakter**  
   Program juga bisa menerima input berupa karakter dengan fungsi `getchar()`. 

## Guided

### 1. Aritmatika
Saya mengerjakan operasi aritmatika sederhana menggunakan operator `+`, `-`, `*`, dan `/`.

### 2. Fungsi dan Prosedur
Saya mengerjakan program yang menggunakan fungsi untuk menghitung luas dan keliling, serta prosedur untuk menampilkan hasil.

### 3. Kondisi
Saya mengerjakan program dengan kondisi `if` dan `switch` untuk menentukan hari kerja atau hari libur.

### 4. Perulangan
Saya mengerjakan perulangan menggunakan `do-while` untuk mencetak teks berulang kali.

### 5. Struct
Saya mengerjakan program dengan `struct` untuk menyimpan data mahasiswa (nama, NIM, IPK).

### 6. Input Karakter
Saya mengerjakan program untuk membaca input berupa karakter dengan `getchar()`.


## Unguided

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan betipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```
#include <iostream>
using namespace std; 

int main (){
    float a, b;
    cout << "Angka 1 : ";
    cin >> a;
    cout << "Angka 2 : ";
    cin >> b;

    // Operasi Dasar
    cout << "Penjumlahan : " << a + b << endl;
    cout << "Pengurangan : " << a - b << endl;
    cout << "Perkalian   : " << a * b << endl;
    cout << "Pembagian   : " << a / b << endl;

    // Or    
    cout << a << " + " << b << " = " << a + b << endl;
    cout << a << " - " << b << " = " << a - b << endl;
    cout << a << " x " << b << " = " << a * b << endl;
    cout << a << " : " << b << " = " << a / b << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](Modul 1 Codeblocks IDE & Pengenalan Bahasa C++/OUTPUT/OUTPUT1.png)

Kode di atas digunakan untuk menghitung penjumlahan, pengurangan, perkalian, dan pembagian dari dua angka yang dimasukkan pengguna. Input disimpan di variabel a dan b, lalu hasil operasi ditampilkan dengan format lengkap, misalnya 5 + 6 = 11.

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100

contoh:

79: tujuh puluh Sembilan


```
#include <iostream> 
using namespace std;

string satuan[] = {"nol","satu","dua","tiga","empat","lima","enam","tujuh","delapan","sembilan"};
string belasan[] = {"sepuluh","sebelas","dua belas","tiga belas","empat belas","lima belas","enam belas","tujuh belas","delapan belas","sembilan belas"};
string puluhan[] = {"","sepuluh","dua puluh","tiga puluh","empat puluh","lima puluh","enam puluh","tujuh puluh","delapan puluh","sembilan puluh"};

int main () {
    int n;
    cout << "Masukkan Angka dari 0 - 100 : ";
    cin >> n;

    cout << n << " = ";

    if ( n < 10 ) {
        cout << satuan[n];
    }
    else if (n < 20 ) {
        cout << belasan [n-10];
    }
    else if (n < 100) {
        int p = n / 10; 
        int s = n % 10; 
        cout << puluhan[p];
        if (s != 0) {
            cout << " " << satuan[s];
        }
    }
    else if (n == 100 ) {
        cout << "seyatus";
    }
    else {
        cout << " no no, WAJIB 0 sampai 100 aja yawwww ";
    }
    cout << endl;
    return 0;
}
```

> Output
> ![Screenshot bagian x](Modul 1 Codeblocks IDE & Pengenalan Bahasa C++/OUTPUT/OUTPUT 2.png)

Kode di atas digunakan untuk mengubah angka 0 sampai 100 menjadi tulisan. Program memakai array satuan, belasan, dan puluhan untuk menyimpan kata dasar angka. Hasilnya disesuaikan dengan kondisi input, misalnya 79 akan ditampilkan sebagai “tujuh puluh sembilan”.

### Soal 3

Buatlah program yang menerima input-an dua buah bilangan betipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```
#include <iostream>
using namespace std; 

int  main () {
    int n;
    cout << " Angka : ";
    cin >> n;

    for (int i = n; i >= 1; i--){

        for (int s = 0; s < n - i; s++){
            cout << " ";
        }
         //ngiri
        for (int j = i; j >= 1; j--) {
            cout << j;
        }

        cout << " * ";
        //nganan
        for (int j = 1; j <= i; j++){
            cout << j;
        } 
        cout << endl;
    }
}
```

> Output
> ![Screenshot bagian x](Modul 1 Codeblocks IDE & Pengenalan Bahasa C++/OUTPUT/OUTPUT 3.png)

Kode di atas digunakan untuk mencetak pola angka simetris dengan tanda * di tengah. Perulangan mengatur spasi, angka menurun di kiri, bintang di tengah, dan angka naik di kanan. Contohnya, jika n = 3, maka keluar pola Segitiga.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://osf.io/preprints/vyech/
3. https://repository.penerbitwidina.com/media/publications/557434-algoritma-dan-struktur-data-39398749.pdf


