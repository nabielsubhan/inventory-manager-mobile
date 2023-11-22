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
* `Material`, untuk memberikan design kepada child berdasarkan desain dari Material Design.
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
   ```dart
   class ItemCard extends StatelessWidget {
     ...
     @override
     Widget build(BuildContext context) {
       return Material(
         color: item.color,
         ...
   ```

## Tugas 8: Flutter Navigation, Layouts, Forms, and Input Elements
### Perbedaan antara Navigator.push() dan Navigator.pushReplacement()
* `Navigator.push()` digunakan untuk menambahkan suatu layar ke dalam tumpukan navigasi, tetapi tidak menghapus layar yang saat ini sehingga setelah melakukan `Navigator.push()`, pengguna masih bisa kembali ke halaman sebelumnya dengan menggunakan fungsi `Navigator.pop()`. Contohnya ketika menekan button pada HomePage untuk pergi ke halaman suatu fitur dan setelah pindah, kita masih bisa kembali lagi ke halaman HomePage.
  ```dart
  onTap: () {
     Navigator.push(context,
        MaterialPageRoute(builder: (context) => const AboutPage()));
   },
  ```
* `Navigator.pushReplacement` digunakan untuk menambahkan suatu layar ke dalam tumpukan navigasi, tetapi menghapus terlebih dahulu layar yang saat ini sehingga pengguna tidak bisa kembali ke halaman sebelumnya. Contohnya ketika setelah melakukan login pada aplikasi dan kita ingin agar pengguna pergi ke HomePage tanpa bisa kembali lagi ke halaman login.
  ```dart
  onTap: () {
     Navigator.pushReplacement(
         context,
         MaterialPageRoute(
           builder: (context) => MyHomePage(),
         ));
   },
  ```

### *Layout widgets* pada Flutter dan konteks penggunaannya

| Layout Widget | Konteks Penggunaan |
|---------------|--------------------|
| Container     | Sebagai tempat untuk menyimpan widget lain dan dapat memberikan properti padding, margin, dan dekorasi kepada childrennya |
| GridView      | Digunakan ketika ingin menyusun children-nya dalam bentuk grid |
| ListView      | Digunakan ketika ingin menyusun children-nya dalam satu kolom dan memungkinkan untuk melakukan *scrolling* jika terlalu panjang |
| Stack         | Digunakan ketika ingin menyusun children-nya secara bertumpuk sehingga memungkinkan suatu widget berada di atas widget lain |
| Card          | Digunakan ketika ingin membungkus suatu widget yang memiliki children sebagai satu unit dalam bentuk box atau kartu |
| ListTile      | Untuk membuat suatu *row widget* yang menyediakan elemen, seperti title, subtitle, leading icon, dan trailing icon. Dapat digunakan untuk membuat suatu item yang memiliki informasi tentang gambar, nama item, dan deskripsi singkat dari item tersebut |
| Row           | Untuk menyusun children-nya dalam satu baris. Dapat digunakan untuk menyusun *widgets* secara horizontal |
| Column        | Untuk menyusun children-nya dalam satu kolom. Dapat digunakan untuk menyusun *widgets* secara vertikal |
| Expanded      | Untuk membuat suatu *widget* memperluas dirinya untuk mengisi ruang yang tersisa pada *widget* induk |
   
### Elemen input yang digunakan pada form
1. `Form`, untuk meletakkan elemen-elemen input lain dan melakukan validasi terhadap elemen input tersebut.
2. `TextFormField`, untuk menerima input berupa teks. Digunakan untuk mengambil input nama, jumlah, dan deskripsi item.

### Penerapan *Clean Architecture* pada Flutter
Penerapan *clean architecture* dapat dilakukan dengan melakukan pemisahan terhadap kode secara terstruktur sehingga dapat dilakukan pengujian setiap bagian secara terpisah. Hal ini dapat dilakukan salah satunya dengan memisahkan struktur folder-folder pada aplikasi, seperti folder screens, widgets, dan lain-lain.

