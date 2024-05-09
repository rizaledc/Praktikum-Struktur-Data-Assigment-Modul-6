# <h1 align="center">Laporan Praktikum Modul Struct dan Implementasi</h1>
<p align="center">Rizal Wahyu Pratama</p>
<p align="center">2311110029</p>
<p align="center">S1SD-04-B</p>

## Tujuan Praktikum

1.	Mahasiswa memahami perbedaan konsep Single, Double, Circular dan Non Linked List. 
2.	Mahasiswa mampu menerapkan SingleSingle, Double, Circular dan Non Linked List ke dalam pemrograman.

## Dasar Teori

List adalah sekumpulan data sejenis yang berada dalam lokasi yang fleksibel 
(dapat berubah sesuai dengan kebutuhan) (Rachmat Slamet). List dapat dibagi menjadi dua yaitu single linked list dan Double Linked List. 

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
Double Linked List merupakan sebuah struktur data yang memiliki tambahan satu pointer pada setiap simpulnya. Hal ini memungkinkan Double Linked List untuk melakukan operasi penghapusan dan penambahan pada semua simpul dengan lebih mudah dan efisien. Double Linked List memiliki tiga elemen penting yaitu data, pointer next (menunjuk ke simpul berikutnya), dan pointer prev (menunjuk ke simpul sebelumnya). Double Linked List biasanya digunakan pada web browser untuk navigasi maju dan mundur halaman web. Berbagai aplikasi yang menyediakan fitur undo dan redo, Cance LRU atau MRU yang menggunakan Double Linked List.

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

#### Bagian 13

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

#### Bagian 13

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

#### Buatlah sebuah struktur dengan skema seperti dibawah, isi dengan nilai kemudian jalankan. 

```C++
#include <iostream>
#include <string>
using namespace std;

struct hewan {
    string nama_hewan;
    string jenis_kelamin;
    string kembangbiak;
    string pernafasan;
    string tempat_hidup;
    bool karnivora;
}; 

struct hewan_darat{
    hewan info_hewan;
    int jumlah_kaki;
    bool apakah_menyusui;
    string suara;
};
hewan_darat hewan1;

struct hewan_laut{
    hewan info_hewan;
    string bentuk_sirip;
    string pertahanan_diri;
};
hewan_laut hewan2;

int main() {
    hewan1.info_hewan.nama_hewan = "Anjing";
    hewan1.info_hewan.jenis_kelamin = "Laki-laki";
    hewan1.info_hewan.kembangbiak = "Melahirkan";
    hewan1.info_hewan.pernafasan = "Paru paru";
    hewan1.info_hewan.tempat_hidup = "Darat";
    hewan1.info_hewan.karnivora = true;
    hewan1.jumlah_kaki = 4;
    hewan1.apakah_menyusui = true;   
    hewan1.suara = "Rawrr, guk, guk,guk";
    
    hewan2.info_hewan.nama_hewan = "Paus";
    hewan2.info_hewan.jenis_kelamin = "Perempuan";
    hewan2.info_hewan.kembangbiak = "Melahirkan";
    hewan2.info_hewan.pernafasan = "paru paru";
    hewan2.info_hewan.tempat_hidup = "Perairan (Laut)";
    hewan2.info_hewan.karnivora = false;
    hewan2.bentuk_sirip = "dosal, sabit, dan gumpalan";
    hewan2.pertahanan_diri = " Menghirup Oksigen di udara";   

	//menampilkan data 
	cout << "\t Hewan Darat" << endl;
	cout << "Nama Hewan :" <<hewan1.info_hewan.nama_hewan << endl;
	cout << "Jenis Kelamin : "<<hewan1.info_hewan.jenis_kelamin << endl;
	cout << "Kembangbiak : "<< hewan1.info_hewan.kembangbiak << endl;
	cout << "Pernapasan : "<< hewan1.info_hewan.pernafasan << endl;
	cout << "Tempat Hidup : "<< hewan1.info_hewan.tempat_hidup << endl;
	cout << "karnivora : "<< hewan1.info_hewan.karnivora << endl;
	cout << "jumlah kaki : "<< hewan1.jumlah_kaki << endl;
	cout << "apakah menyusui?  : "<< hewan1.apakah_menyusui << endl;
	cout << "suara : "<< hewan1.suara << "\n" << endl ;

	//menampilkan data 
	cout << "\t Hewan Laut" << endl;
	cout << "Nama Hewan :" <<hewan2.info_hewan.nama_hewan << endl;
	cout << "Jenis Kelamin : "<<hewan2.info_hewan.jenis_kelamin << endl;
	cout << "Kembangbiak : "<< hewan2.info_hewan.kembangbiak << endl;
	cout << "Pernapasan : "<< hewan2.info_hewan.pernafasan << endl;
	cout << "Tempat Hidup : "<< hewan2.info_hewan.tempat_hidup << endl;
	cout << "apakah karnivora? "<< hewan2.info_hewan.karnivora << endl;
	cout << "bentuk sirip : "<< hewan2.bentuk_sirip << endl;
	cout << "pertahanan diri : "<< hewan2.pertahanan_diri << endl;


	return 0;
	}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>
#include <string>

using namespace std;
```

