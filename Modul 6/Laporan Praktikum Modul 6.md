# <h1 align="center">Laporan Praktikum Modul Struct dan Implementasi</h1>
<p align="center">Rizal Wahyu Pratama</p>
<p align="center">2311110029</p>
<p align="center">S1SD-04-B</p>

## Tujuan Praktikum

1.	Mahasiswa memahami perbedaan konsep Single, Double, Circular dan Non Linked List. 
2.	Mahasiswa mampu menerapkan SingleSingle, Double, Circular dan Non Linked List ke dalam pemrograman.

## Dasar Teori

List adalah sekumpulan data sejenis yang berada dalam lokasi yang fleksibel 
(dapat berubah sesuai dengan kebutuhan) [1]. List dapat dibagi menjadi dua yaitu single linked list dan Double Linked List. 

a. Single Linked List
Single linked list merupukan struktur data yang terdiri dari sejumlah node yang dihubungkan melalui pointer. Single linked list memiliki dua komponen utama di dalamnya yaitu Data dan Pointer yang menuju ke node berikutnya. 

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/SingleLinkedList.png" alt="Alt Text">
</p>

- Node pertama (head) menunjuk pada node yang pertama yang disebut dengan head.
- Node terakhir memiliki pointer yang menunjuk ke NULL yang merupakan akhir dari linked list.
- Penambahan Node, pada single linked list seseorang dapat menambahkan node baru dimanapun.
- Penghapusan Node, pada single linked list seseorang dapat menghapus node yang ada.
- Pencarian Node, dapat mencari node berdasarkan KEY tertentu.
- Iterasi atau perulangan, semua node dapat diakses dengan iterator.

  Linked List Circular
  Linked List Circular tidak memiliki nilai akhir, hal ini dikarenakan pada list di node terakhir tidak bernilai NULL, namun node terakhir terhubung dengan node pertama (head). Linked List Circular biasanya digunakan untuk menyimpan data yang dapat diakses dengan berulang-ulang sehingga memudahkan penggunanya.

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/Circular.png" alt="Alt Text">
</p> 

b. Double Linked List
Double Linked List merupakan sebuah struktur data yang memiliki tambahan satu pointer pada setiap simpulnya. Hal ini memungkinkan Double Linked List untuk melakukan operasi penghapusan dan penambahan pada semua simpul dengan lebih mudah dan efisien [2]. Double Linked List memiliki tiga elemen penting yaitu data, pointer next (menunjuk ke simpul berikutnya), dan pointer prev (menunjuk ke simpul sebelumnya). Double Linked List biasanya digunakan pada web browser untuk navigasi maju dan mundur halaman web. Berbagai aplikasi yang menyediakan fitur undo dan redo, Cance LRU atau MRU yang menggunakan Double Linked List.

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/DoubleLinkedList.png" alt="Alt Text">
</p>

## Guided 

### 1. Guided 1

```C++
#include <iostream>
using namespace std;

///PROGRAM SINGLE LINKED LIST NON-CIRCULAR
//Deklarasi Struct Node
struct Node{
    //komponen/member
    int data;
    Node *next;
};
    Node *head;
    Node *tail;
//Inisialisasi Node
void init(){
    head = NULL;
    tail = NULL;
}
// Pengecekan
bool isEmpty(){
    if (head == NULL)
    return true;
    else
    return false;
}
//Tambah Depan
void insertDepan(int nilai){
    //Buat Node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty() == true){
        head = tail = baru;
        tail->next = NULL;
    }
    else{
        baru->next = head;
        head = baru;
    }
}
//Tambah Belakang
void insertBelakang(int nilai){
    //Buat Node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty() == true){
        head = tail = baru;
        tail->next = NULL;
    }
    else{
    tail->next = baru;
    tail = baru;
    }
}
//Hitung Jumlah List
int hitungList(){
    Node *hitung;
    hitung = head;
    int jumlah = 0;
    while( hitung != NULL ){
        jumlah++;
        hitung = hitung->next;
    }
    return jumlah;
}
//Tambah Tengah
void insertTengah(int data, int posisi){
    if( posisi < 1 || posisi > hitungList() ){
        cout << "Posisi diluar jangkauan" << endl;
    }
    else if( posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        Node *baru, *bantu;
        baru = new Node();
        baru->data = data;
        // tranversing
            bantu = head;
            int nomor = 1;
        while( nomor < posisi - 1 ){
            bantu = bantu->next;
            nomor++;
        }
        baru->next = bantu->next;
        bantu->next = baru;
    }
}
//Hapus Depan
void hapusDepan() {
    Node *hapus;
    if (isEmpty() == false){
        if (head->next != NULL){
            hapus = head;
            head = head->next;
            delete hapus;
        }
        else{
            head = tail = NULL;
        }
    }
    else{
        cout << "List kosong!" << endl;
    }
}
//Hapus Belakang
void hapusBelakang() {
    Node *hapus;
    Node *bantu;
    if (isEmpty() == false){
        if (head != tail){
            hapus = tail;
            bantu = head;
            while (bantu->next != tail){
                bantu = bantu->next;
            }
            tail = bantu;
            tail->next = NULL;
        delete hapus;
        }
        else{
            head = tail = NULL;
        }
    }
    else{
        cout << "List kosong!" << endl;
    }
}
//Hapus Tengah
void hapusTengah(int posisi){
    Node *hapus, *bantu, *bantu2;
    if( posisi < 1 || posisi > hitungList() ){
        cout << "Posisi di luar jangkauan" << endl;
    }
    else if( posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        int nomor = 1;
        bantu = head;
        while( nomor <= posisi ){
            if( nomor == posisi-1 ){
                bantu2 = bantu;
            }
            if( nomor == posisi ){
                hapus = bantu;
            }
            bantu = bantu->next;
            nomor++;
        }
        bantu2->next = bantu;
    delete hapus;
    }
}
//Ubah Depan
void ubahDepan(int data){
    if (isEmpty() == false){
        head->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Ubah Tengah
void ubahTengah(int data, int posisi){
    Node *bantu;
    if (isEmpty() == false){
        if( posisi < 1 || posisi > hitungList() ){
            cout << "Posisi di luar jangkauan" << endl;
        }
        else if( posisi == 1){
            cout << "Posisi bukan posisi tengah" << endl;
        }
        else{
            bantu = head;
            int nomor = 1;
            while (nomor < posisi){
                bantu = bantu->next;nomor++;
            }
            bantu->data = data;
        }
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Ubah Belakang
void ubahBelakang(int data){
    if (isEmpty() == false){
        tail->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Hapus List
void clearList(){
    Node *bantu, *hapus;
    bantu = head;
    while (bantu != NULL){
        hapus = bantu;
        bantu = bantu->next;
        delete hapus;
    }
    head = tail = NULL;
    cout << "List berhasil terhapus!" << endl;
}
//Tampilkan List
void tampil(){
    Node *bantu;
    bantu = head;
    if (isEmpty() == false){
        while (bantu != NULL){
            cout << bantu->data << ends;
            bantu = bantu->next;
        }
        cout << endl;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
int main(){
    init();
    insertDepan(3);
    tampil();
    insertBelakang(5);
    tampil();
    insertDepan(2);
    tampil();
    insertDepan(1);
    tampil();
    hapusDepan();
    tampil();
    hapusBelakang();
    tampil();
    insertTengah(7,2);
    tampil();
    hapusTengah(2);
    tampil();
    ubahDepan(1);
    tampil();
    ubahBelakang(8);
    tampil();
    ubahTengah(11, 2);
    tampil();

    insertTengah(7,1);
    tampil();
    return 0;
}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>
using namespace std;
```