### Implementasi Checklist Tugas 8
1. Membuat file baru dengan nama `inventory_manager_form.dart` untuk membuat halaman form.
2. Isi file tersbut dengan kode berikut.
   ```dart
   import 'package:flutter/material.dart';
   class ShopFormPage extends StatefulWidget {
       const ShopFormPage({super.key});
   
       @override
       State<ShopFormPage> createState() => _ShopFormPageState();
   }
   
   class _ShopFormPageState extends State<ShopFormPage> {
       @override
       Widget build(BuildContext context) {
           return Scaffold(
              appBar: AppBar(
                title: const Center(
                  child: Text(
                    'Form Tambah Produk',
                  ),
                ),
                backgroundColor: Colors.indigo,
                foregroundColor: Colors.white,
              ),
              body: Form(
                child: SingleChildScrollView(),
              ),
            );
         }
      }
   ```
3. Menambahkan variabel `_formKey` pada class state milik widget yang berfungsi sebagai state dari form tersebut, memvalidasi form, dan untuk proses penyimpanan form.
   ```dart
   class _ShopFormPageState extends State<ShopFormPage> {
    final _formKey = GlobalKey<FormState>();
   ```
   ```dart
   body: Form(
     key: _formKey,
     child: SingleChildScrollView(),
   ),
   ```
4. Menambahkan *field* name, amount, dan description. Lalu, membuat variabel `_name`, `_amount`, dan `_description` untuk menyimpan input untuk masing-masing *field.*
   ```dart
   class _ShopFormPageState extends State<ShopFormPage> {
     final _formKey = GlobalKey<FormState>();
     String _name = "";
     int _amount = 0;
     String _description = "";
     ...
   ```
5. Membuat 3 `TextFormField` yang dibungkung di dalam `column` dan ditempatkan sebagai child dari `SingleChildScrollView` untuk menampilkan tempat untuk menerima input. Lalu, menambahkan button yang dibungkus dengan widget `Align` dan `Padding`.
   ```dart
   child: Column(
         crossAxisAlignment: CrossAxisAlignment.start,
         children: [
           Padding(
             padding: const EdgeInsets.all(8.0),
             child: TextFormField(
               decoration: InputDecoration(
                 hintText: "Nama Item",
                 labelText: "Nama Item",
                 border: OutlineInputBorder(
                   borderRadius: BorderRadius.circular(5.0),
                 ),
               ),
               onChanged: (String? value) {
                 setState(() {
                   _name = value!;
                 });
               },
               validator: (String? value) {
                 if (value == null || value.isEmpty) {
                   return "Nama tidak boleh kosong!";
                 }
                 return null;
               },
             ),
           ),
           Padding(
             padding: const EdgeInsets.all(8.0),
             child: TextFormField(
               decoration: InputDecoration(
                 hintText: "Jumlah",
                 labelText: "Jumlah",
                 border: OutlineInputBorder(
                   borderRadius: BorderRadius.circular(5.0),
                 ),
               ),
               onChanged: (String? value) {
                 setState(() {
                   _amount = int.parse(value!);
                 });
               },
               validator: (String? value) {
                 if (value == null || value.isEmpty) {
                   return "Jumlah tidak boleh kosong!";
                 }
                 if (int.tryParse(value) == null) {
                   return "Jumlah harus berupa angka!";
                 }
                 return null;
               },
             ),
           ),
           Padding(
             padding: const EdgeInsets.all(8.0),
             child: TextFormField(
               decoration: InputDecoration(
                 hintText: "Deskripsi item",
                 labelText: "Deskripsi item",
                 border: OutlineInputBorder(
                   borderRadius: BorderRadius.circular(5.0),
                 ),
               ),
               onChanged: (String? value) {
                 setState(() {
                   _description = value!;
                 });
               },
               validator: (String? value) {
                 if (value == null || value.isEmpty) {
                   return "Deskripsi item tidak boleh kosong!";
                 }
                 return null;
               },
             ),
           ),
           Align(
             alignment: Alignment.bottomCenter,
             child: Padding(
               padding: const EdgeInsets.all(8.0),
               child: ElevatedButton(
                 style: ButtonStyle(
                   backgroundColor:
                       MaterialStateProperty.all(Color(0xFF0E2954)),
                 ),
                 onPressed: () {
                   if (_formKey.currentState!.validate()) {
                     showDialog(
                       context: context,
                       builder: (context) {
                         return AlertDialog(
                           title: const Text('Item berhasil tersimpan'),
                           content: SingleChildScrollView(
                             child: Column(
                               crossAxisAlignment:
                                   CrossAxisAlignment.start,
                               children: [
                                 Text('Name: $_name'),
                                 Text('Amount: $_amount'),
                                 Text('Description: $_description'),
                               ],
                             ),
                           ),
                           actions: [
                             TextButton(
                               child: const Text('OK'),
                               onPressed: () {
                                 Navigator.pop(context);
                               },
                             ),
                           ],
                         );
                       },
                     );
                   }
                   _formKey.currentState!.reset();
                 },
                 child: const Text(
                   "Save",
                   style: TextStyle(color: Colors.white),
                 ),
               ),
             ),
           ),
         ]  
       ),
     ),
   ```
