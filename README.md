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

# Tugas 9
## Membuat halaman login pada proyek tugas Flutter.
Dalam pembuatan halaman login (`login.dart`), berikut adalah kode yang dibuat untuk mengisi bagian `login.dart` pada folder `screens` yang telah dikerjakan.
```dart
import 'package:dvntory_mobile/screens/menu.dart';
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

                                // Cek kredensial
                                // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                                // Untuk menyambungkan Android emulator dengan Django pada localhost,
                                // gunakan URL http://10.0.2.2/
                                final response = await request.login("http://10.0.2.2:8000/auth/login/", {
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
Di `main.dart`, rute diubah agar langsung menuju `LoginPage()` sebelum masuk ke aplikasi.

## Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.
Untuk mengintegrasikan autentikasi Django dengan Flutter, pertama-tama, di Django dibuat aplikasi `authentication` dan disiapkan `corsheaders`. Kemudian, fungsi login dibuat di `authentication/views.py` dan diatur routing-nya di `authentication/urls.py`. Di Flutter, widget akar diubah untuk menyediakan `CookieRequest` ke semua widget anak menggunakan `Provider`.

## Membuat model kustom sesuai dengan proyek aplikasi Django.
Untuk membuat model khusus yang sesuai dengan aplikasi Django, data JSON diambil dari Django melalui `Postman` di `localhost:8000/json`. Menggunakan _Quicktype_, data JSON diubah menjadi model di Flutter. Selanjutnya, dibuat `product.dart` di `lib/models` dengan kode:
```dart
import 'dart:convert';

List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class Product {
    String model;
    int pk;
    Fields fields;

    Product({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory Product.fromJson(Map<String, dynamic> json) => Product(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    String name;
    int amount;
    int price;
    String description;
    int user;

    Fields({
        required this.name,
        required this.amount,
        required this.description,
        required this.price,
        required this.user,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        name: json["name"],
        amount: json["amount"],
        price: json["price"],
        description: json["description"],
        user: json["user"],
    );

    Map<String, dynamic> toJson() => {
        "name": name,
        "amount": amount,
        "price": price,
        "description": description,
        "user": user,
    };
}
```

## Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django
Halaman yang menampilkan daftar item dari endpoint JSON Django dibuat dalam file `dvntory_list.dart`. Halaman ini menampilkan nama produk dan setiap nama produk mengarah ke `dvntory_detail.dart` untuk detail produk, dengan kode:
```dart
import 'package:dvntory_mobile/screens/dvntory_detail.dart';
import 'package:dvntory_mobile/widgets/left_drawer.dart';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:dvntory_mobile/models/product.dart';

class ProductPage extends StatefulWidget {
    const ProductPage({Key? key}) : super(key: key);

    @override
    _ProductPageState createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
Future<List<Product>> fetchProduct() async {
    // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
    var url = Uri.parse(
        'http://10.0.2.2:8000/json/');
    var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
    );

    // melakukan decode response menjadi bentuk json
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // melakukan konversi data json menjadi object Product
    List<Product> list_product = [];
    for (var d in data) {
        if (d != null) {
            list_product.add(Product.fromJson(d));
        }
    }
    return list_product;
}

@override
Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text('Item'),
          backgroundColor: const Color.fromARGB(255, 28, 56, 121),
          foregroundColor: Colors.white,
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
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
                      itemBuilder: (_, index) => InkWell(
                        onTap: () {
                          Navigator.push(
                            context,
                            MaterialPageRoute(
                              builder: (context) => DetailProductPage(
                                product: snapshot.data![index],
                              ),
                            ),
                          );
                        },
                        child: Card(
                          elevation: 3,
                          margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                          child: Padding(
                            padding: const EdgeInsets.all(16.0),
                            child: Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Text(
                                  "${snapshot.data![index].fields.name}",
                                  style: const TextStyle(
                                    fontSize: 14.0,
                                    fontWeight: FontWeight.bold,
                                  ),
                                ),
                              ],
                            ),
                          ),
                        ),
                      ),
                    );
                  }
                }
            }));
    }
}
```

## Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item.
Akhirnya, untuk menampilkan detail tiap item pada halaman daftar Item, dibuat halaman di `dvntory_detail.dart` dengan kode:
```dart
import 'package:flutter/material.dart';
import 'package:dvntory_mobile/models/product.dart';

class DetailProductPage extends StatelessWidget {
  final Product product;

