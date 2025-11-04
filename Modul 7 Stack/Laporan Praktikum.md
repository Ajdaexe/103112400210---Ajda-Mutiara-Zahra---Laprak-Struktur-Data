# <h1 align="center">Laporan Praktikum Modul 7 <br> Modul 7 Stack </h1>
<p align="center">Ajda Mutiara Zahra - 103112400210</p>

## Dasar Teori
Stack merupakan salah satu bentuk struktur data dinamis yang menggunakan prinsip LIFO (Last In First Out), artinya data yang terakhir dimasukkan akan menjadi data yang pertama dikeluarkan. Struktur stack bekerja seperti tumpukan benda di mana elemen yang paling atas adalah yang pertama bisa diambil. Dalam implementasinya, stack dapat direpresentasikan dengan pointer (linked list) maupun tabel (array). Komponen utama stack adalah TOP, yaitu penunjuk ke elemen paling atas yang menjadi satu-satunya titik akses untuk melakukan operasi. Dua operasi dasar pada stack adalah push dan pop. Operasi push digunakan untuk menambah elemen baru ke bagian atas stack, sedangkan pop digunakan untuk menghapus elemen teratas dari stack. Selain itu, terdapat juga fungsi tambahan seperti isEmpty() untuk memeriksa apakah stack kosong, createStack() untuk membuat stack baru, serta fungsi pencarian atau tampilan isi stack. Representasi stack dengan pointer bersifat dinamis karena memanfaatkan alokasi memori saat program berjalan, sedangkan representasi tabel bersifat statis dengan ukuran tertentu yang sudah ditentukan sebelumnya. Konsep stack ini banyak digunakan dalam pemrograman, seperti dalam proses pemanggilan fungsi (function call), pengelolaan memori, serta proses undo-redo pada aplikasi komputer.

## Guided

### 1. Double Linked List
```
//pop hapus data
//top hrus di depan antara stack
//newnode -> next = akses var, node baru selaku jadi top
//pakai library stack gpp
//fungsi size, buuat ukuran stack

#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;

}

void push(Node *&top, int data)
{
    Node *newNode = new Node();
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop (Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    Node *temp = top;
    top = top -> next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
    {
        cout << "Stack Kosong." << endl;
        return;
    }

    cout << "TOP ->";
    Node *temp = top;

    while (temp != nullptr) 
    {
        cout << temp -> data << "->";
        temp = temp -> next;
    }

    cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan Isi Stack" << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: "<< endl;
    show(stack);

    return 0;
}
```

Penjelasan Program :
Program di atas untuk membuat dan mengelola struktur data stack menggunakan pointer dan linked list di C++. Stack bekerja dengan prinsip LIFO (Last In, First Out), di mana data yang terakhir masuk akan keluar lebih dulu. Fungsi isEmpty() dipakai untuk mengecek apakah stack kosong, push() untuk menambah data baru di bagian atas stack, pop() untuk menghapus data teratas dan mengembalikannya, sedangkan show() digunakan untuk menampilkan semua isi stack dari atas ke bawah. Di fungsi main(), program membuat stack kosong, lalu menambahkan data 10, 20, dan 30 ke dalamnya, menampilkan hasilnya, menghapus satu data paling atas dengan pop(), dan akhirnya menampilkan sisa isi stack setelah penghapusan tersebut.


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

Program di atas untuk Latihan 1 adalah implementasi dasar dari struktur data Stack menggunakan representasi tabel (array). Kode ini berfokus pada pembuatan fungsi-fungsi fundamental yang diperlukan untuk sebuah stack, seperti CreateStack untuk inisialisasi tumpukan kosong (di mana Top = 0 ), push untuk menambahkan elemen baru ke tumpukan (dengan Top = Top + 1 ), dan pop untuk mengambil elemen teratas (dengan TOP = TOP - 1 ).


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
2. https://jurnal.stkippersada.ac.id/jurnal/index.php/jutech/article/view/4263
3. https://www.irjet.net/archives/V5/i3/IRJET-V5I3434.pdf