Kode di atas digunakan agar dapat membuat operasi input dan output pada program C++, pada namespace std digunakan agar dalam membuat fungsi tidak perlu menuliskan std lagi.

#### Bagian 2

```C++
struct Node{
    int data;
    Node *next;
};
```

Struktur node terdiri dari dua anggota yaitu data yang dapat menyimpan elemen serta next yang menjadi pointer ke node berikutnya.

#### Bagian 3

```C++
Node *head;
Node *tail;

void init(){
    head = NULL;
    tail = NULL;
}
```

head dan tail sebagai variabel global untuk menunjuk node pertama dan terakhir. Keduanya menjadi NULL yang menginisiasi list kosong.

#### Bagian 4

```C++
bool isEmpty(){
    return (head == NULL);
}
void insertDepan(int nilai){
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty()){
        head = tail = baru;
    }
    else{
        baru->next = head;
        head = baru;
    }
}
```

Mengembalikan true jia linked list kosong dan false jika berisi value. Pada kode berikutnya digunakan untuk menambahkan node baru di depan linked list dengan nilai.

#### Bagian 5

```C++
void insertBelakang(int nilai){
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty()){
        head = tail = baru;
    }
    else{
        tail->next = baru;
        tail = baru;
    }
}
```

Kode di atas digunakan untuk menambahkan sebuah node baru di belakang linked list.

#### Bagian 6

```C++
int hitungList(){
    Node *hitung = head;
    int jumlah = 0;
    while (hitung != NULL){
        jumlah++;
        hitung = hitung->next;
    }
    return jumlah;
}
```

Kode di atas digunakan untuk menghitung jumlah node dalam linked list.

#### Bagian 7

```C++
void insertTengah(int data, int posisi){
    if (posisi < 1 || posisi > hitungList()){
        cout << "Posisi diluar jangkauan" << endl;
    }
    else if (posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        Node *baru = new Node();
        baru->data = data;
        Node *bantu = head;
        int nomor = 1;
        while (nomor < posisi - 1){
            bantu = bantu->next;
            nomor++;
        }
        baru->next = bantu->next;
        bantu->next = baru;
    }
}
```

Menambahkan node baru yang ada di posisi tengah linked list dengan nilai 'data' dan pada posisinya.

#### Bagian 8

```C++
void hapusDepan() {
    if (!isEmpty()){
        Node *hapus = head;
        if (head->next != NULL){
            head = head->next;
        }
        else{
            head = tail = NULL;
        }
        delete hapus;.
    }
    else{
        cout << "List kosong!" << endl;
    }
}
```

Kode di atas ini digunakan untuk menghapus nilai depan linked list.

#### Bagian 9

```C++
void hapusBelakang() {
    if (!isEmpty()){
        Node *hapus = tail;
        if (head != tail){
            Node *bantu = head;
            while (bantu->next != tail){
                bantu = bantu->next;
            }
            tail = bantu;
            tail->next = NULL;
        }
        else{
            head = tail = NULL;
        }
        delete hapus;
    }
    else{
        cout << "List kosong!" << endl;
    }
}

```

Kode di atas ini digunakan untuk menghapus nilai belakang linked list.

#### Bagian 10

```C++
void hapusTengah(int posisi){
    if (posisi < 1 || posisi > hitungList()){
        cout << "Posisi di luar jangkauan" << endl;
    }
    else if (posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        int nomor = 1;
        Node *bantu = head;
        Node *hapus;
        while (nomor <= posisi){
            if (nomor == posisi - 1){
                hapus = bantu->next;
            }
            if (nomor == posisi){
                bantu->next = bantu->next->next;
            }
            bantu = bantu->next;
            nomor++;
        }
        delete hapus;
    }
}
```

Kode di atas ini digunakan untuk menghapus nilai tengah linked list.

#### Bagian 11

```C++
void ubahDepan(int data){
    if (!isEmpty()){
        head->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}

void ubahTengah(int data, int posisi){
    if (!isEmpty()){
        if (posisi < 1 || posisi > hitungList()){
            cout << "Posisi di luar jangkauan" << endl;
        }
        else if (posisi == 1){
            cout << "Posisi bukan posisi tengah" << endl;
        }
        else{
            Node *bantu = head;
            int nomor = 1;
            while (nomor < posisi){
                bantu = bantu->next;
                nomor++;
            }
            bantu->data = data;
        }
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
void ubahBelakang(int data){
    if (!isEmpty()){
        tail->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}

```

Terdapat tiga fungsi pada kode di atas, yaitu fungsi untuk mengubah nilai data dari node yang berada di tengah linked list,mengubah data node pertama dalam linked list, dan node paling belakang.

#### Bagian 12