  const DetailProductPage({Key? key, required this.product}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Detail Item'),
        backgroundColor: const Color.fromARGB(255, 28, 56, 121),
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              "${product.fields.name}",
              style: const TextStyle(
                fontSize: 18.0,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 16),
            Text(
              "Amount: ${product.fields.amount}",
              style: const TextStyle(
                fontSize: 14.0,
                color: Colors.grey,
              ),
            ),
            const SizedBox(height: 8),
            Text(
              "Price: ${product.fields.price}",
              style: const TextStyle(
                fontSize: 14.0,
                color: Colors.grey,
              ),
            ),
            const SizedBox(height: 8),
            Text(
              "Description: ${product.fields.description}",
              style: const TextStyle(
                fontSize: 14.0,
                color: Colors.grey,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
## Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?
Pengambilan data JSON bisa dilakukan tanpa perlu membuat model terlebih dahulu. JSON, yang dikenal sebagai format pertukaran data yang ringkas dan mudah dipahami, memungkinkan proses parsing atau penguraian untuk mengakses data yang diinginkan. Dalam kasus di mana struktur JSON sederhana, pembuatan model khusus bisa diabaikan.
Namun, dalam situasi di mana struktur JSON lebih kompleks, atau tugas-tugas seperti klasifikasi dan pengolahan bahasa alami diperlukan, disarankan untuk membuat model JSON terlebih dahulu. Model ini akan mempermudah dalam memahami dan menangani struktur serta konten data JSON yang lebih rumit.

## Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
`CookieRequest` adalah sebuah kelas yang digunakan untuk mengirim permintaan HTTP bersama dengan cookie. Saat mengirim permintaan HTTP, cookie dapat ditambahkan ke dalam permintaan dengan membuat sebuah instansi dari `CookieRequest` dan memasukkan cookie tersebut ke dalam header permintaan. Instansi `CookieRequest` ini kemudian digunakan untuk mengirim permintaan HTTP dengan cookie terlampir.

Pentingnya berbagi instansi `CookieRequest` di seluruh komponen aplikasi Flutter terletak pada fakta bahwa instansi ini memegang cookie yang dibutuhkan untuk permintaan HTTP. Jika `CookieRequest` hanya dibuat di satu komponen dan dicoba untuk digunakan di komponen lain, cookie yang relevan tidak akan tersedia. Dengan demikian, membagikan instansi `CookieRequest` ke seluruh komponen di aplikasi Flutter memastikan ketersediaan cookie di seluruh bagian aplikasi.

## Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
Untuk mengambil dan menggunakan data JSON dalam aplikasi Flutter, prosesnya dapat dibuat dalam beberapa langkah utama:

1. **Mengambil Data JSON:**
   - Gunakan perpustakaan atau metode yang cocok dalam bahasa pemrograman yang Anda gunakan untuk mengambil data JSON. Ini bisa melalui API atau dengan membaca file JSON dari sumber lokal.

2. **Parsing Data JSON:**
   - Setelah data JSON diperoleh, lakukan parsing atau penguraian data tersebut. Di Flutter, yang menggunakan bahasa Dart, Anda bisa memanfaatkan library `dart:convert` yang tersedia bawaan untuk melakukan tugas parsing ini.

3. **Menggunakan Data dalam Flutter:**
   - Setelah parsing, data yang diperoleh dapat diintegrasikan ke dalam aplikasi Flutter. Ini biasanya melibatkan penerapan data tersebut ke berbagai widget dan komponen dalam Flutter untuk menampilkan atau memanipulasinya sesuai kebutuhan.

4. **Pengelolaan State (Opsional):**
   - Dalam kasus di mana data JSON perlu diperbarui secara dinamis atau ada banyak widget yang bergantung pada data ini, pertimbangkan untuk menggunakan teknik pengelolaan state. Flutter menyediakan beberapa opsi untuk ini, termasuk `setState`, `Provider`, `Riverpod`, dan lainnya, yang membantu dalam sinkronisasi dan pengelolaan data secara efektif di seluruh aplikasi.

## Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
**Flutter (Sebagai Klien)**

1. **Input Informasi Akun:**
   - Buat sebuah antarmuka di aplikasi Flutter yang memungkinkan pengguna untuk memasukkan detil akun mereka, seperti nama pengguna dan password.

2. **Mengirim Permintaan Autentikasi ke Server:**
   - Setelah formulir login disubmit oleh pengguna, aplikasi Flutter harus mengirim permintaan HTTP ke server Django. Ini bisa dilakukan menggunakan library `http` yang tersedia di Flutter.

**Django (Sebagai Server)**

1. **Menangani Proses Autentikasi:**
   - Pada sisi server yang menggunakan Django, harus ada implementasi untuk proses autentikasi. Django menawarkan berbagai fungsi dan library bawaan untuk mengatur autentikasi. Penting untuk memastikan penggunaan HTTPS untuk menjaga keamanan data saat transit.

2. **Mengirim Respon ke Aplikasi Flutter:**
   - Setelah permintaan autentikasi diproses oleh Django, server harus mengirimkan respons kembali ke aplikasi Flutter. Respons ini bisa berupa token akses jika pengguna berhasil diautentikasi, atau pesan error jika proses autentikasi gagal.

## Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.
1. **ElevatedButton dan TextButton:** Tombol interaktif untuk pengguna, seperti tombol "Login", yang memungkinkan aksi atau input dari pengguna.

2. **FutureBuilder:** Digunakan untuk mengelola operasi asinkron, seperti permintaan HTTP untuk autentikasi. FutureBuilder membangun antarmuka pengguna berdasarkan hasil dari operasi asinkron (misalnya, sedang memuat, berhasil, atau gagal).

3. **Navigator:** Mengatur navigasi di aplikasi Flutter. Digunakan untuk berpindah antar halaman, seperti dari halaman login ke halaman utama setelah autentikasi berhasil.

4. **Scaffold:** Memberikan struktur dasar UI, termasuk komponen seperti AppBar dan body, untuk membangun tampilan utama aplikasi.

5. **Column dan ListView:** Mengatur widget secara vertikal. Berguna untuk menyusun elemen seperti tombol dan teks dalam urutan vertikal.

6. **Text:** Menampilkan teks pada UI, seperti pesan kesalahan atau informasi lainnya.

7. **ListTile:** Menampilkan item dalam format daftar. Mendukung penggunaan avatar, yang bisa digunakan untuk menampilkan gambar profil pengguna atau elemen grafis serupa.

8. **SizedBox:** Menetapkan ukuran khusus untuk widget atau memberikan ruang kosong dalam layout.

9. **TextField:** Widget untuk input teks, digunakan untuk memasukkan informasi seperti nama pengguna dan kata sandi.

10. **Card:** Membuat elemen UI berbentuk kartu yang bisa digunakan untuk menampilkan informasi atau konten dalam cara yang terorganisir, sering digunakan untuk ragam pengelompokan informasi dalam antarmuka pengguna.