6. Pada widget ItemCard, tambahkan kode berikut untuk melakukan navigasi ke halaman form jika tombol `Tambah Item` di klik.
   ```dart
   onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
          // Navigate ke route yang sesuai (tergantung jenis tombol)
          if (item.name == "Tambah Item") {
            Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ShopFormPage()));
          }
        },
   ```
7. Menambahkan fungsi `showDialog()` pada bagian `inPressed()` pada button save untuk memunculkan widget `AlertDialog` yang berisi informasi terkait item yang berhasil di save.
   ```dart
   onPressed: () {
       if (_formKey.currentState!.validate()) {
         showDialog(
           context: context,
           builder: (context) {
             return AlertDialog(
               title: const Text('Item berhasil tersimpan'),
               content: SingleChildScrollView(
                 child: Column(
                   crossAxisAlignment:
                       CrossAxisAlignment.start,
                   children: [
                     Text('Name: $_name'),
                     Text('Amount: $_amount'),
                     Text('Description: $_description'),
                   ],
                 ),
               ),
               actions: [
                 TextButton(
                   child: const Text('OK'),
                   onPressed: () {
                     Navigator.pop(context);
                   },
                 ),
               ],
             );
           },
         );
       }
       _formKey.currentState!.reset();
     },
   ```
8. Buat file baru dengan nama `left_drawer.dart` untuk membuat suatu drawer.
9. Tambahkan import berikut.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:inventory_manager/screens/menu.dart';
    import 'package:inventory_manager/screens/inventory_manager_form.dart';
    ```
10. Melakukan *routing* untuk pergi ke halaman-halaman yang sudah di import dan menambahkan style untuk menghias drawer.
    ```dart
    class LeftDrawer extends StatelessWidget {
        const LeftDrawer({super.key});
      
        @override
        Widget build(BuildContext context) {
          return Drawer(
            child: ListView(
              children: [
                const DrawerHeader(
                  decoration: BoxDecoration(
                    color: Color(0xFF0E2954),
                  ),
                  child: Column(
                    children: [
                      Text(
                        'Inventory Manager',
                        textAlign: TextAlign.center,
                        style: TextStyle(
                          fontSize: 30,
                          fontWeight: FontWeight.bold,
                          color: Colors.white,
                        ),
                      ),
                      Padding(padding: EdgeInsets.all(10)),
                      Text("Simpan semua item yang kamu miliki di sini!",
                          textAlign: TextAlign.center,
                          style: TextStyle(
                            fontSize: 15,
                            fontWeight: FontWeight.normal,
                            color: Colors.white,
                          )
                          ),
                    ],
                  ),
                ),  
                ListTile(
                  leading: const Icon(Icons.home_outlined),
                  title: const Text('Halaman Utama'),
                  // Bagian redirection ke MyHomePage
                  onTap: () {
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(
                          builder: (context) => MyHomePage(),
                        ));
                  },
                ),
                ListTile(
                  leading: const Icon(Icons.add_shopping_cart),
                  title: const Text('Tambah Item'),
                  // Bagian redirection ke ShopFormPage
                  onTap: () {
                    Navigator.push(context,
                    MaterialPageRoute(builder: (context) => const ShopFormPage()));
                  },
                ),
              ],
            ),
          );
        }
      }
11. Setelah selesai membuat drawer, import file drawer tersebut ke `menu.dart` untuk menambahkan drawer pada halaman menu.
    ```dart
    ...
      import '../widgets/left_drawer.dart';
      ...
      return Scaffold(
        appBar: AppBar(
          backgroundColor: Color(0xFF0E2954),
          iconTheme: IconThemeData(color: Colors.white),
          title: const Text(
            'Inventory Manager',
            style: TextStyle(
              color: Colors.white,
            )
          ),
        ),
        drawer: const LeftDrawer(),
      ...
    ```