```C++
void clearList(){
    Node *bantu, *hapus;
    bantu = head;
    while (bantu != NULL){
        hapus = bantu;
        bantu = bantu->next;
        delete hapus;
    }
    head = tail = NULL;
    cout << "List berhasil terhapus!" << endl;
}
```

Fungsi di atas digunakan untuk menghapus semua node yang ada di dalam linked list serta mengembalikan linked list ke dalam kondisi awa (NULL) atau kosong.

#### Bagian 13

```C++
Node *head;
Node *tail;

void init(){
    head = NULL;
    tail = NULL;
}
```

head dan tail sebagai variabel global untuk menunjuk node pertama dan terakhir. Keduanya menjadi NULL yang menginisiasi list kosong.

#### Bagian 14

```C++
void tampil(){
    Node *bantu = head;
    if (!isEmpty()){
        while (bantu != NULL){
            cout << bantu->data << " ";
            bantu = bantu->next;
        }
        cout << endl;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
```

Memunculkan isi dari linked list yang masih ada di dalamnya, jika tidak ada maka akan kosong.

#### Bagian 15

```C++
int main(){
    init(); // Inisialisasi linked list

    // Menambahkan beberapa node ke linked list dan menampilkan isi setiap kali dilakukan operasi
    insertDepan(3);
    tampil();
    insertBelakang(5);
    tampil();
    insertDepan(2);
    tampil();
    insertDepan(1);
    tampil();

    // Menghapus node pertama dan terakhir dari linked list dan menampilkan isi setiap kali dilakukan operasi
    hapusDepan();
    tampil();
    hapusBelakang();
    tampil();

    // Menambahkan node di posisi tengah, kemudian menghapusnya, dan menampilkan isi setiap kali dilakukan operasi
    insertTengah(7, 2);
    tampil();
    hapusTengah(2);
    tampil();

    // Mengubah nilai node pertama, terakhir, dan di posisi tengah, kemudian menampilkan isi setiap kali dilakukan operasi
    ubahDepan(1);
    tampil();
    ubahBelakang(8);
    tampil();
    ubahTengah(11, 2);
    tampil();

    // Menambahkan node baru di posisi tengah dan menampilkan isi linked list akhir
    insertTengah(7, 1);
    tampil();

    return 0;
}
```

Fungsi main atau fungsi utama ini merupakan fungsi yang pertama kali akan dieksekusi dalam progrm. Pada main terdapat berbagai fungsi yang telah dibuat sebelumnya sehingga pada main hanya tinggal mengatur saja posisi fungsi yang telah di buat.

#### Full Code Screenshot

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G1.1.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G1.2.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G1.3.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G1.4.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G1.5.png" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/OGuid1.png" alt="Alt Text">
</p>

#### Penjelasan

Dari hasil output di atas, menyatakan bahwa posisi yang dipilih bukan merupakan posisi tengah, hal ini sudah ada pada setiap fungsi di dalam kode. Fungsi main yang mengatur segalaa output dari kode.


### 2. Guided 2

#### Double Linked List 

```C++
// Rizal Wahyu Pratama
// 2311110029

#include <iostream>
#include <iomanip>

using namespace std;

struct Node {
    string nama_produk;
    int harga;
    Node* prev;
    Node* next;
};

class LinkedList {
private:
    Node* head;
    Node* tail;
public:
    LinkedList() {
        head = NULL;
        tail = NULL;
    }
    void tambahData(string nama_produk, int harga) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (head == NULL) {
            head = newNode;
            tail = newNode;
        }
        else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
    void hapusData(string nama_produk) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                if (currentNode == head) {
                    head = head->next;
                    head->prev = NULL;
                }
                else if (currentNode == tail) {
                    tail = tail->prev;
                    tail->next = NULL;
                }
                else {
                    currentNode->prev->next = currentNode->next;
                    currentNode->next->prev = currentNode->prev;
                }
                delete currentNode;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void updateData(string nama_produk, string new_nama_produk, int new_harga) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                currentNode->nama_produk = new_nama_produk;
                currentNode->harga = new_harga;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void tambahDataUrutan(string nama_produk, int harga, int urutan) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (urutan == 1) {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan - 1) {
                currentNode = currentNode->next;
                i++;
            }
            newNode->prev = currentNode;
            newNode->next = currentNode->next;
            currentNode->next->prev = newNode;
            currentNode->next = newNode;
        }
    }
    void hapusDataUrutan(int urutan) {
        if (urutan == 1) {
            head = head->next;
            head->prev = NULL;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan) {
                currentNode = currentNode->next;
                i++;
            }
            if (currentNode == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                currentNode->prev->next = currentNode->next;
                currentNode->next->prev = currentNode->prev;
            }
        }
    }
    void hapusSeluruhData() {
        while (head != NULL) {
            Node* currentNode = head;
            head = head->next;
            delete currentNode;
        }
        tail = NULL;
    } // <-- add closing bracket here


    void tampilkanData() {
        Node* currentNode = head;
        cout << setw(15) <<left<< "Nama Produk" << setw(10)<<"Harga"<< endl;
        while (currentNode != NULL) {
            cout <<  setw(15) << left <<  currentNode->nama_produk << setw(10) << currentNode->harga << endl;
            currentNode = currentNode->next;
        }
    }
    void tampilkanMenu() {
        int pilihan, harga, urutan;
        string nama_produk, new_nama_produk;
        cout << "Toko Skincare Purwokerto" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Hapus Data" << endl;
        cout << "3. Update Data" << endl;
        cout << "4. Tambah Data Urutan Tertentu" << endl;
        cout << "5. Hapus Data Urutan Tertentu" << endl;
        cout << "6. Hapus Seluruh Data" << endl;
        cout << "7. Tampilkan Data" << endl;
        cout << "8. Exit" << endl;
        do {
            cout << "Pilih menu: ";
            cin >> pilihan;
            switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                tambahData(nama_produk, harga);
                break;
            case 2:
                cout << "Masukkan Nama Produk yang akan dihapus: ";
                cin >> nama_produk;
                hapusData(nama_produk);
                break;
            case 3:
                cout << "Masukkan Nama Produk yang akan diupdate: ";
                cin >> nama_produk;
                cout << "Masukkan Nama Produk baru: ";
                cin >> new_nama_produk;
                cout << "Masukkan Harga baru: ";
                cin >> harga;
                updateData(nama_produk, new_nama_produk, harga);
                break;
            case 4:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                tambahDataUrutan(nama_produk, harga, urutan);
                break;
            case 5:
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                hapusDataUrutan(urutan);
                break;
            case 6:
                hapusSeluruhData();
                break;
            case 7:
                tampilkanData();
                break;
            case 8:
                cout << "Terima kasih." << endl;
                break;
            default:
                cout << "Pilihan tidak tersedia." << endl;
            }
        } while (pilihan != 8);
    }
};

int main() {
    LinkedList list;
    list.tambahData ("Originote",60000);
    list.tambahData ("Somethinc",150000);
    list.tambahData ("Skintific",100000);
    list.tambahData ("Wardah"   ,50000);
    list.tambahData ("Hanasui"  ,30000);
    list.tampilkanMenu();
    return 0;
}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>
#include <iomanip>

using namespace std;
```

