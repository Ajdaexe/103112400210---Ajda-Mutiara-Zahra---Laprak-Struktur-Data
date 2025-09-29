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
### 1. Operasi Aritmatika (aritmatika.cpp)
Program ini mendemonstrasikan penggunaan **operator aritmatika** di C++.  
Variabel `X`, `Y`, dan `W` digunakan untuk menyimpan angka. Hasil operasi `(X + Y) / (Y + W)` disimpan ke dalam variabel `Z`.

```cpp
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}

### soal 1

aku mengerjakan perulangan

## Unguided

### Soal 1

copy paste soal nomor 1 disini

```go
package main

func main() {
	fmt.Println("Kode kalian disini")
	fmt.Println("JANGAN MASUKIN >>SCREENSHOT<< KODE KALIAN DISINI")
	fmt.Println("KALAU ADA -20 POIN LAPRAK")
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