## Tugas 9: Integrasi Layanan Web Django dengan Aplikasi Flutter
### Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?
Kita bisa melakukan pengambilan data JSON tanpa membuat model terlebih dahulu. Namun, jika data yang akan kita ambil memiliki struktur yang kompleks, maka membuat model terlebih dahulu akan lebih baik dan memudahkan manajemen data. Pengambilan data JSON tanpa membuat model dapat dilakukan untuk pengambilan data yang tidak memiliki struktur yang kompleks.

### Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest berfungsi untuk mengelola permintaan HTTP terkait cookie pada aplikasi. Instance CookieRequest perlu dibagikan ke semua komponen agar terjaga konsistensi status pengguna aplikasi, konsistensi data yang perlu ditampilkan, dan agar setiap widget mempertahankan status login pengguna yang sama.

### Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
1. Menambahkan dependensi `http` ke proyek agar dapat bertukar HTTP request.
2. Membuat model yang sesuai dengan data yang akan diambil.
3. Membuat HTTP request ke web service dengan menggunakan dependensi `http`.
   ```dart
   var url = Uri.parse(
        'https://muhammad-nabiel21-tugas.pbp.cs.ui.ac.id/json/');
    var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
    );
   ```
5. Men-Decode dan mengonversikan data JSON yang didapat ke model yang sudah dibuat sebelumnya.
   ```dart
   // melakukan decode response menjadi bentuk json
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // melakukan konversi data json menjadi object Item
    List<Item> list_product = [];
    for (var d in data) {
        if (d != null) {
            list_product.add(Item.fromJson(d));
        }
    }
   ```
6. Menampilkan data yang telah dikonversi ke aplikasi dengan FutureBuilder.

### Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
1. Pengguna memasukkan input *username* dan *password* pada field input halaman login.
2. Aplikasi membuat permintaan HTTP request ke halaman *endpoint login* aplikasi Django dengan mengirimkan data input *username* dan *password* pada bagian *body request*-nya.
3. Aplikasi Django memproses permintaan tersebut dan melakukan verifikasi *username* dan *password*. Lalu, Django mengirim response dari hasil verifikasi tersebut ke aplikasi flutter. Jika verifikasi berhasil, aplikasi Flutter akan dinavigasi ke halaman `MyHomePage`.

### Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.
1. `Provider`, untuk membagikan objek ke widget dibawahnya pada widget tree, pada tugas ini yang dibagikan adalah instance CookieRequest.
2. `TextField`, untuk memungkinkan pengguna meng-input teks.
3. `ElevatedButton`, untuk menampilkan button dengan tampilan yang lebih tinggi.
4. `FutureBuilder`, untuk memungkinkan memproses data dari Future dan membuat widget berdasarkan data tersebut.
5. `Listview.builder`, untuk membuat widget yang berisi daftar item.
6. `Text`, untuk menampilkan teks.
7. `SizedBox`, untuk mengatur ukuran atau jarak pada widget.
8. `InputDecoration`, untuk mendefinisikan tampilan pada `TextField`.
9. `AlertDialog`, untuk menampilkan informasi dalam bentuk modal dialog.
10. `TextButton`, untuk menampilkan teks yang dapat diklik.
11. `MaterialPageRoute`, untuk menambahkan efek transisi ketika berpindah halaman.
12. `CircularProgressIndicator`, untuk menampilkan indikator loading.
13. `LoginPage`, untuk menampilkan halaman login.
14. `ItemPage`, untuk menampilkan halaman daftar item.

### Implementasi Checklist Tugas 9
1. Untuk memastikan *deployment* proyek tugas Django telah berjalan dengan baik, lakukan *deployment* ulang.
2. Untuk membuat halaman login, buat terlebih dahulu app baru dengan nama `authentication` dengan command `python manage.py startapp authentication`.
3. Tambahkan `authentication` ke `INSTALLED APPS` di `settings.py` proyek utama.
4. Jalankan command `pip install django-cors-headers` untuk menginstall library yang akan digunakan.
5. Tambahkan `corsheaders` ke `INSTALLED APPS` di `settings.py` proyek utama, tambahkan `corsheaders.middleware.CorsMiddleware` ke `MIDDLEWARE`, dan tambahkan variabel berikut.
   ```python
   CORS_ALLOW_ALL_ORIGINS = True
   CORS_ALLOW_CREDENTIALS = True
   CSRF_COOKIE_SECURE = True
   SESSION_COOKIE_SECURE = True
   CSRF_COOKIE_SAMESITE = 'None'
   SESSION_COOKIE_SAMESITE = 'None'
   ```