Library iostream digunakan untuk menjalankan operasi input dan output pada program dan iomanip digunakan untuk memanipulasi lebar kolom. Lalu namespace std dipanggil agar saat penulisan fungsi tidak perlu ditambahkan std lagi.

#### Bagian 2

```C++
struct Node {
    string nama_produk;
    int harga;
    Node* prev;
    Node* next;
};
```

Kode mendeklarasikan struktur node dimana terdapat dua variabel yaitu nama_produk dan harga. Serta terdapat dua pointer prev dan next yang menunjuk ke node sebelumnya dan berikutnya.

#### Bagian 3

```C++
class LinkedList {
private:
    Node* head;
    Node* tail;
public:
    LinkedList() {
        head = NULL;
        tail = NULL;
    }
    // Fungsi-fungsi anggota LinkedList
};
```

Deklarasi linkedlist sebagai kelas. Dimana LinkedList ini memiliki dua pointer yaitu head dan tail yang menunjuk pada node pertama dan node terakhir dalam linked list.

#### Bagian 4

```C++
void tambahData(string nama_produk, int harga) {
    // Membuat node baru
    Node* newNode = new Node;
    newNode->nama_produk = nama_produk;
    newNode->harga = harga;
    newNode->prev = NULL;
    newNode->next = NULL;
    // Menambahkan node baru ke linked list
    if (head == NULL) {
        head = newNode;
        tail = newNode;
    }
    else {
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode;
    }
}
```

Membuat fungsi tambahData() yang dapat menambahkan node baru yang memiliki nama produk dan harga ke akhir linked list. 

#### Bagian 5

```C++
 void hapusData(string nama_produk) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                if (currentNode == head) {
                    head = head->next;
                    head->prev = NULL;
                }
                else if (currentNode == tail) {
                    tail = tail->prev;
                    tail->next = NULL;
                }
                else {
                    currentNode->prev->next = currentNode->next;
                    currentNode->next->prev = currentNode->prev;
                }
                delete currentNode;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void updateData(string nama_produk, string new_nama_produk, int new_harga) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                currentNode->nama_produk = new_nama_produk;
                currentNode->harga = new_harga;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void tambahDataUrutan(string nama_produk, int harga, int urutan) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (urutan == 1) {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan - 1) {
                currentNode = currentNode->next;
                i++;
            }
            newNode->prev = currentNode;
            newNode->next = currentNode->next;
            currentNode->next->prev = newNode;
            currentNode->next = newNode;
        }
    }
    void hapusDataUrutan(int urutan) {
        if (urutan == 1) {
            head = head->next;
            head->prev = NULL;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan) {
                currentNode = currentNode->next;
                i++;
            }
            if (currentNode == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                currentNode->prev->next = currentNode->next;
                currentNode->next->prev = currentNode->prev;
            }
        }
    }
    void hapusSeluruhData() {
        while (head != NULL) {
            Node* currentNode = head;
            head = head->next;
            delete currentNode;
        }
        tail = NULL;
    } // <-- add closing bracket here


    void tampilkanData() {
        Node* currentNode = head;
        cout << setw(15) <<left<< "Nama Produk" << setw(10)<<"Harga"<< endl;
        while (currentNode != NULL) {
            cout <<  setw(15) << left <<  currentNode->nama_produk << setw(10) << currentNode->harga << endl;
            currentNode = currentNode->next;
        }
    }
    void tampilkanMenu() {
        int pilihan, harga, urutan;
        string nama_produk, new_nama_produk;
        cout << "Toko Skincare Purwokerto" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Hapus Data" << endl;
        cout << "3. Update Data" << endl;
        cout << "4. Tambah Data Urutan Tertentu" << endl;
        cout << "5. Hapus Data Urutan Tertentu" << endl;
        cout << "6. Hapus Seluruh Data" << endl;
        cout << "7. Tampilkan Data" << endl;
        cout << "8. Exit" << endl;
        do {
            cout << "Pilih menu: ";
            cin >> pilihan;
            switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                tambahData(nama_produk, harga);
                break;
            case 2:
                cout << "Masukkan Nama Produk yang akan dihapus: ";
                cin >> nama_produk;
                hapusData(nama_produk);
                break;
            case 3:
                cout << "Masukkan Nama Produk yang akan diupdate: ";
                cin >> nama_produk;
                cout << "Masukkan Nama Produk baru: ";
                cin >> new_nama_produk;
                cout << "Masukkan Harga baru: ";
                cin >> harga;
                updateData(nama_produk, new_nama_produk, harga);
                break;
            case 4:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                tambahDataUrutan(nama_produk, harga, urutan);
                break;
            case 5:
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                hapusDataUrutan(urutan);
                break;
            case 6:
                hapusSeluruhData();
                break;
            case 7:
                tampilkanData();
                break;
            case 8:
                cout << "Terima kasih." << endl;
                break;
            default:
                cout << "Pilihan tidak tersedia." << endl;
            }
        } while (pilihan != 8);
    }
};
```

Terdapat banyak fungsi pada kode di atas seperti fungsi hapusData(), updateData(), tambahDataUrutan(), hapusDataUrutan(), hapusSeluruhData(), tampilkanData(), dan tampilkanMenu(). Fungsi ini dapat melakukan operasi-operasi tambahan pada linked list yang telah dibuat seperti update data, hapus data, menampilkan data, menghapus semua data, dan menampilkan seluruh menu ke pengguna.

