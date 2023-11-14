# DVNTORY (Mobile)
Devin Faiz Faturahman 2206830593 PBP E

# Tugas 7
## Membuat sebuah program Flutter baru dengan tema inventory
1. Buka command prompt, navigasi ke direktori tempat Anda ingin menyimpan aplikasi, kemudian buat proyek flutter baru dengan menjalankan `flutter create dvntory_mobile` dan masuk ke direktori tersebut.

2. Dalam direktori `dvntory_mobile/lib`, tambahkan file baru `menu.dart`.

3. Di awal `menu.dart`, tambahkan `import 'package:flutter/material.dart';` dan pindahkan class berikut dari file `main.dart` ke dalam `menu.dart`

``` dart
class MyHomePage ... {
    ...
}

class _MyHomePageState ... {
    ...
}
```

4. Dalam `main.dart`, tambahkan baris `import 'package:dvntory_mobile/menu.dart';` untuk memasukkan fungsi-fungsi dari `menu.dart` sehingga menghindari error.

## Membuat tiga tombol sederhana dengan ikon dan teks dan memunculkan Snackbar dengan tulisan ketika ditekan tombolnya
1. Pada `main.dart`, ganti `MyHomePage(title: 'Flutter Demo Home Page')` menjadi `home: MyHomePage()`.

2. Modifikasi `menu.dart` pada `class MyHomePage()` dari widget yang memiliki state ke widget tanpa state, dan ubah isinya seperti berikut. lalu jangan lupa untuk hapus fungsi State yang ada dibawah bagian stateless widget ini.
```dart
class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            ...
        );
    }
}
```

3. Tambahkan class berikut sebagai atribut dalam aplikasi kita
```dart
class InvItem {
  final String name; // Nama item
  final IconData icon; // Icon yang digunakan
  final Color color; // Warna background
  InvItem(this.name, this.icon, this.color); // Constructor
}
```

4. Dalam `menu.dart` pada `class MyHomePage extends StatelessWidget`, tambahkan kode berikut di bawah `MyHomePage({Key? key}) : super(key: key);` untuk mendefinisikan tombol yang ingin ditambahkan
```dart
...
final List<InvItem> items = [
    InvItem("Lihat Item", Icons.checklist, Colors.green),
    InvItem("Tambah Item", Icons.add_shopping_cart, Colors.blue),
    InvItem("Logout", Icons.logout, Colors.red),
    ];
...
```

5. Pada class yang sama, ubah function `Widget build` menjadi seperti berikut
```dart
...
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // AppBar dengan background color dan judul
      appBar: AppBar(
        backgroundColor: const Color.fromARGB(255, 28, 56, 121),
        title: const Text(
          'Dvntory',
          style: TextStyle(color: Color.fromARGB(255, 255, 255, 255)),
        ),
      ),
      // Body aplikasi yang scrollable
      body: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Padding disekitar column
          child: Column(
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                child: Text(
                  'Main Menu',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // GridView untuk menampilkan item-item secara grid
              GridView.count(
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true, // Mengontrol apakah children harus shrink ke ukuran mereka di cross axis
                children: items.map((InvItem item) {
                  // Mapping dari list item ke widget InvCard
                  return InvCard(item);
                }).toList(), // Konversi kembali ke list setelah mapping
              ),
            ],
          ),
        ),
      ),
    );
  }
...
```

