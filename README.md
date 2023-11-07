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