#### Bagian 6

```C++
int main() {
    LinkedList list;
    // Menambahkan data awal ke linked list
    list.tambahData ("Originote",60000);
    list.tambahData ("Somethinc",150000);
    list.tambahData ("Skintific",100000);
    list.tambahData ("Wardah"   ,50000);
    list.tambahData ("Hanasui"  ,30000);
    // Menampilkan menu untuk interaksi dengan pengguna
    list.tampilkanMenu();
    return 0;
}
```

Fungsi di atas merupakan fungsi main atau fungsi inti yang akan pertama kali di eksekusi pada program, dengan adanya fungsi main maka kode dapat berjalan sesuai yang kita inginkan. Di kode ini pengguna kode akan dapat melihat menu yag ada pada program lalu dipilih.

#### Full Code Screenshot

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G2.1.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/G2.2.png" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/OGuid2.png" alt="Alt Text">
</p>

#### Penjelasan

Pada output di atas pengguna akan dapat melihat 6 buah menu yang ada pada program, pengguna diminta untuk memasukkan nomor sesuai dengan pilihannya.

## Unguided 

### 1. Unguided 1

#### Buatlah program menu Single Linked List Non-Circular untuk menyimpan Nama dan usia mahasiswa, dengan menggunakan inputan dari user.

**Kode Program:**

```C++
// Rizal Wahyu Pratama
// 2311110029

#include <iostream>
using namespace std;

// deklarasi struct node
struct Node {
    string nama;
    int usia;
    Node* next;
};

// deklarasi head node
Node* head = NULL;

// fungsi untuk menambahkan node di awal
void tambahDiAwal(string nama, int usia) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = head;
    head = newNode;
}

// fungsi untuk menambahkan node di akhir
void tambahDiAkhir(string nama, int usia) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    Node* curr = head;
    while (curr->next != NULL) {
        curr = curr->next;
    }
    curr->next = newNode;
}

// fungsi untuk menambahkan node di tengah
void tambahDiTengah(string nama, int usia, int pos) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    Node* curr = head;
    int i = 1;
    while (i < pos-1 && curr->next != NULL) {
        curr = curr->next;
        i++;
    }
    newNode->next = curr->next;
    curr->next = newNode;
}

// fungsi untuk menghapus node dengan nama tertentu
void hapus(string nama) {
    Node* curr = head;
    Node* prev = NULL;

    while (curr != NULL && curr->nama != nama) {
        prev = curr;
        curr = curr->next;
    }

    if (curr == NULL) {
        cout << "Data tidak ditemukan" << endl;
        return;
    }

    if (prev == NULL) {
        head = curr->next;
    } else {
        prev->next = curr->next;
    }

    delete curr;
}

// fungsi untuk mengubah data node dengan nama tertentu
void ubah(string nama, string newNama, int newUsia) {
    Node* curr = head;

    while (curr != NULL && curr->nama != nama) {
        curr = curr->next;
    }

    if (curr == NULL) {
        cout << "Data tidak ditemukan" << endl;
        return;
    }

    curr->nama = newNama;
    curr->usia = newUsia;
}

// fungsi untuk menampilkan semua data
void tampilkan() {
    if (head == NULL) {
        cout << "List kosong" << endl;
        return;
    }

    Node* curr = head;

    while (curr != NULL) {
        cout << curr->nama << " " << curr->usia << endl;
        curr = curr->next;
    }
}

int main() {
    // memasukkan data pertama (nama dan usia anda)
    string namaAnda;
    int usiaAnda;
    cout << "Masukkan nama anda: ";
    cin >> namaAnda;
    cout << "Masukkan usia anda: ";
    cin >> usiaAnda;
    tambahDiAwal(namaAnda, usiaAnda);
    // memasukkan data lainnya
tambahDiAkhir("John", 19);
tambahDiAkhir("Jane", 20);
tambahDiAkhir("Michael", 18);
tambahDiAkhir("Yusuke", 19);
tambahDiAkhir("Akechi", 20);
tambahDiAkhir("Hoshino", 18);
tambahDiAkhir("Karin", 18);

// menampilkan semua data
cout << "Data awal:" << endl;
tampilkan();

// menghapus data Akechi
hapus("Akechi");
cout << endl << "Setelah menghapus Akechi: " << endl;
tampilkan();

// menambahkan data Futaba di antara Carol dan Ann
tambahDiTengah("Futaba", 18, 3);
cout << endl << "Setelah menambahkan Futaba di antara John dan Jane: " << endl;
tampilkan();

// menambahkan data Igor di awal
tambahDiAwal("Igor", 20);
cout << endl << "Setelah menambahkan Igor di awal: " << endl;
tampilkan();

// mengubah data Carol menjadi Reyn
ubah("Michael", "Reyn", 18);
cout << endl << "Setelah mengubah Michael menjadi Reyn: " << endl;
tampilkan();

// menampilkan semua data setelah perubahan
cout << endl << "Data setelah perubahan:" << endl;
tampilkan();

return 0;
}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>

using namespace std;
```

Library iostream digunakan untuk menjalankan operasi input dan output pada program. Lalu namespace std dipanggil agar saat penulisan fungsi tidak perlu ditambahkan std lagi.

#### Bagian 2

```C++
struct Node {
    string nama;
    int usia;
    Node* next;
};
```

Kode di atas mendeklarasikan struct node yang memperlihatkan semua elemen dalam linked list. Pada node di atas memiliki dua data yaitu nama dan usia serta pointer next yang menunjuk terhadap node selanjutnya.

#### Bagian 3

```C++
Node* head = NULL;

void tambahDiAwal(string nama, int usia) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = head;
    head = newNode;
}
```

Kode di atas mendeklarasikan variabel head sebagai variabel global yang digunakan untuk menyimpan alamat node pertama di dalam linked list. Berikutnya void tambahDiAwal akan digunakan untuk menambahkan node baru di awal list.


#### Bagian 4