Library iostream digunakan untuk menjalankan operasi input dan output pada program. Library string digunakan untuk memanipulasi dan mengolah data string. Lalu namespace std dipanggil agar saat penulisan fungsi tidak perlu ditambahkan std lagi.

#### Bagian 2

```C++
struct hewan {
    string nama_hewan;
    string jenis_kelamin;
    string kembangbiak;
    string pernafasan;
    string tempat_hidup;
    bool karnivora;
}; 

struct hewan_darat{
    hewan info_hewan;
    int jumlah_kaki;
    bool apakah_menyusui;
    string suara;
};
hewan_darat hewan1;

struct hewan_laut{
    hewan info_hewan;
    string bentuk_sirip;
    string pertahanan_diri;
};
hewan_laut hewan2;
```

Pada kode di atas, didefinisikan 3 buah struct. Dimana struct yang pertama yaitu struct hewan yang merupakan struct inti dari dua struct setelahnya. Di dalam struct ini didefinisikan 5 variabel yang akan diisi dengan valuenya masing-masing. Berikutnya terdapat 2 struct turunan dari struct hewan yaitu struct hewan_darat dan struct hewan_laut sebagai tambahan informasi dari masing-masing jenis hewan.

#### Bagian 3

```C++
int main() {
    hewan1.info_hewan.nama_hewan = "Anjing";
    hewan1.info_hewan.jenis_kelamin = "Laki-laki";
    hewan1.info_hewan.kembangbiak = "Melahirkan";
    hewan1.info_hewan.pernafasan = "Paru paru";
    hewan1.info_hewan.tempat_hidup = "Darat";
    hewan1.info_hewan.karnivora = true;
    hewan1.jumlah_kaki = 4;
    hewan1.apakah_menyusui = true;   
    hewan1.suara = "Rawrr, guk, guk,guk";
    
    hewan2.info_hewan.nama_hewan = "Paus";
    hewan2.info_hewan.jenis_kelamin = "Perempuan";
    hewan2.info_hewan.kembangbiak = "Melahirkan";
    hewan2.info_hewan.pernafasan = "paru paru";
    hewan2.info_hewan.tempat_hidup = "Perairan (Laut)";
    hewan2.info_hewan.karnivora = false;
    hewan2.bentuk_sirip = "dosal, sabit, dan gumpalan";
    hewan2.pertahanan_diri = " Menghirup Oksigen di udara";   

	//menampilkan data 
	cout << "\t Hewan Darat" << endl;
	cout << "Nama Hewan :" <<hewan1.info_hewan.nama_hewan << endl;
	cout << "Jenis Kelamin : "<<hewan1.info_hewan.jenis_kelamin << endl;
	cout << "Kembangbiak : "<< hewan1.info_hewan.kembangbiak << endl;
	cout << "Pernapasan : "<< hewan1.info_hewan.pernafasan << endl;
	cout << "Tempat Hidup : "<< hewan1.info_hewan.tempat_hidup << endl;
	cout << "karnivora : "<< hewan1.info_hewan.karnivora << endl;
	cout << "jumlah kaki : "<< hewan1.jumlah_kaki << endl;
	cout << "apakah menyusui?  : "<< hewan1.apakah_menyusui << endl;
	cout << "suara : "<< hewan1.suara << "\n" << endl ;

	//menampilkan data 
	cout << "\t Hewan Laut" << endl;
	cout << "Nama Hewan :" <<hewan2.info_hewan.nama_hewan << endl;
	cout << "Jenis Kelamin : "<<hewan2.info_hewan.jenis_kelamin << endl;
	cout << "Kembangbiak : "<< hewan2.info_hewan.kembangbiak << endl;
	cout << "Pernapasan : "<< hewan2.info_hewan.pernafasan << endl;
	cout << "Tempat Hidup : "<< hewan2.info_hewan.tempat_hidup << endl;
	cout << "apakah karnivora? "<< hewan2.info_hewan.karnivora << endl;
	cout << "bentuk sirip : "<< hewan2.bentuk_sirip << endl;
	cout << "pertahanan diri : "<< hewan2.pertahanan_diri << endl;


	return 0;
	}
```

