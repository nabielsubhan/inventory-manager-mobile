# Inventory Manager
**Nama    : Muhammad Nabiel Subhan**<br>
**NPM     : 2206081553**<br>
**Kelas   : PBP A**<br>

## Tugas 7: Elemen Dasar Flutter
### Perbedaan utama antara *stateless* dan *stateful widget* dalam konteks pengembangan aplikasi Flutter
* *Stateless Widget*<br>
*Stateless widget* adalah suatu widget yang tidak mempunyai *state* atau kondisi yang bisa berubah-ubah sepanjang program berjalan atau bisa dibilang sebagai entitas yang statis. Widget ini cocok digunakan untuk membuat bagian antarmuka yang tidak berubah-ubah jika dikenakan berbagai macam interaksi kepadanya. Karena widget ini tidak akan berubah-ubah, maka pembuatannya hanya dilakukan sekali saja ketika diperlukan.

* *Stateful Widget*<br>
Berbeda dengan *Stateless Widget*, *Stateful Widget* adalah suatu widget yang mempunyai *state* atau kondisi yang dapat berubah-ubah atau merupakan entitas yang dinamis. Widget ini cocok digunakan untuk membuat bagian antarmuka yang perlu berubah ketika dikenakan interaksi kepadanya, seperti button yang berubah warna ketika diklik, dan lain sebagainya. Karena widget ini akan berubah-ubah, maka Flutter akan membuat widget tersebut berkali-kali sesuai dengan perubahan yang terjadi kepada widget tersebut untuk memperlihatkan perubahan yang terjadi. Pengelolaan *Stateful Widget* juga sedikit berbeda dengan *Stateless Widget*, yaitu diperlukannya kelas tambahan yang disebut kelas **State** yang berfungsi untuk mengelola *state* dari suatu widget.

### Widget-widget yang digunakan pada tugas kali ini
* `Scaffold`, mengatur struktur dasar halaman aplikasi, menampilkan AppBar dan Body.
* `AppBar`, untuk menampilkan judul aplikasi.
* `Text`, untuk menampilkan string teks.
* `SingleChildScrollView`, menampilkan suatu widget yang isinya dapat di-*scroll*.
* `Padding`, untuk memberikan *padding* yang ditentukan kepada child.
* `Column`, untuk menampilkan *children* secara vertikal.
* `GridView`, untuk menampilkan *children* dengan layout *grid*.
* `ItemCard`, *stateless widget* berisi widget-widget lain untuk membentuk suatu kesatuan *card* yang akan menjadi suatu template.
* `Material`, untuk memberikan design kepada child.
* `InkWell`, untuk memungkinkan sentuhan responsif pada child.
* `SnackBar`, untuk menampilkan pesan singkat di bagian bawah layar.
* `Container`, untuk mengatur tata letak, *style*, dan properti lainnya pada child.
* `Center`, untuk memosisikan child agar berada di tengah.
* `Icon`, untuk menampilkan ikon.

### Implementasi Checklist Tugas 7
1. Pergi ke direktori dimana aplikasi ini ingin dibuat, lalu buka *command prompt* pada direktori tersebut.
2. Membuat proyek Flutter baru dengan nama `inventory_manager` dengan menggunakan command berikut.
   ```
   flutter create inventory_manager
   cd inventory_manager
   ```
3. Membuat file baru dengan nama `menu.dart` pada folder `lib`, lalu tambahkan baris import berikut.
   ```dart
   import 'package:flutter/material.dart';
   ```
4. Memindahkan kode pada file `main.dart` pada bagian *class* `MyHomePage` dan `_MyHomePage` ke file `menu.dart`.
5. Menambahkan baris import berikut ke file `main.dart` agar class `MyHomePage` tetap bisa digunakan di file `main.dart`.
   ```dart
   import 'package:inventory_manager/menu.dart';
   ```
6. Mengubah sifat widget `MyHomePage` menjadi *stateless* dengan mengubah kode pada class `MyHomePage` menjadi seperti berikut.
   ```dart
   class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);
  
    @override
      Widget build(BuildContext context) {
          return Scaffold(

          )
   ```