```C++
void tambahDiAkhir(string nama, int usia) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    Node* curr = head;
    while (curr->next != NULL) {
        curr = curr->next;
    }
    curr->next = newNode;
}
```

Kode di atas digunakan untuk menambahkan node baru di akhir linked list.

#### Bagian 5

```C++
void tambahDiTengah(string nama, int usia, int pos) {
    Node* newNode = new Node;
    newNode->nama = nama;
    newNode->usia = usia;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    Node* curr = head;
    int i = 1;
    while (i < pos-1 && curr->next != NULL) {
        curr = curr->next;
        i++;
    }
    newNode->next = curr->next;
    curr->next = newNode;
}
```

Pada kode di atas, dibuatkan fungsi yang dapat menambahkan node baru di posisi manapun dalam linked list.

#### Bagian 6

```C++
void hapus(string nama) {
    Node* curr = head;
    Node* prev = NULL;

    while (curr != NULL && curr->nama != nama) {
        prev = curr;
        curr = curr->next;
    }

    if (curr == NULL) {
        cout << "Data tidak ditemukan" << endl;
        return;
    }

    if (prev == NULL) {
        head = curr->next;
    } else {
        prev->next = curr->next;
    }

    delete curr;
}
```

Pada kode di atas, dibuatkan fungsi yang dapat menghapus node dengan nama tertentu dalam linked list.

#### Bagian 7

```C++
void ubah(string nama, string newNama, int newUsia) {
    Node* curr = head;

    while (curr != NULL && curr->nama != nama) {
        curr = curr->next;
    }

    if (curr == NULL) {
        cout << "Data tidak ditemukan" << endl;
        return;
    }

    curr->nama = newNama;
    curr->usia = newUsia;
}
```

Pada kode di atas, dibuatkan fungsi yang dapat mengubah data node degan nama tertentu di dalam linked list.

#### Bagian 8

```C++
void tampilkan() {
    if (head == NULL) {
        cout << "List kosong" << endl;
        return;
    }

    Node* curr = head;

    while (curr != NULL) {
        cout << curr->nama << " " << curr->usia << endl;
        curr = curr->next;
    }
}
```

Pada kode di atas digunakan untuk menampilkan seluruh data di dalam linked list.

#### Bagian 9

```C++
int main() {
    // memasukkan data pertama (nama dan usia anda)
    string namaAnda;
    int usiaAnda;
    cout << "Masukkan nama anda: ";
    cin >> namaAnda;
    cout << "Masukkan usia anda: ";
    cin >> usiaAnda;
    tambahDiAwal(namaAnda, usiaAnda);
    // memasukkan data lainnya
tambahDiAkhir("John", 19);
tambahDiAkhir("Jane", 20);
tambahDiAkhir("Michael", 18);
tambahDiAkhir("Yusuke", 19);
tambahDiAkhir("Akechi", 20);
tambahDiAkhir("Hoshino", 18);
tambahDiAkhir("Karin", 18);

// menampilkan semua data
cout << "Data awal:" << endl;
tampilkan();

// menghapus data Akechi
hapus("Akechi");
cout << endl << "Setelah menghapus Akechi: " << endl;
tampilkan();

// menambahkan data Futaba di antara Carol dan Ann
tambahDiTengah("Futaba", 18, 3);
cout << endl << "Setelah menambahkan Futaba di antara John dan Jane: " << endl;
tampilkan();

// menambahkan data Igor di awal
tambahDiAwal("Igor", 20);
cout << endl << "Setelah menambahkan Igor di awal: " << endl;
tampilkan();

// mengubah data Carol menjadi Reyn
ubah("Michael", "Reyn", 18);
cout << endl << "Setelah mengubah Michael menjadi Reyn: " << endl;
tampilkan();

// menampilkan semua data setelah perubahan
cout << endl << "Data setelah perubahan:" << endl;
tampilkan();

return 0;
}
```

Fungsi di atas merupakan fungsi main yang berupa fungsi utama di dalam program yang disebut dengan fungsi main. Pengguna diminta untuk memasukkan nama dan usianya. Pada data di awal dimasukkan ke dalam linked list menggunakan fungsi-fungsi yang telah didefinisikan pada kode-kode di atas.

#### Full code Screenshot:

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U1.1.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U1.2.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U1.3.png" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/OUn1.png" alt="Alt Text">
</p>

#### Penjelasan

Dari output di atas kita mengetahui bahwa pengguna dapat memasukkan nama dan umur. Dimana pengguna memasukkan nama Rizal dengan umur 19 maka nama Rizal dan umurnya 19 dimasukkan ke dalam Linked List.

### 2. Unguided 2

#### Modifikasi Guided Double Linked List dilakukan dengan penambahan operasi untuk menambah data, menghapus, dan update di tengah / di urutan tertentu yang diminta. Selain itu, buatlah agar tampilannya menampilkan Nama produk dan harga.

**Kode Program:**