Fungsi di atas merupakan fungsi main atau fungsi utama dalam pemrograman, fungsi ini akan dieksekusi pertama kali dalam program. Dimana programer akan mengisi masing-masing value dari variabel yang disediakan. Lalu programer akan membuat kode yang berupa output dari value-value yang telah di masukkan. Mulai dari hewan_darat sampai hewan_laut.

#### Output:

```C++
Hewan Darat
Nama Hewan :Anjing
Jenis Kelamin : Laki-laki
Kembangbiak : Melahirkan
Pernapasan : Paru paru
Tempat Hidup : Darat
karnivora : 1
jumlah kaki : 4
apakah menyusui?  : 1
suara : Rawrr, guk, guk,guk

         Hewan Laut
Nama Hewan :Paus
Jenis Kelamin : Perempuan
Kembangbiak : Melahirkan
Pernapasan : paru paru
Tempat Hidup : Perairan (Laut)
apakah karnivora? 0
bentuk sirip : dosal, sabit, dan gumpalan
pertahanan diri :  Menghirup Oksigen di udara
```

**Penjelasan:**

Sesuai dengan fungsi main, output di atas urutannya telah di atur dalam fungsi main. Dimana output yang pertama tentunya akan berisi informasi dari jenis hewan darat, berikutnya akan berisi output dari jenis hewan laut. Output ini sesuai dengan value yang dimasukkan oleh programer ke dalam variabelnya.

#### Full Code Screenshot

<p align="center">
  <img src="" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="" alt="Alt Text">
</p>

## Unguided 

### 1. Unguided 1

#### Modifikasi tugas guided pertama, sehingga setiap item yang terdapat pada struct buku berupa array yang berukuran 5, isi dengan data kemudian tampilkan.

**Kode Program:**

```C++
#include <iostream>
#include <string>

using namespace std;

const int MAX_BUKU = 5;

struct Buku {
    string judul_buku;
    string pengarang;
    string penerbit;
    int tebal_buku;
    double harga_buku;
    int tahun_terbit;
};

// Fungsi untuk memasukkan data buku
void tambahData(Buku &buku) {
    cout << "Judul Buku: ";
    getline(cin, buku.judul_buku);
    cout << "Pengarang: ";
    getline(cin, buku.pengarang);
    cout << "Penerbit: ";
    getline(cin, buku.penerbit);
    cout << "Tebal Buku (halaman): ";
    cin >> buku.tebal_buku;
    cout << "Harga Buku: ";
    cin >> buku.harga_buku;
    cout << "Tahun Terbit: ";
    cin >> buku.tahun_terbit;
    cin.ignore(); // Membersihkan buffer input
}

int main() {
    Buku daftar_buku[MAX_BUKU];

    // Memasukkan data untuk setiap buku
    for (int i = 0; i < MAX_BUKU; ++i) {
        cout << "Masukkan data untuk Buku " << i + 1 << endl;
        tambahData(daftar_buku[i]);
        cout << endl;
    }

    // Menampilkan data buku yang telah dimasukkan
    cout << "Data Buku:"<<endl<<endl;
    for (int i = 0; i < MAX_BUKU; ++i) {
        cout << "Daftar Buku ke-" << i + 1 << endl;
        cout << "Judul: " << daftar_buku[i].judul_buku << endl;
        cout << "Pengarang: " << daftar_buku[i].pengarang << endl;
        cout << "Penerbit: " << daftar_buku[i].penerbit << endl;
        cout << "Tebal Buku: " << daftar_buku[i].tebal_buku << " halaman" << endl;
        cout << "Harga Buku: Rp" << daftar_buku[i].harga_buku << endl;
        cout << "Tahun Terbit: " << daftar_buku[i].tahun_terbit << endl << endl;
    }

    return 0;
}
```

**Penjelasan:**

#### Bagian 1

```C++
#include <iostream>
#include <string>

using namespace std;
```

Library iostream digunakan untuk menjalankan operasi input dan output pada program. #include <string> digunakan mengatur string lebih luas dan lebih mudah serta dapat dimanipulasi. Lalu namespace std dipanggil agar saat penulisan fungsi tidak perlu ditambahkan std lagi.