7. Mengubah baris kode `MyHomePage(title: 'Flutter Demo Home Page')` pada file `main.dart` menjadi `MyHomePage()`.
8. Membuat class Item.
   ```dart
   class Item {
    final String name;
    final IconData icon;
  
    Item(this.name, this.icon);
   }
   ```
9. Menambahkan baris kode berikut untuk menambahkan item-item yang akan dibuat di bawah *constructor* pada class `MyHomePage`.
    ```dart
    final List<ShopItem> items = [
      ShopItem("Lihat Produk", Icons.checklist),
      ShopItem("Tambah Produk", Icons.add_shopping_cart),
      ShopItem("Logout", Icons.logout),
    ];
    ```
10. Menambahkan kode berikut di dalam `Widget build` pada class `MyHomePage`.
    ```dart
    return Scaffold(
            appBar: AppBar(
              backgroundColor: Color(0xFF0E2954),
              title: const Text(
                'Inventory Manager',
                style: TextStyle(
                  color: Colors.white,
                )
              ),
            ),
            body: SingleChildScrollView(
              // Widget wrapper yang dapat discroll
              child: Padding(
                padding: const EdgeInsets.all(10.0), // Set padding dari halaman
                child: Column(
                  // Widget untuk menampilkan children secara vertikal
                  children: <Widget>[
                    const Padding(
                      padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                      // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                      child: Text(
                        'Inventory', // Text yang menandakan toko
                        textAlign: TextAlign.center,
                        style: TextStyle(
                          fontSize: 30,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ),
                    // Grid layout
                    GridView.count(
                      // Container pada card kita.
                      primary: true,
                      padding: const EdgeInsets.all(20),
                      crossAxisSpacing: 10,
                      mainAxisSpacing: 10,
                      crossAxisCount: 3,
                      shrinkWrap: true,
                      children: items.map((Item item) {
                        // Iterasi untuk setiap item
                        return ItemCard(item);
                      }).toList(),
                    ),
                  ],
                ),
              ),
            ),
        ); 
    ```
11. Membuat *stateless widget* `ItemCard` untuk menampilkan card.
    ```dart
    class ItemCard extends StatelessWidget {
      final Item item;
    
      const ItemCard(this.item, {super.key}); // Constructor
    
      @override
      Widget build(BuildContext context) {
        return Material(
          color: item.color,
          child: InkWell(
            // Area responsive terhadap sentuhan
            onTap: () {
              // Memunculkan SnackBar ketika diklik
              ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("Kamu telah menekan tombol ${item.name}!")));
            },
            child: Container(
              // Container untuk menyimpan Icon dan Text
              padding: const EdgeInsets.all(8),
              child: Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(
                      item.icon,
                      color: Colors.white,
                      size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                      item.name,
                      textAlign: TextAlign.center,
                      style: const TextStyle(color: Colors.white),
                    ),
                  ],
                ),
              ),
            ),
          ),
        );
      }
    }
    ```
12. Menghapus class `_MyHomePage` karena widget `MyHomePage` sudah berubah menjadi *stateless* sehingga class `_MyHomePage` tidak dibutuhkan.

### Bonus (mengimplementasikan warna-warna berbeda untuk setiap tombol `Lihat Item`, `Tambah Item`, dan `Logout`)
1. Menambahkan atribut baru pada class `Item` untuk menyimpan warna tiap Item.
   ```dart
   class Item {
      final String name;
      final IconData icon;
      final Color color;
    
      Item(this.name, this.icon, this.color);
    }
   ```
2. Menambahkan argumen warna yang diinginkan pada setiap item di variabel `items`.
   ```dart
   final List<Item> items = [
      Item("Lihat Item", Icons.checklist, Color(0xFF78D6C6)),
      Item("Tambah Item", Icons.add_shopping_cart, Color(0xFF419197)),
      Item("Logout", Icons.logout, Color(0xFF12486B)),
   ];
   ```
3. Mengubah baris kode pada `Widget build` di class `ItemCard` pada bagian `color: Colors.indigo,` menjadi `color: item.color,`.