```C++
// Rizal Wahyu Pratama
// 2311110029

#include <iostream>
#include <iomanip>

using namespace std;

struct Node {
    string nama_produk;
    int harga;
    Node* prev;
    Node* next;
};

class LinkedList {
private:
    Node* head;
    Node* tail;
public:
    LinkedList() {
        head = NULL;
        tail = NULL;
    }
    void tambahData(string nama_produk, int harga) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (head == NULL) {
            head = newNode;
            tail = newNode;
        }
        else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
    void hapusData(string nama_produk) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                if (currentNode == head) {
                    head = head->next;
                    head->prev = NULL;
                }
                else if (currentNode == tail) {
                    tail = tail->prev;
                    tail->next = NULL;
                }
                else {
                    currentNode->prev->next = currentNode->next;
                    currentNode->next->prev = currentNode->prev;
                }
                delete currentNode;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void updateData(string nama_produk, string new_nama_produk, int new_harga) {
        Node* currentNode = head;
        while (currentNode != NULL) {
            if (currentNode->nama_produk == nama_produk) {
                currentNode->nama_produk = new_nama_produk;
                currentNode->harga = new_harga;
                break;
            }
            currentNode = currentNode->next;
        }
    }
    void tambahDataUrutan(string nama_produk, int harga, int urutan) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (urutan == 1) {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan - 1) {
                currentNode = currentNode->next;
                i++;
            }
            newNode->prev = currentNode;
            newNode->next = currentNode->next;
            currentNode->next->prev = newNode;
            currentNode->next = newNode;
        }
    }
    void hapusDataUrutan(int urutan) {
        if (urutan == 1) {
            head = head->next;
            head->prev = NULL;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan) {
                currentNode = currentNode->next;
                i++;
            }
            if (currentNode == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                currentNode->prev->next = currentNode->next;
                currentNode->next->prev = currentNode->prev;
            }
        }
    }
    void hapusSeluruhData() {
        while (head != NULL) {
            Node* currentNode = head;
            head = head->next;
            delete currentNode;
        }
        tail = NULL;
    } // <-- add closing bracket here


    void tampilkanData() {
        Node* currentNode = head;
        cout << setw(15) <<left<< "Nama Produk" << setw(10)<<"Harga"<< endl;
        while (currentNode != NULL) {
            cout <<  setw(15) << left <<  currentNode->nama_produk << setw(10) << currentNode->harga << endl;
            currentNode = currentNode->next;
        }
    }
    void tampilkanMenu() {
        int pilihan, harga, urutan;
        string nama_produk, new_nama_produk;
        cout << "Toko Skincare Purwokerto" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Hapus Data" << endl;
        cout << "3. Update Data" << endl;
        cout << "4. Tambah Data Urutan Tertentu" << endl;
        cout << "5. Hapus Data Urutan Tertentu" << endl;
        cout << "6. Hapus Seluruh Data" << endl;
        cout << "7. Tampilkan Data" << endl;
        cout << "8. Exit" << endl;
        do {
            cout << "Pilih menu: ";
            cin >> pilihan;
            switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                tambahData(nama_produk, harga);
                break;
            case 2:
                cout << "Masukkan Nama Produk yang akan dihapus: ";
                cin >> nama_produk;
                hapusData(nama_produk);
                break;
            case 3:
                cout << "Masukkan Nama Produk yang akan diupdate: ";
                cin >> nama_produk;
                cout << "Masukkan Nama Produk baru: ";
                cin >> new_nama_produk;
                cout << "Masukkan Harga baru: ";
                cin >> harga;
                updateData(nama_produk, new_nama_produk, harga);
                break;
            case 4:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                tambahDataUrutan(nama_produk, harga, urutan);
                break;
            case 5:
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                hapusDataUrutan(urutan);
                break;
            case 6:
                hapusSeluruhData();
                break;
            case 7:
                tampilkanData();
                break;
            case 8:
                cout << "Terima kasih." << endl;
                break;
            default:
                cout << "Pilihan tidak tersedia." << endl;
            }
        } while (pilihan != 8);
    }
};

int main() {
    LinkedList list;
    list.tambahData ("Originote",60000);
    list.tambahData ("Somethinc",150000);
    list.tambahData ("Skintific",100000);
    list.tambahData ("Wardah"   ,50000);
    list.tambahData ("Hanasui"  ,30000);
    list.tampilkanMenu();
    return 0;
}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>
#include <iomanip>

using namespace std;
```

Library iostream digunakan untuk menjalankan operasi input dan output pada program dan iomanip digunakan untuk memanipulasi lebar kolom. Lalu namespace std dipanggil agar saat penulisan fungsi tidak perlu ditambahkan std lagi.

#### Bagian 2

```C++
struct Node {
    string nama_produk;
    int harga;
    Node* prev;
    Node* next;
};
```

Pada kode di atas dideklarasikan sebuah struct  node yang memiliki dua data seperti nama_produk, harga, prev yang menuju ke node sebelumnya, dan next yang menuju ke node selanjutnya.

#### Bagian 3

```C++
class LinkedList {
private:
    Node* head;
    Node* tail;
public:
    LinkedList() {
        head = NULL;
        tail = NULL;
    }
};
```

Pada kode di atas dideklarasikan sebuah kelas Linked list yang memiliki dua pointer head dan tail yang merupakan node pertama dan terakhir dalam linked list. 

#### Bagian 4

```C++
void tambahData(string nama_produk, int harga) {
    // Pembuatan node baru
    Node* newNode = new Node;
    newNode->nama_produk = nama_produk;
    newNode->harga = harga;
    newNode->prev = NULL;
    newNode->next = NULL;
    // Penambahan node ke dalam linked list
    if (head == NULL) {
        head = newNode;
        tail = newNode;
    } else {
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode;
    }
}
```

Pada kode di atas dibuat fungsi yang dapat menambahkan data produk skincare ke dalam linked list. Data yang baru dibuat akan diletakkan di akhir linked list.

#### Bagian 5

```C++
void hapusData(string nama_produk) {
    // Pencarian node dengan nama_produk yang sesuai
    Node* currentNode = head;
    while (currentNode != NULL) {
        if (currentNode->nama_produk == nama_produk) {
            // Penghapusan node sesuai dengan kondisi
            if (currentNode == head) {
                head = head->next;
                head->prev = NULL;
            } else if (currentNode == tail) {
                tail = tail->prev;
                tail->next = NULL;
            } else {
                currentNode->prev->next = currentNode->next;
                currentNode->next->prev = currentNode->prev;
            }
            delete currentNode;
            break;
        }
        currentNode = currentNode->next;
    }
}
```

Kode di atas merupakan fungsi yang digunakan untuk menghapus data produk dari linked list dengan memasukkan nama produknya. Apabila nama produk yang dimasukkan ada di dalam linked list maka produk tersebut akan dihapus dari linked list.

#### Bagian 6

```C++
void updateData(string nama_produk, string new_nama_produk, int new_harga) {
    // Pencarian node dengan nama_produk yang sesuai
    Node* currentNode = head;
    while (currentNode != NULL) {
        if (currentNode->nama_produk == nama_produk) {
            // Mengubah data node sesuai dengan kondisi
            currentNode->nama_produk = new_nama_produk;
            currentNode->harga = new_harga;
            break;
        }
        currentNode = currentNode->next;
    }
}
```

Fungsi di atas dapat digunakan untuk mengubah data produk hanya dengan memasukkan nama produknya. Apabila nama produk yang dimasukkan ada di dalam linked list maka produk tersebut akan diubah dari linked list.


