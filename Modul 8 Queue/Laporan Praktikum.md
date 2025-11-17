# <h1 align="center">Laporan Praktikum Modul 8 <br> Modul 8 Queue </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Queue merupakan salah satu struktur data linear yang bekerja berdasarkan prinsip FIFO (First In First Out), di mana elemen yang pertama kali masuk akan menjadi elemen pertama yang keluar. Konsep ini mirip dengan antrean di dunia nyata, seperti antrean pembelian tiket, di mana orang yang datang lebih awal akan dilayani lebih dulu. Queue dapat diimplementasikan menggunakan array maupun linked list, dengan dua operasi utama yaitu enqueue untuk menambahkan elemen di bagian belakang (tail) dan dequeue untuk menghapus elemen di bagian depan (head). Selain itu, terdapat operasi pendukung seperti isEmpty() untuk memeriksa apakah queue kosong, isFull() untuk memeriksa penuh tidaknya kapasitas, dan printQueue() untuk menampilkan isi antrian. Struktur data queue banyak digunakan dalam berbagai kasus pemrograman seperti penjadwalan proses, manajemen buffer, dan sistem antrian data.

## Guided

### 1. Queue
```
#include <iostream>
using namespace std;

#define MAX 5

struct Queue {
    int data [MAX];
    int head;
    int tail;
};

void createQueue (Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q){
    return (Q.tail == MAX - 1);
}

void printQueue (Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue Kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x){
    if (isFull(Q)){
        cout << " Queue penuh! tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueu: "<< x << endl;
    }
}

void dequeue (Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue Kosong! tidak ada data yang di hapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head]<< endl;
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            for (int i = Q.head; i < Q.tail; i++){
                Q.data[i] = Q.data[i+1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    createQueue;

    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;

}
```

Penjelasan Program :
Program di atas adalah implementasi struktur data queue menggunakan array dengan kapasitas maksimal 5 elemen. Queue diatur dengan dua indeks, yaitu head dan tail, yang menandakan posisi data terdepan dan data terakhir. Program menyediakan fungsi enqueue untuk menambah data ke belakang queue dan dequeue untuk menghapus data dari depan queue sesuai prinsip FIFO. Selain itu, ada fungsi isEmpty untuk mengecek apakah queue kosong, isFull untuk mengecek apakah queue penuh, dan printQueue untuk menampilkan isi queue.


## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h”:

Type infotype : integer
Type Stack <
info : array [20] of integer
top : integer
>
procedure CreateStack( input/output S : Stack )
procedure push(input/output S : Stack,
input x : infotype)
function pop(input/output t S : Stack )
→ infotype
procedure printInfo( input S : Stack )
procedure balikStack(input/output S :
Stack )

Program 2 Stack.h

Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp”
int main()
{
cout << "Hello world!" <<
endl;
Stack S;
createStack(S);
Push(S,3);
Push(S,4);
Push(S,8);
pop(S)
Push(S,2);
Push(S,3);
pop(S);
Push(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}

### Soal 2
Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)
int main()
{

Gambar 7-11 Output stack

STRUKTUR DATA 65

cout << "Hello world!" << endl;
Stack S;
createStack(S);
pushAscending(S,3);
pushAscending(S,4);
pushAscending(S,8);
pushAscending(S,2);
pushAscending(S,3);
pushAscending(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}

### Soal 3
Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan
menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan
tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.
int main()
{
cout << "Hello world!" << endl;
Stack S;
createStack(S);
getInputStream(S);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}

stack.h
```
#ifndef STACK_H_INCLUDED
#define STACK_H_INCLUDED

#include <iostream>
using namespace std;

const int MAX_SIZE = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX_SIZE + 1];
    int top;
};

void CreateStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

bool isEmpty(Stack S);
bool isFull(Stack S);

void pushAscending(Stack &S, infotype x);

void getInputStream(Stack &S);

#endif
```

stack.cpp
```
#include "stack.h"

void CreateStack(Stack &S) {
    S.top = 0;
}

bool isEmpty(Stack S) {
    return S.top == 0;
}

bool isFull(Stack S) {
    return S.top == MAX_SIZE;
}

void push(Stack &S, infotype x) {
    if (!isFull(S)) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh." << endl;
    }
}

infotype pop(Stack &S) {
    if (!isEmpty(S)) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 1; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp1, temp2;
    CreateStack(temp1);
    CreateStack(temp2);

    while (!isEmpty(S)) {
        push(temp1, pop(S));
    }
    while (!isEmpty(temp1)) {
        push(temp2, pop(temp1));
    }
    while (!isEmpty(temp2)) {
        push(S, pop(temp2));
    }
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    CreateStack(temp);

    while (!isEmpty(S) && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (!isEmpty(temp)) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    char c;
    c = cin.get();

    while (c != '\n') {
        int x = c - '0';
        push(S, x);
        c = cin.get();
    }
}
```
main1.cpp
```
#include <iostream>
#include "stack.h"

using namespace std;

int main() {
    cout << "Hello world!" << endl;
    Stack S;

    // --- Soal 1 ---
    cout << "\n--- Soal 1 ---" << endl;
    CreateStack(S);
    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    // --- Soal 2 ---
    cout << "\n--- Soal 2 ---" << endl;
    CreateStack(S);
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    // --- Soal 3 ---
    cout << "\n--- Soal Latihan 3 ---" << endl;
    CreateStack(S);
    cout << "Masukkan angka (diakhiri Enter): ";
    getInputStream(S);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```
> Output
> ![Screenshot bagian x](OUTPUT/output.png)

Program pada Soal 1 menampilkan proses dasar penggunaan stack dengan operasi push, pop, printInfo, dan balikStack. Data dimasukkan dan dihapus sesuai prinsip LIFO (Last In First Out), di mana elemen terakhir yang masuk akan menjadi yang pertama keluar. Setelah semua operasi dilakukan, fungsi balikStack membalik urutan elemen di dalam stack sehingga hasil akhirnya menampilkan isi stack yang urutannya terbalik dari kondisi semula.

Program pada Soal 2 menambahkan prosedur pushAscending, yaitu fungsi untuk menyisipkan elemen baru agar isi stack tetap terurut secara menurun (descending). Setiap kali data baru dimasukkan, program akan memindahkan sementara elemen yang lebih besar agar data baru ditempatkan di posisi yang benar. Hasil akhirnya menunjukkan urutan stack [TOP] 9 8 4 3 3 2, yang menandakan bahwa fungsi ini berjalan dengan benar menjaga keterurutan data dalam stack.

Program pada Soal 3 memperkenalkan prosedur getInputStream, yang memungkinkan pengguna mengetik data secara langsung. Setiap karakter yang dimasukkan akan dikonversi menjadi angka dan dimasukkan ke dalam stack satu per satu sampai pengguna menekan Enter. Misalnya, jika pengguna mengetik “4729601”, maka hasilnya menjadi [TOP] 1 0 6 9 2 7 4. Setelah fungsi balikStack dijalankan, urutannya menjadi kebalikan dari input, sesuai prinsip LIFO pada stack.


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://journal.stiestekom.ac.id/index.php/TEKNIK/article/view/976
3. https://jurnal.kdi.or.id/index.php/bt/article/view/1867