6. Definisikan function baru untuk tombol/kartu yang ditambahkan
```dart
class InvCard extends StatelessWidget {
  final InvItem item; // Item inventaris yang diterima

  const InvCard(this.item, {super.key}); // Constructor dengan super.key

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color, // Warna background dari card
      child: InkWell(
        onTap: () {
          // Handler ketika card diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!"))); // Menampilkan SnackBar
        },
        child: Container(
          padding: const EdgeInsets.all(8), // Padding disekitar content dalam card
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center, // Center content secara vertikal
              children: [
                Icon(
                  item.icon, // Icon dari item
                  color: Colors.white,
                  size: 40.0,
                ),
                const Padding(padding: EdgeInsets.all(3)), // Memberikan space antar elemen
                Text(
                  item.name, // Nama item
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white), // Style text
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

## Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?
Perbedaan utama antara Stateless dan Stateful widget dalam Flutter adalah:

- **Stateless Widget**: Ini adalah widget yang tidak memerlukan state yang dapat berubah selama waktu hidup widget. Stateless widget tidak dapat memperbarui dirinya sendiri kecuali data eksternal yang diberikan kepada mereka berubah. Mereka digunakan untuk UI yang tetap konstan sepanjang waktu hidupnya atau UI yang hanya berubah ketika widget parentnya memberikan data baru kepadanya. Contoh: `Text`, `Icon`, dan `FlatButton`.

- **Stateful Widget**: Ini adalah widget yang dapat mempertahankan state dan oleh karena itu dapat berubah berdasarkan interaksi pengguna atau data internal. Stateful widget memiliki `State` yang dapat diperbarui untuk memicu pembangunan ulang widget tersebut dengan UI yang diperbarui. Ini berguna untuk widget yang interaktif seperti formulir, atau widget yang harus memperbarui tampilannya sebagai respons terhadap perubahan dalam data atau preferensi pengguna. Contoh: `Checkbox`, `Slider`, dan `TextField`.

Jika UI berubah dinamis (misalnya, berubah dengan interaksi pengguna), gunakan Stateful widget. Jika UI hanya bergantung pada informasi yang diberikan dan tidak berubah seiring waktu, gunakan Stateless widget.

## Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing
- `MaterialApp`: Widget yang membungkus sejumlah widget lain untuk memungkinkan pengembangan aplikasi dengan material design. Ini juga menangani navigasi dan tema pada aplikasi.

- `ThemeData`: Mengatur tema global untuk aplikasi, yang mencakup skema warna, jenis font, dan ukuran font yang digunakan oleh widget material lainnya dalam aplikasi.

- `Scaffold`: Menyediakan kerangka dasar untuk layout dengan struktur aplikasi mobile yang khas, termasuk AppBar, Body, dan Floating Action Button.

- `AppBar`: Widget yang ditampilkan di bagian atas Scaffold, umumnya menampilkan judul aplikasi dan aksi.

- `SingleChildScrollView`: Sebuah widget yang memungkinkan pengguna untuk scroll pada konten yang lebih besar daripada ruang tampilan yang tersedia.

- `Padding`: Menambahkan ruang kosong di sekitar widget lain untuk memberi ruang dalam layout.

- `Column`: Mengatur widget anak secara vertikal.

- `GridView.count`: Membentuk grid dengan jumlah kolom tetap dan menata widget anak di dalamnya.

- `Material`: Widget yang mengikuti prinsip material design, biasanya digunakan untuk efek visual seperti ripple saat widget di dalamnya ditekan.

- `InkWell`: Widget yang merespons ketukan dengan efek visual gelombang tinta dan memungkinkan aksi saat ditekan.

- `Container`: Widget yang sering digunakan untuk mendekorasi child widgetnya, seperti dengan padding, margin, atau constraints.

- `Icon`: Menampilkan ikon dari kumpulan ikon yang ditentukan.

- `Text`: Menampilkan teks dengan berbagai opsi styling.

- `ScaffoldMessenger`: Widget yang digunakan untuk menampilkan SnackBar, yaitu pesan ringkas di bagian bawah layar.

- `SnackBar`: Widget yang menampilkan pesan ringkas yang muncul dari bawah layar.

# Tugas 8
## Membuat Halaman Formulir Penambahan Item Baru
1. Buatlah file baru dengan nama "dvntory_form.dart" di dalam proyek Flutter Anda dan tambahkan baris import untuk material.dart dan left_drawer.dart di file "dvntory_form.dart" tersebut.

2. Buatlah sebuah widget yang bernama "ItemFormPage" sebagai StatefulWidget yang berisi sebuah formulir. Gunakan widget Scaffold dan tambahkan app bar dengan judul `"Tambahkan Item Anda"`. Sesuaikan warna background dan warna teks sesuai dengan keinginan Anda.

```dart
import 'package:flutter/material.dart';
import 'package:dvntory_mobile/widgets/left_drawer.dart';
import 'package:dvntory_mobile/widgets/dvntory_card.dart';

class ItemFormPage extends StatefulWidget {
  const ItemFormPage({super.key});

  @override
  State<ItemFormPage> createState() => _ItemFormPageState();
}

List<Item> items = [];