#### Bagian 2

```C++
const int MAX_BUKU = 5;
```

Kode di atas mendeklarasikan konstanta MAX_BUKU yang mengizinkan maksimal buku di input sebanyak 5 buku.


#### Bagian 3

```C++
struct Buku {
    string judul_buku;
    string pengarang;
    string penerbit;
    int tebal_buku;
    double harga_buku;
    int tahun_terbit;
};
```

Kode di atas mendeklarasikan sebuah struct dengan nama Buku dengan 6 anggotanya tentunya memiliki tipe data yang berbeda-beda. Variabel yang telah dideklarasikan dalam struct ini akan digunakan pada fungsi main dan diberi value oleh pengguna yang memberi inputan.


#### Bagian 4

```C++
void tambahData(Buku &buku) {
    cout << "Judul Buku: ";
    getline(cin, buku.judul_buku);
    cout << "Pengarang: ";
    getline(cin, buku.pengarang);
    cout << "Penerbit: ";
    getline(cin, buku.penerbit);
    cout << "Tebal Buku (halaman): ";
    cin >> buku.tebal_buku;
    cout << "Harga Buku: ";
    cin >> buku.harga_buku;
    cout << "Tahun Terbit: ";
    cin >> buku.tahun_terbit;
    cin.ignore(); // Membersihkan buffer input
}
```

Kode di atas mendeklarasikan fungsi dengan nama tambahData. Fungsi ini dibuat untuk memasukkan data buku ke dalam struct Buku. Dimana fungsi tambahData ini akan digunakan pada fungsi main untuk menerima inputan dari pengguna program.

#### Bagian 5

```C++
int main() {
    Buku daftar_buku[MAX_BUKU];

    // Memasukkan data untuk setiap buku
    for (int i = 0; i < MAX_BUKU; ++i) {
        cout << "Masukkan data untuk Buku " << i + 1 << endl;
        tambahData(daftar_buku[i]);
        cout << endl;
    }

    // Menampilkan data buku yang telah dimasukkan
    cout << "Data Buku:"<<endl<<endl;
    for (int i = 0; i < MAX_BUKU; ++i) {
        cout << "Daftar Buku ke-" << i + 1 << endl;
        cout << "Judul: " << daftar_buku[i].judul_buku << endl;
        cout << "Pengarang: " << daftar_buku[i].pengarang << endl;
        cout << "Penerbit: " << daftar_buku[i].penerbit << endl;
        cout << "Tebal Buku: " << daftar_buku[i].tebal_buku << " halaman" << endl;
        cout << "Harga Buku: Rp" << daftar_buku[i].harga_buku << endl;
        cout << "Tahun Terbit: " << daftar_buku[i].tahun_terbit << endl << endl;
    }

    return 0;
```

Fungsi di atas merupakan fungsi main yang berupa fungsi utama di dalam progran. Fungsi ini akan meminta pengguna untuk memasukkan value dari setiap variabel yang telah dideklarasikan. for (int i = 0; i < MAX_BUKU; ++i) { } digunakan untuk meminta pengguna memasukkan value hingga maksimal 5 buku sesuai batas yang ditetapkan. Pada kode berikutnya, programer membuat ouput yang sesuai dengan value yang dimasukkan oleh pengguna.


**Output:**

