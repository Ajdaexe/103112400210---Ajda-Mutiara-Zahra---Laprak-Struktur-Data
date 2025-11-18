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

Buatlah ADT Queue menggunakan ARRAY sebagai berikut di dalam file “queue.h”:
Type infotype: integer
Type Queue: <
info : array [5] of infotype {index array dalam C++
dimulai dari 0}
head, tail : integer
>
procedure CreateQueue (input/output Q: Queue)
function isEmptyQueue (Q: Queue) → boolean
function isFullQueue (Q: Queue) → boolean
procedure enqueue (input/output Q: Queue, input x: infotype)
function dequeue (input/output Q: Queue) → infotype
procedure printInfo (input Q: Queue)
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).
int main() {
cout << "Hello World" << endl;
Queue Q;
createQueue(Q);
cout<<"----------------------"<<endl;
cout<<" H - T \t | Queue info"<<endl;
cout<<"----------------------"<<endl;
printInfo(Q);
enqueue(Q,5); printInfo(Q);
enqueue(Q,2); printInfo(Q);
enqueue(Q,7); printInfo(Q);
dequeue(Q); printInfo(Q);
enqueue(Q,4); printInfo(Q);
dequeue(Q); printInfo(Q);
dequeue(Q); printInfo(Q);
return 0;

### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

queue.h
```
#ifndef QUEUE_H_INCLUDED
#define QUEUE_H_INCLUDED

#include <iostream>
using namespace std;

#define MAX 5
typedef int infotype;

struct Queue {
    infotype info[MAX];
    int head;
    int tail;
};

void CreateQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
void dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```

queue.cpp
```
#include "queue.h"

void CreateQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh! tidak bisa menambah data." << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0; 
        }
        Q.tail++; 
        Q.info[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

void dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue Kosong! tidak ada data yang di hapus." << endl;
    } else {
        infotype temp = Q.info[Q.head];
        cout << "Dequeue: " << temp << endl;

        if (Q.head == Q.tail) {
            CreateQueue(Q);
        } else {
            for (int i = Q.head; i < Q.tail; i++) {
                Q.info[i] = Q.info[i + 1];
            }
            Q.tail--;
        }
    }
}

//no 1
// void printInfo(Queue Q) {
//     if (isEmptyQueue(Q)) {
//         cout << "empty queue" << endl;
//     } else {
//         cout << "Queue info : ";
//         for (int i = Q.head; i <= Q.tail; i++) {
//             cout << Q.info[i] << " ";
//         }
//         cout << endl;
//     }
// }

//no 2
// void printInfo(Queue Q) {
//     if (isEmptyQueue(Q)) {
//         cout << ">> Antrian sekarang kosong." << endl;
//     } else {
//         cout << ">> Isi Antrian:  ";
//         for (int i = Q.head; i <= Q.tail; i++) {
//             cout << Q.info[i] << " ";
//         }
//         cout << endl;
//     }
// }

// no 3
void printInfo(Queue Q) { 
    if (isEmptyQueue(Q)) {
        cout << ">> Antrian sekarang kosong." << endl;
    } else {
        cout << ">> Isi Antrian:  ";
        int i = Q.head;
        while (true) {
            cout << Q.info[i] << " ";
            if (i == Q.tail) break;
            i = (i + 1) % MAX; 
        }
        cout << endl;
    }
}
```

main.cpp
#include <iostream>
#include "queue.h"

using namespace std;

int main() {
    Queue Q;
    CreateQueue(Q);

    cout << "[Keadaan Awal]" << endl;
    printInfo(Q);

    cout << "\n[Enqueue 5]" << endl;
    enqueue(Q, 5);
    printInfo(Q);

    cout << "\n[Enqueue 2]" << endl;
    enqueue(Q, 2);
    printInfo(Q);

    cout << "\n[Enqueue 7]" << endl;
    enqueue(Q, 7);
    printInfo(Q);

    cout << "\n[Dequeue]" << endl;
    dequeue(Q);
    printInfo(Q);

    cout << "\n[Enqueue 4]" << endl;
    enqueue(Q, 4);
    printInfo(Q);

    cout << "\n[Dequeue]" << endl;
    dequeue(Q);
    printInfo(Q);

    cout << "\n[Dequeue]" << endl;
    dequeue(Q);
    printInfo(Q);

    return 0;
} 
```
> Output
> ![Screenshot bagian 1](OUTPUT/output.png)
> ![Screenshot bagian 2](OUTPUT/output.png)
> ![Screenshot bagian 3](OUTPUT/output.png)

Soal 1 Program di atas menggunakan metode penampilan data berdasarkan pendekatan queue Alternatif 1, yaitu head berada di posisi tetap dan hanya tail yang bergerak setiap kali elemen ditambahkan. Ketika elemen dihapus, data digeser ke kiri (shifting) agar elemen tetap berurutan mulai dari indeks awal.

Soal 2 Program di atas mewakili pendekatan queue Alternatif 2, yaitu baik head maupun tail dapat bergerak maju sesuai operasi yang dilakukan. Pada metode ini, saat terjadi dequeue, head tidak lagi direset menjadi 0 atau dilakukan shifting, melainkan cukup digeser satu langkah ke indeks berikutnya.

Soal 3 Program di atas menggunakan pendekatan circular queue, di mana head dan tail bergerak secara melingkar menggunakan operasi (i + 1) % MAX

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://journal.stiestekom.ac.id/index.php/TEKNIK/article/view/976
3. https://jurnal.kdi.or.id/index.php/bt/article/view/1867