6. Membuat method untuk login dan logout pada `authentication/views.py`.
   ```python
   from django.shortcuts import render
   from django.contrib.auth import authenticate, login as auth_login
   from django.contrib.auth import logout as auth_logout
   from django.http import JsonResponse
   from django.views.decorators.csrf import csrf_exempt
   
   @csrf_exempt
   def login(request):
       username = request.POST['username']
       password = request.POST['password']
       user = authenticate(username=username, password=password)
       if user is not None:
           if user.is_active:
               auth_login(request, user)
               # Status login sukses.
               return JsonResponse({
                   "username": user.username,
                   "status": True,
                   "message": "Login sukses!"
                   # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
               }, status=200)
           else:
               return JsonResponse({
                   "status": False,
                   "message": "Login gagal, akun dinonaktifkan."
               }, status=401)

       else:
           return JsonResponse({
               "status": False,
               "message": "Login gagal, periksa kembali email atau kata sandi."
           }, status=401)
   @csrf_exempt
   def logout(request):
       username = request.user.username
   
       try:
           auth_logout(request)
           return JsonResponse({
               "username": username,
               "status": True,
               "message": "Logout berhasil!"
           }, status=200)
       except:
           return JsonResponse({
           "status": False,
           "message": "Logout gagal."
           }, status=401)
   ```
7. Buat file `authentication/urls.py` dan tambahkkan *routing* untuk kedua fungsi tersebut.
   ```python
   from django.urls import path
   from authentication.views import login, logout
   
   app_name = 'authentication'
   
   urlpatterns = [
       path('login/', login, name='login'),
       path('logout/', logout, name='logout'),
   ]
   ```
8. Tambakan `path('auth/', include('authentication.urls')),` pada `inventory_manager/urls.py`
9. Untuk melakukan integrasi sistem autentikasi dengan flutter, install pakcage berikut pada direktori proyek flutter.
    ```
    flutter pub add provider
    flutter pub add pbp_django_auth
    ```
10. Ubah root widget pada `myApp` menjadi seperti berikut untuk menambahkan objek Provider sehingga dapat memberikan `CookieRequest` ke semua komponen aplikasi.
    ```dart
    // This widget is the root of your application.
     @override
     Widget build(BuildContext context) {
       return Provider(
         create: (_) {
                   CookieRequest request = CookieRequest();
                   return request;
               },
   
         child: MaterialApp(
           title: 'Flutter Demo',
           theme: ThemeData(
             colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
             useMaterial3: true,
           ),
           home: LoginPage(),
         )
       );
     }
    ```
11. Buat file baru `screens/login.dart`
    ```dart
      import 'package:inventory_manager/screens/menu.dart';
      import 'package:flutter/material.dart';
      import 'package:pbp_django_auth/pbp_django_auth.dart';
      import 'package:provider/provider.dart';
      
      void main() {
          runApp(const LoginApp());
      }
      
      class LoginApp extends StatelessWidget {
      const LoginApp({super.key});
      
      @override
      Widget build(BuildContext context) {
          return MaterialApp(
              title: 'Login',
              theme: ThemeData(
                  primarySwatch: Colors.blue,
          ),
          home: const LoginPage(),
          );
          }
      }
      
      class LoginPage extends StatefulWidget {
          const LoginPage({super.key});
      
          @override
          _LoginPageState createState() => _LoginPageState();
      }
      
      class _LoginPageState extends State<LoginPage> {
          final TextEditingController _usernameController = TextEditingController();
          final TextEditingController _passwordController = TextEditingController();
      
          @override
          Widget build(BuildContext context) {
              final request = context.watch<CookieRequest>();
              return Scaffold(
                  appBar: AppBar(
                      title: const Text('Login'),
                  ),
                  body: Container(
                      padding: const EdgeInsets.all(16.0),
                      child: Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          children: [
                              TextField(
                                  controller: _usernameController,
                                  decoration: const InputDecoration(
                                      labelText: 'Username',
                                  ),
                              ),
                              const SizedBox(height: 12.0),
                              TextField(
                                  controller: _passwordController,
                                  decoration: const InputDecoration(
                                      labelText: 'Password',
                                  ),
                                  obscureText: true,
                              ),
                              const SizedBox(height: 24.0),
                              ElevatedButton(
                                  onPressed: () async {
                                      String username = _usernameController.text;
                                      String password = _passwordController.text;
    
                                      final response = await request.login("https://muhammad-nabiel21-tugas.pbp.cs.ui.ac.id/auth/login/", {
                                      'username': username,
                                      'password': password,
                                      });
                          
                                      if (request.loggedIn) {
                                          String message = response['message'];
                                          String uname = response['username'];
                                          Navigator.pushReplacement(
                                              context,
                                              MaterialPageRoute(builder: (context) => MyHomePage()),
                                          );
                                          ScaffoldMessenger.of(context)
                                              ..hideCurrentSnackBar()
                                              ..showSnackBar(
                                                  SnackBar(content: Text("$message Selamat datang, $uname.")));
                                          } else {
                                          showDialog(
                                              context: context,
                                              builder: (context) => AlertDialog(
                                                  title: const Text('Login Gagal'),
                                                  content:
                                                      Text(response['message']),
                                                  actions: [
                                                      TextButton(
                                                          child: const Text('OK'),
                                                          onPressed: () {
                                                              Navigator.pop(context);
                                                          },
                                                      ),
                                                  ],
                                              ),
                                          );
                                      }
                                  },
                                  child: const Text('Login'),
                              ),
                          ],
                      ),
                  ),
              );
          }
      }
    ```