```C++
Masukkan data untuk Buku 1
Judul Buku: Perjalanan Menuju Bintang
Pengarang: Rizal Pratama
Penerbit: Erlangga
Tebal Buku (halaman): 172
Harga Buku: 99000
Tahun Terbit: 2024

Masukkan data untuk Buku 2
Judul Buku: Seorang Pria Pencari Kesalahan Wanita
Pengarang: Wisnu Aji
Penerbit: Erlangga
Tebal Buku (halaman): 90
Harga Buku: 169000
Tahun Terbit: 2015

Masukkan data untuk Buku 3
Judul Buku: Seorang Kristen Pindah Muslim
Pengarang: Mikhael
Penerbit: Sinar Dunia
Tebal Buku (halaman): 800
Harga Buku: 400000
Tahun Terbit: 2010

Masukkan data untuk Buku 4
Judul Buku: Perjalanan Menjadi Coach 
Pengarang: Yoka
Penerbit: Montoon
Tebal Buku (halaman): 76
Harga Buku: 50000
Tahun Terbit: 2020

Masukkan data untuk Buku 5
Judul Buku: Cinta yang Tak Pernah ku Bayangkan
Pengarang: Fahmi Hidayat
Penerbit: PLH Entertain
Tebal Buku (halaman): 200
Harga Buku: 56000
Tahun Terbit: 2023

Data Buku:

Daftar Buku ke-1
Judul: Perjalanan Menuju Bintang
Pengarang: Rizal Pratama
Penerbit: Erlangga
Tebal Buku: 172 halaman
Harga Buku: Rp99000
Tahun Terbit: 2024

Daftar Buku ke-2
Judul: Seorang Pria Pencari Kesalahan Wanita
Pengarang: Wisnu Aji
Penerbit: Erlangga
Tebal Buku: 90 halaman
Harga Buku: Rp169000
Tahun Terbit: 2015

Daftar Buku ke-3
Judul: Seorang Kristen Pindah Muslim
Pengarang: Mikhael
Penerbit: Sinar Dunia
Tebal Buku: 800 halaman
Harga Buku: Rp400000
Tahun Terbit: 2010

Daftar Buku ke-4
Judul: Perjalanan Menjadi Coach
Pengarang: Yoka
Penerbit: Montoon
Tebal Buku: 76 halaman
Harga Buku: Rp50000
Tahun Terbit: 2020

Daftar Buku ke-5
Judul: Cinta yang Tak Pernah ku Bayangkan
Pengarang: Fahmi Hidayat
Penerbit: PLH Entertain
Tebal Buku: 200 halaman
Harga Buku: Rp56000
Tahun Terbit: 2023
```

#### Penjelasan

Pada output di atas, pengguna memasukkan value yang berbeda dari 5 buku. Mulai dari judul, pengarang, penerbit, tebal buku, harga buku, dan tahun terbit. Semua value yang dimasukkan akan keluar seperti output di atas sesuai dengan yang dideklarasikan pada fungsi main.

#### Full code Screenshot:

<p align="center">
  <img src="https://github.com/rizaledc/Praktikum-Struktur-Data-Assigment-Modul-5/blob/main/Modul%205/SS/codeunguided1.png" alt="Alt Text">
</p>

#### Screenshot Output

<p align="center">
  <img src="" alt="Alt Text">
</p>

NB : Screenshot terlalu panjang, oleh karena itu screenshot dibagi menjadi dua bagian.


### 2. Unguided 2

#### Apa yang terjadi jika deklarasi variabel struct yang dibuat pada tugas guided I, berjenis Array. Bagaimana cara mengisi data dan menampilkannya ? 

a. Jika deklarasi variabel struct pada guided 1 beripe array, dimana contohnya adalah Buku daftar_buku[MAX_BUKU] maka kita telah membuat array dari struktur buku dengan ukurannya yaitu MAX_BUKU yang dapat menyimpan buku hingga 5 jenis buku. 

b. Cara mengisi datanya sangatlah mudah, fungsi tambahData akan menerima objek Buku, lau digunakan sebuah looping for disetiap elemen dalam array daftar_buku. Berikutnya terdapat fungsi tambahData yang meminta pengguna kode untuk memasukkan judul buku, pengarang, penerbit, tebal buku, harga buku, dan tahun terbit yang disimpan dalam objek Buku. 

c. Untuk menampilkan datanya, digunakan looping for yang akan melakukan perulangan dalam elemen di dalam array daftar_buku. Kemudian, program akan mencetak setiap value yang diinputkan pada setiap variabel Buku.

## Kesimpulan

Pemrograman merupakan sebuah proses dalam pembuat program sebuah komputer. Dalam pembuatan program ini tentunya seorang programer harus memilih salah satu dari banyak bahasa pemrograman, salah satunya C++. Dalam bahasa pemrograman C++ terdapat Struct yang memungkinkan seseorang untuk membuat tipe data baru yang terdiri dari beberapa tipe data standar atau tipe data bentukan lainnya. 

Dalam bahasa pemrograman C++, struct dapat mempermudah dan memungkinkan programer untuk mengatur dan mengelola data dengan lebih baik. Tentunya, dengan algoritma yang tepat dalam penulisan struct dapat memberikan kemudahan dan meningkatkan efisiensi perangkat lunak.

## Referensi


[2]	A. Aliyanto, S. Utomo, and S. Santosa, “Sistem Pembelajaran Algoritma Stack Dan Queue Dengan Pendekatan Program Based Learning,” J. Teknol. Inf., vol. 7, no. 1, pp. 17–18, 2011.


