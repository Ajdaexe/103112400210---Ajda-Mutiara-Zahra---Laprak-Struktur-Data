# <h1 align="center">Laporan Praktikum Modul 1 <br> Modul 1 Code Block IDE & Pengenalan Bahasa C++ </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Bahasa C++ merupakan bahasa pemrograman yang mendukung paradigma prosedural dan berorientasi objek. Dalam praktikum ini, konsep dasar yang digunakan meliputi:

1. **Operator Aritmatika**  
   Digunakan untuk melakukan perhitungan matematis, misalnya penjumlahan (+), pengurangan (-), perkalian (*), dan pembagian (/).
   
3. **Fungsi dan Prosedur**  
   - *Fungsi* adalah blok kode yang mengembalikan nilai.  
   - *Prosedur* adalah blok kode yang tidak mengembalikan nilai, hanya menampilkan hasil.
   - 
4. **Kondisi (if, else, switch)**  
   Kondisi digunakan untuk mengambil keputusan dalam program. Contohnya `switch-case` untuk menentukan hari kerja/libur.

5. **Perulangan (for, while, do-while)**  
   Perulangan digunakan untuk menjalankan instruksi berulang kali. `do-while` menjamin perintah dijalankan minimal sekali.

6. **Struct**  
   `struct` digunakan untuk mengelompokkan variabel dengan tipe berbeda menjadi satu kesatuan, misalnya data mahasiswa.

7. **Input Karakter**  
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

```#include <iostream>
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
> ![Screenshot bagian x](output/screenshot_soal1.png)
> %% Untuk mencantumkan screenshot, tidak boleh ada spasi di urlnya `()`, penamaan file bebas asal gak sara dan mudah dipahami aja,, dan jangan lupa hapus komen ini yah%%

Penjelasan ttg kode kalian disini

### Soal 2

soal nomor 2A

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

penjelasan kode

Kalau adalanjutan di lanjut disini aja

soal nomor 2B

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