12. Pada file `main.dart`, ubah `home: MyHomePage(),` menjadi `home: LoginPage(),`.
13. Untuk membuat model kustom, buka *endpoint* json pada aplikasi django, lalu salin semua datanya.
14. Setelah itu, pergi ke [Quicktype](https://app.quicktype.io/). Lalu, salin smeua data tersebut ke bagian text, ubah `Name` menjadi `Item`, source type menjadi `JSON`, dan language `Dart`.
15. Klik `Copy Code`, lalu buat file baru pada `lib/models/item.dart` dan tempel salinan kodenya pada file tersebut.
16. Untuk melakukan perintah HTTP request, jalankan command `flutter pub add http`.
17. Pada file `android/app/src/main/AndroidManifest.xml`, tambahkan baris kode berikut.
    ```xml
    ...
     </application>
    
    <!-- Required to fetch data from the Internet. -->
    <uses-permission android:name="android.permission.INTERNET" />
    ```
18. Buat file baru dengan nama `list_item.dart` pada `lib/screens`, isi dengan kode berikut.
    ```dart
      import 'package:flutter/material.dart';
      import 'package:http/http.dart' as http;
      import 'dart:convert';
      import 'package:inventory_manager/models/item.dart';
      import 'package:inventory_manager/widgets/left_drawer.dart';
      
      class ItemPage extends StatefulWidget {
          const ItemPage({Key? key}) : super(key: key);
      
          @override
          _ItemPageState createState() => _ItemPageState();
      }
      
      class _ItemPageState extends State<ItemPage> {
      Future<List<Item>> fetchItem() async {
          var url = Uri.parse(
              'https://muhammad-nabiel21-tugas.pbp.cs.ui.ac.id/json/');
          var response = await http.get(
              url,
              headers: {"Content-Type": "application/json"},
          );
      
          // melakukan decode response menjadi bentuk json
          var data = jsonDecode(utf8.decode(response.bodyBytes));
      
          // melakukan konversi data json menjadi object Item
          List<Item> list_product = [];
          for (var d in data) {
              if (d != null) {
                  list_product.add(Item.fromJson(d));
              }
          }
          return list_product;
      }
      
      @override
      Widget build(BuildContext context) {
          return Scaffold(
              appBar: AppBar(
              title: const Text('Product'),
              ),
              drawer: const LeftDrawer(),
              body: FutureBuilder(
                  future: fetchItem(),
                  builder: (context, AsyncSnapshot snapshot) {
                      if (snapshot.data == null) {
                          return const Center(child: CircularProgressIndicator());
                      } else {
                          if (!snapshot.hasData) {
                          return const Column(
                              children: [
                              Text(
                                  "Tidak ada data produk.",
                                  style:
                                      TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                              ),
                              SizedBox(height: 8),
                              ],
                          );
                      } else {
                          return ListView.builder(
                              itemCount: snapshot.data!.length,
                              itemBuilder: (_, index) => Container(
                                      margin: const EdgeInsets.symmetric(
                                          horizontal: 16, vertical: 12),
                                      padding: const EdgeInsets.all(20.0),
                                      child: Column(
                                      mainAxisAlignment: MainAxisAlignment.start,
                                      crossAxisAlignment: CrossAxisAlignment.start,
                                      children: [
                                          Text(
                                          "${snapshot.data![index].fields.name}",
                                          style: const TextStyle(
                                              fontSize: 18.0,
                                              fontWeight: FontWeight.bold,
                                          ),
                                          ),
                                          const SizedBox(height: 10),
                                          Text("${snapshot.data![index].fields.price}"),
                                          const SizedBox(height: 10),
                                          Text(
                                              "${snapshot.data![index].fields.description}")
                                      ],
                                      ),
                                  ));
                          }
                      }
                  }));
          }
      }
    ```
19. Tambahkan halaman `list_item` pada drawer di `widgets/left_drawer.dart`
    ```dart
    ...
    ListTile(
            leading: const Icon(Icons.shopping_basket),
            title: const Text('Daftar Item'),
            onTap: () {
              // Route menu ke halaman item
              Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => const ItemPage()),);
            },
          ),
    ```
20. Tambahkan baris `else if` baru di `widgets/item_card.dart` untuk me-*redirect* ke halaman `ItemPage`.
    ```dart
    ...
    else if (item.name == "Lihat Item") {
            Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ItemPage()));
    ```
21. *Handle error* dengan melakukan *Quick fix* di tiap baris kode untuk menambahkan import yang dibutuhkan.
22. Untuk mengintegrasi form flutter dengan django, buat fungsi baru pada proyek django di `main/views.py` dengan kode berikut.
    ```python
      @csrf_exempt
      def create_item_flutter(request):
          if request.method == 'POST':
              
              data = json.loads(request.body)
      
              new_item = Item.objects.create(
                  user = request.user,
                  name = data["name"],
                  amount = int(data["amount"]),
                  description = data["description"]
              )
      
              new_item.save()
      
              return JsonResponse({"status": "success"}, status=200)
          else:
              return JsonResponse({"status": "error"}, status=401)
    ```
23. Import fungsi tersebut ke `urls.py` dan tambahkan *routing* ke fungsi tersebut.
    ```python
    from main.views. import ..., create_item_flutter

    ...
       path('create-flutter/', create_item_flutter, name='create_item_flutter'),
    ]
    ```
24. Hubungkan halaman `inventory_manager_form.dart` dengan `CookieRequest` dengan menambahkan kode berikut.
    ```dart
      ...
      @override
      Widget build(BuildContext context) {
          final request = context.watch<CookieRequest>();
      
          return Scaffold(
      ...
    ```
25. Ubah perintah `OnPressed()`-nya menjadi seperti berikut.
    ```dart
    ...
    onPressed: () async {
          if (_formKey.currentState!.validate()) {
            // Kirim ke Django dan tunggu respons
            // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
            final response = await request.postJson(
            "https://muhammad-nabiel21-tugas.pbp.cs.ui.ac.id/create-flutter/",
            jsonEncode(<String, String>{
                'name': _name,
                'amount': _amount.toString(),
                'description': _description,
            }));
            if (response['status'] == 'success') {
                ScaffoldMessenger.of(context)
                    .showSnackBar(const SnackBar(
                content: Text("Produk baru berhasil disimpan!"),
                ));
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => MyHomePage()),
                );
            } else {
                ScaffoldMessenger.of(context)
                    .showSnackBar(const SnackBar(
                    content:
                        Text("Terdapat kesalahan, silakan coba lagi."),
                ));
            }
    }
    ```
26. Untuk implementasi logout, tambahkan baris kode berikut ke `lib/widgets/item_card.dart`.
    ```dart
      ...
      @override
      Widget build(BuildContext context) {
          final request = context.watch<CookieRequest>();
          return Material(
      ...
    ```
27. Ubah `OnTap() {...}` pada eidget `InkWell` menjadi `OnTap() async {...}` dan tambahkan baris `else if` bari lagi dengan kode berikut.
    ```dart
    else if (item.name == "Logout") {
      final response = await request.logout(
          "https://muhammad-nabiel21-tugas.pbp.cs.ui.ac.id/auth/logout/");
      String message = response["message"];
      if (response['status']) {
        String uname = response["username"];
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(
          content: Text("$message Sampai jumpa, $uname."),
        ));
        Navigator.pushReplacement(
          context,
          MaterialPageRoute(builder: (context) => const LoginPage()),
        );
      } else {
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(
          content: Text("$message"),
        ));
      }
    }
    ```