class _ItemFormPageState extends State<ItemFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  int _price = 0;
  String _description = "";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Tambahkan Item Anda'),
        backgroundColor: const Color.fromARGB(255, 28, 56, 121),
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        // ... Isi formulir di sini
      ),
    );
  }
}
```

3. Dalam formulir, tambahkan elemen-elemen input seperti `Name`, `Amount`, `Price`, dan `Description`. Gunakan TextFormField dan atur dekorasinya sesuai keinginan. Tambahkan validasi pada setiap elemen input agar tidak boleh kosong dan harus sesuai dengan tipe data yang diinginkan.
```dart
...
body: Form(
  key: _formKey,
  child: SingleChildScrollView(
    child: Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: TextFormField(
            decoration: InputDecoration(
              hintText: "Nama",
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
                _amount = int.tryParse(value!) ?? 0;
              });
            },
            validator: (String? value) {
              if (value == null || value.isEmpty) {
                return "Jumlah tidak boleh kosong!";
              }
              if (int.tryParse(value) == null) {
                return "Jumlah harus berupa angka yang valid!";
              }
              return null;
            },
          ),
        ),
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: TextFormField(
            decoration: InputDecoration(
              hintText: "Harga",
              labelText: "Harga",
              border: OutlineInputBorder(
                borderRadius: BorderRadius.circular(5.0),
              ),
            ),
            onChanged: (String? value) {
              setState(() {
                _price = int.tryParse(value!) ?? 0;
              });
            },
            validator: (String? value) {
              if (value == null || value.isEmpty) {
                return "Harga tidak boleh kosong!";
              }
              if (int.tryParse(value) == null) {
                return "Harga harus berupa angka yang valid!";
              }
              return null;
            },
          ),
        ),
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: TextFormField(
            decoration: InputDecoration(
              hintText: "Deskripsi",
              labelText: "Deskripsi",
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
                return "Deskripsi tidak boleh kosong!";
              }
              return null;
            },
          ),
        ),
      ],
    ),
  ),
),
...
```

4. Tambahkan tombol "Save" di bagian bawah halaman formulir dan pop-up konfirmasi yang muncul setelah tombol "Save" ditekan, yang akan menampilkan detail item yang ditambahkan.
```dart
Padding(
  padding: const EdgeInsets.all(8.0),
  child: ElevatedButton(
    style: ButtonStyle(
      backgroundColor: MaterialStateProperty.all(const Color.fromARGB(255, 67, 179, 70)),
    ),
    onPressed: () {
      if (_formKey.currentState!.validate()) {
        items.add(Item(
          name: _name,
          price: _price,
          description: _description,
          amount: _amount,
        ));
        showDialog(
          context: context,
          builder: (context) {
            return AlertDialog(
              title: const Text('Item Berhasil Disimpan'),
              content: SingleChildScrollView(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: <Widget>[
                    Text('Nama: $_name'),
                    Text('Harga: $_price'),
                    Text('Jumlah: $_amount'),
                    Text('Deskripsi: $_description'),
                  ],
                ),
              ),
              actions: <Widget>[
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
        _formKey.currentState!.reset();
      }
    },
    child: const Text(
      "Save",
      style: TextStyle(color: Colors.white),
    ),
  ),
),
...
```

## Membuat Drawer Menu
1. Buatlah widget drawer di folder terpisah bernama `widgets` dan dalam file bernama `left_drawer.dart`. Drawer ini akan berisi opsi-opsi menu navigasi. Pastikan untuk melakukan `import material.dart` di dalam file tersebut.

2. Buatlah widget yang bernama "LeftDrawer" sebagai StatelessWidget dengan isi drawer. Gunakan ListView untuk menampilkan opsi-opsi menu.
```dart
import 'package:flutter/material.dart';
import 'package:dvntory_mobile/screens/menu.dart';
import 'package:dvntory_mobile/screens/dvntory_form.dart';
import 'package:dvntory_mobile/screens/dvntory_list.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          // ... Isi opsi-opsi menu di sini
        ],
      ),
    );
  }
}
```

3. Tambahkan opsi-opsi menu pada drawer, seperti "Halaman Utama" dan "Tambah Produk" dengan menggunakan ListTile dan ikon yang sesuai. Gunakan Navigator.pushReplacement() untuk melakukan navigasi ke halaman yang terkait pada setiap opsi menu.
```dart
...
ListTile(
  leading: const Icon(Icons.home_outlined),
  title: const Text('Home'),
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
  leading: const Icon(Icons.checklist),
  title: const Text('Lihat Item'),
  // Bagian redirection ke ShopFormPage
  onTap: () {
    Navigator.pushReplacement(
        context,
        MaterialPageRoute(
          builder: (context) => const ItemsPage(),
        ));
  },
),
ListTile(
  leading: const Icon(Icons.add_shopping_cart),
  title: const Text('Tambah Item'),
  // Bagian redirection ke ShopFormPage
  onTap: () {
    /*
    Routing ke ShopFormPage di sini, setelah halaman ShopFormPage sudah dibuat.
    */
    Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) => const ItemFormPage()));
  },
),
...
```

## Menggunakan Drawer pada Halaman Utama dan Halaman Formulir
1. Di halaman utama di `menu.dart`, tambahkan widget LeftDrawer ke dalam widget Scaffold. Hal ini akan memunculkan menu drawer di halaman utama.
```dart
...
return Scaffold(
  appBar: AppBar(
    centerTitle: false,
    title: const Text(
      'Dvntory',
    ),
    backgroundColor: const Color.fromARGB(255, 28, 56, 121),
    foregroundColor: Colors.white,
  ),
  drawer: const LeftDrawer(),// Tambahkan drawer ke halaman utama
  // ... Konten halaman utama
);
...
```

2. Di halaman formulir `dvntory_form.dart`, tambahkan juga widget LeftDrawer ke dalam widget Scaffold. Ini akan memunculkan menu drawer di halaman formulir.
```dart
...
return Scaffold(
  appBar: AppBar(
    title: const Text('Tambahkan Item Anda'),
    backgroundColor: const Color.fromARGB(255, 28, 56, 121),
    foregroundColor: Colors.white,
  ),
  drawer: const LeftDrawer(), // Tambahkan drawer ke halaman formulir
  // ... Konten halaman formulir
);
...
```

### Setelah melakukan semua langkah di atas, saya melakukan refactor pada struktur penyimpanan file untuk membuatnya lebih terorganisir.

## Perbedaan antara `Navigator.push()` dan `Navigator.pushReplacement()` di Flutter

- **Navigator.push()**:
  - **Fungsi**: Digunakan untuk menambahkan sebuah route (halaman) baru ke atas stack navigasi tanpa menghapus route sebelumnya.
  - **Konteks Penggunaan**: Ideal untuk situasi di mana Anda ingin mempertahankan halaman sebelumnya, seperti navigasi dari daftar item ke detail item. Pengguna bisa kembali ke halaman sebelumnya dengan tombol back.
  - **Contoh**: Dari halaman beranda ke halaman detail produk.
  ```dart
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => DetailPage()),
  );
  ```
  
- **Navigator.pushReplacement()**:
  - **Fungsi**: Menggantikan route saat ini dengan route baru di stack navigasi. Route sebelumnya dihapus.
  - **Konteks Penggunaan**: Berguna saat Anda tidak ingin pengguna kembali ke halaman sebelumnya, misalnya setelah proses login berhasil dan Anda ingin navigasi ke homepage tanpa memberi opsi kembali ke halaman login.
  - **Contoh**: Mengganti halaman login dengan halaman utama setelah login berhasil.
  ```dart
  Navigator.pushReplacement(
    context,
    MaterialPageRoute(builder: (context) => HomePage()),
  );
  ```

## Layout Widget pada Flutter dan Konteks Penggunaannya
- **Container**: Widget serbaguna untuk pembungkus, styling, dan positioning. Digunakan untuk membuat kotak dengan warna, ukuran, atau dekorasi tertentu.
- **Row dan Column**: Untuk layout linear secara horizontal (Row) dan vertikal (Column). Berguna untuk menata widget dalam satu baris atau kolom.
- **Stack**: Menumpuk widget satu di atas yang lain. Ideal untuk overlay atau positioning widget di atas widget lain.
- **ListView**: Untuk menampilkan daftar item yang bisa di-scroll. Cocok untuk daftar yang panjang atau data yang dinamis.
- **GridView**: Menampilkan item dalam grid. Digunakan untuk galeri foto atau item yang perlu ditampilkan secara grid.
- **Flex dan Expanded**: Mengatur distribusi ruang antar widget dalam Row atau Column. Expanded mengambil ruang tersedia, sementara Flex memberikan kontrol lebih terhadap proporsi ruang.

## Elemen Input pada Form yang Digunakan dan Alasannya
Dalam pembuatan form, saya memilih untuk menggunakan `TextFormField` yang disertai dengan validasi input. Alasan utama penggunaan ini adalah untuk memudahkan pengambilan data teks, seperti nama produk, jumlah, harga, dan deskripsi. Untuk memastikan keakuratan data, khusus untuk bidang jumlah dan harga, saya menerapkan validasi tambahan dengan mencoba mengkonversi input tersebut menjadi tipe data `int`. Pendekatan ini membantu dalam menjamin bahwa input untuk jumlah dan harga hanya berisi nilai int yang valid.

## Penerapan Clean Architecture pada Aplikasi Flutter
Clean Architecture adalah konsep arsitektur perangkat lunak yang memisahkan kode menjadi lapisan dengan tanggung jawab yang berbeda, meningkatkan kebersihan dan kemudahan pemeliharaan kode. Dalam konteks Flutter:

- **Presentation Layer**: Berisi UI dan logic UI. Menggunakan Widget untuk membangun UI dan mengambil data dari Bloc atau ViewModel.
- **Business Logic Layer (BLL)**: Menggunakan Bloc atau Provider untuk mengelola state dan logic aplikasi.
- **Data Layer**: Terdiri dari Repository dan Data Source. Repository bertindak sebagai mediator antara BLL dan sumber data (API, database lokal).
- **Domain Layer**: Berisi entitas dan use case. Entitas adalah model data, dan use case menentukan operasi bisnis.

Masing-masing lapisan ini harus memiliki tanggung jawab yang jelas dan terpisah untuk memudahkan testing, maintenance, dan scalability aplikasi.