#### Bagian 7

```C++
    void tambahDataUrutan(string nama_produk, int harga, int urutan) {
        Node* newNode = new Node;
        newNode->nama_produk = nama_produk;
        newNode->harga = harga;
        newNode->prev = NULL;
        newNode->next = NULL;
        if (urutan == 1) {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan - 1) {
                currentNode = currentNode->next;
                i++;
            }
            newNode->prev = currentNode;
            newNode->next = currentNode->next;
            currentNode->next->prev = newNode;
            currentNode->next = newNode;
        }
    }
    void hapusDataUrutan(int urutan) {
        if (urutan == 1) {
            head = head->next;
            head->prev = NULL;
        }
        else {
            Node* currentNode = head;
            int i = 1;
            while (i < urutan) {
                currentNode = currentNode->next;
                i++;
            }
            if (currentNode == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                currentNode->prev->next = currentNode->next;
                currentNode->next->prev = currentNode->prev;
            }
        }
    }
    void hapusSeluruhData() {
        while (head != NULL) {
            Node* currentNode = head;
            head = head->next;
            delete currentNode;
        }
        tail = NULL;
    } // <-- add closing bracket here


    void tampilkanData() {
        Node* currentNode = head;
        cout << setw(15) <<left<< "Nama Produk" << setw(10)<<"Harga"<< endl;
        while (currentNode != NULL) {
            cout <<  setw(15) << left <<  currentNode->nama_produk << setw(10) << currentNode->harga << endl;
            currentNode = currentNode->next;
        }
    }
    void tampilkanMenu() {
        int pilihan, harga, urutan;
        string nama_produk, new_nama_produk;
        cout << "Toko Skincare Purwokerto" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Hapus Data" << endl;
        cout << "3. Update Data" << endl;
        cout << "4. Tambah Data Urutan Tertentu" << endl;
        cout << "5. Hapus Data Urutan Tertentu" << endl;
        cout << "6. Hapus Seluruh Data" << endl;
        cout << "7. Tampilkan Data" << endl;
        cout << "8. Exit" << endl;
        do {
            cout << "Pilih menu: ";
            cin >> pilihan;
            switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                tambahData(nama_produk, harga);
                break;
            case 2:
                cout << "Masukkan Nama Produk yang akan dihapus: ";
                cin >> nama_produk;
                hapusData(nama_produk);
                break;
            case 3:
                cout << "Masukkan Nama Produk yang akan diupdate: ";
                cin >> nama_produk;
                cout << "Masukkan Nama Produk baru: ";
                cin >> new_nama_produk;
                cout << "Masukkan Harga baru: ";
                cin >> harga;
                updateData(nama_produk, new_nama_produk, harga);
                break;
            case 4:
                cout << "Masukkan Nama Produk: ";
                cin >> nama_produk;
                cout << "Masukkan Harga: ";
                cin >> harga;
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                tambahDataUrutan(nama_produk, harga, urutan);
                break;
            case 5:
                cout << "Masukkan Urutan: ";
                cin >> urutan;
                hapusDataUrutan(urutan);
                break;
            case 6:
                hapusSeluruhData();
                break;
            case 7:
                tampilkanData();
                break;
            case 8:
                cout << "Terima kasih." << endl;
                break;
            default:
                cout << "Pilihan tidak tersedia." << endl;
            }
        } while (pilihan != 8);
    }
};
```

Pada kode di atas terdapat 5 buah fungsi yang memiliki tugas yang berbeda-beda seperti tambahDataUrutan, hapusDataUrutan, hapusSeluruhData, tampilkanData, dan tampilkanMenu. Kode di atas akan dapat dipanggil pada fungsi inti nantinya.

#### Bagian 8

```C++
int main() {
    LinkedList list;
    list.tambahData ("Originote",60000);
    list.tambahData ("Somethinc",150000);
    list.tambahData ("Skintific",100000);
    list.tambahData ("Wardah"   ,50000);
    list.tambahData ("Hanasui"  ,30000);
    list.tampilkanMenu();
    return 0;
}
```

Kode di atas merupakan fungsi inti atau fungsi main dari seluruh kode, dimana pada fungsi main ini akan dieksekusi lebih awal di dalam kode. Kode di atas akan mengeksekusi sesuai dengan interuksi dari pembuat kode, ini akan berpengaruh terhadap output dari kode nantinya.

#### Full code Screenshot:

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U2.1.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U2.2.png" alt="Alt Text">
</p>
<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/U2.3.png" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-6/blob/main/Modul%206/SekirinSot/OUn2.png" alt="Alt Text">
</p>

#### Penjelasan

Dari kode di atas, pengguna dapat melihat 8 pilihan jika kode di jalankan. Pengguna dapat memilih sesuai dengan fitur-fitur yang ingin di akses hanya dengan memasukkan nomor dari fiturnya. Seperti menambahkan produk baru maka dapat mengklik angka 1.

## Kesimpulan

Single linked list dan double linked list merupakan dua hal yang hampir mirip. Namun memiliki perbedaan pada pointernya, dimana pada double linked list memiliki satu pointer tambahan dibandingkan single linked list, sehingga double linked list dapat melakukan operasi penghapusan dan penambahan pada semua simpul dengan lebih efisien. Pada single linked list memiliki dua bagian yaitu bagian isi dan bagian pointer. Pada double linked list memiliki tiga elemen penting bagian isi, pointer next dan pointer prev.

Kedua jenis linked list ini memiliki kelebihan dan kekurangannya masing-masing, dimana single linked list  ini nodenya saling sambung menyambung dan tersusun secara sekuensial. Pada double linked list saling menyambung seperti bolak-balik. Namun kekurangannya pada double linked list akan lebih lama dalam waktu eksekusi dibandingkan single linked list.

## Referensi

[1]	R. Selamet, “Implementasi Struktur Data List, Queue Dan Stack Dalam Java,” Media Inform., vol. 15, no. 3, pp. 18–25, 2016.

[2]	S. Santosa A. Aliyanto,and S. Utomo, “Sistem Pembelajaran Algoritma Stack Dan Queue Dengan Pendekatan Program Based Learning,” J. Teknol. Inf., vol. 7, no. 1, pp. 17–18, 2019.


