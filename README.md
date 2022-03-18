# Traffic Capture Wireshark

## Soal 1

```
Cari filter dari soal1.pcap
1. Display Filter sehingga wireshark hanya mengambil paket yang berasal dari 192.168.1.158
2. Display Filter sehingga wireshark hanya mengambil paket yang menuju ke 192.168.1.255
```

**1.** Command untuk mencari paket yang berasal dari suatu port adalah `ip.src = IP_ADDRESS`  
Maka, dengan menginputkan display filter sesuai ip addressnya, yaitu `ip.src == 192.168.1.158`, kita akan memperoleh paket hanya dari ip address 192.168.1.158
![image](https://user-images.githubusercontent.com/78243059/158618024-28506881-5aa2-4c23-92b8-929023ec57fe.png)

**2.** Command untuk mencari paket yang menuju ke suatu port adalah `ip.dst = IP_ADDRESS`  
Maka, dengan menginputkan display filter sesuai ip addressnya, yaitu `ip.src == 192.168.1.255`, kita akan memperoleh paket hanya dari ip address 192.168.1.255
![image](https://user-images.githubusercontent.com/78243059/158618447-409ca21c-37ea-46af-b6ac-826b9bc69a67.png)

## Soal 2

```
Ann adalah seorang tersangka dalam sebuah tindak kejahatan. Setelah bebas dengan uang jaminan, Ann melarikan diri.
Polisi mengatakan bahwa kemungkinan besar dia melarikan diri bersama pacarnya. Penyidik telah memonitor lalu lintas jaringan yang digunakan Ann.
Dari file soal2.pcap yang merupakan hasil capture lalu lintas jaringan, diharapkan investigator bisa mencari keberadaan Ann.

Cari data sebanyak mungkin berdasar filter di dalam file soal2.pcap
1. Cari data user berupa email yang ada dalam .pcap
2. Pada protokol imf terdapat 2 pesan. Cari 2 data pesan tersebut!
3. Cari data file .docx yang dikirim Ann
4. Cari lokasi meeting Ann
```

**1.** Untuk mencari data yang berkaitan dengan email, kita bisa memanfaatkan keywork gmail, yahoo, atau semacamnya. Di sini, kita akan menggunakan keyword yang lebih umum, yaitu .com sehingga syntax-nya menjadi `tcp contains .com`  
Akan diperoleh beberapa paket-paket yang mengandung keyword `.com`.  
![image](https://user-images.githubusercontent.com/78243059/158636448-33c960cb-032f-4081-938b-9249810ba732.png)
![image](https://user-images.githubusercontent.com/78243059/158636344-35c4fb2f-8ade-460e-aba3-572c863ae57b.png)

Dengan menelusuri paket-paket yang ada, kita memperoleh beberapa email user yang terlibat, yaitu:

- sneakyg33k@aol.com selaku Ann Dercover
- mistersecretx@aol.com
- sec558@gmail.com

**2.** Dua pesan pada protokol IMF bisa didapatkan melalui File > Export Objects > IMF. Terdapat dua buah file bernama `lunch next week.eml` dan `rendezvous.eml` yang bisa di-save dan dibuka salah satunya menggunakan Microsoft Outlook.  
![image](https://user-images.githubusercontent.com/78243059/158637384-439b561a-cdbe-43b5-9557-7934dfae71ff.png)
![image](https://user-images.githubusercontent.com/78243059/159020137-0a34111e-3977-4f5c-8a03-e38fbf7be3eb.png)
![image](https://user-images.githubusercontent.com/78243059/159020225-9cbf8eab-6ed1-4147-b61f-85105c12e872.png)

**3.** Pada file `rendezvous.eml`, terdapat attachment berupa file `secretrendezvous.docx`.  
![image](https://user-images.githubusercontent.com/78243059/158637916-0d3f7edb-1683-4902-bbee-1e3863924ed2.png)

**4.** File `secretrendezvous.docx` tadi menyimpan gambar alamat pertemuan Ann, yaitu di Playa del Carmen, Mexico.  
![image](https://user-images.githubusercontent.com/78243059/158638211-6016190f-e915-4814-9cf4-85ec909b524a.png)

### Informasi Tambahan

**1.** Dapat diamati bahwa interkasi yang dilakukan Ann menggunakan email. Kita bisa mengamati lebih dalam traffic yang bersangkutan dengan protokol email, yaitu smtp.  
Menggunakan command `smtp`, kita bisa mendapatkan semua traffic email dan menemukan autentifikasi saat user login. Terlihat datanya sudah dienkripsi, maka kita bisa coba decode base64 dan mendapatkan hasil sebagai berikut:  
**Username** : sneakyg33k@aol.com  
**Password** : 558r00lz  
![autentikasi - edit](https://user-images.githubusercontent.com/78243059/158768753-1be2e1e1-f0b9-443e-b246-22d5ac0a8692.png)

## Soal 3

```
Buat suatu display filter sehingga wireshark hanya mengambil paket yang mengandung port 21!
```

Tahapan penyelesaiannya dilakukan dalam beberapa langkah sebagai berikut:

**1.** Buka wireshark dan start capturing pada `Adapter for Loopback Traffic Capture` untuk menangkap traffic pada lokal komputer kita.  
![image](https://user-images.githubusercontent.com/78243059/158621582-5af468f4-2c68-4be4-91e8-0fd6a6ee38f9.png)

**2.** Start server FileZilla di XAMPP dan connect ke loopback ip address `127.0.0.1`. Lalu, buat user dan pastikan server terbuka untuk port 21  
![image](https://user-images.githubusercontent.com/78243059/158621865-79674fcc-10b4-4581-b540-358d4a7fb948.png)

**3.** Connect ke server menggunakan FilleZilla client pada host 127.0.0.1 dan port 21 berdasarkan user yang sudah dibuat tadi.  
![image](https://user-images.githubusercontent.com/78243059/158623267-f5f2026f-b41c-4238-b5a7-6fc83b732d9b.png)

Pastikan sudah mendapat konfirmasi directory listing sukses dan panel kanan aplikasi terisi oleh path folder server kita.  
![image](https://user-images.githubusercontent.com/78243059/158624168-ec5f39d4-f530-4fff-a70d-f7a02e2ae2f2.png)

**4.** Simulasikan transfer file antara client dan server pada FileZilla.  
Contoh dan caranya, drag and drop file `ncc.txt` dari panel kiri ke kanan untuk meng-copy-nya dari client ke server. File akan otomatis ter-copy.
![image](https://user-images.githubusercontent.com/78243059/158624767-99a637f7-cfd1-4d79-af97-c8a76e850e41.png)

**5.** Perhatikan di Wireshark, syntax untuk memfilter paket yang mengandung port 21 adalah `tcp.port == 21` karena traffic pada lokal komputer di sini menggunakan protokol tcp.  
![image](https://user-images.githubusercontent.com/78243059/158626273-ad29eb2c-f9f5-41cf-a822-d88d33994176.png)

Sejak saat kita koneksikan client dengan server, traffic request-nya sudah tercatat di Wireshark. Karena kita mengetahui nama user-nya tadi adalah `marcel`, maka kita bisa cari cepat dengan menggunakan syntax `tcp contains marcel`.
![image](https://user-images.githubusercontent.com/78243059/158626981-25feaf95-0100-48fb-bf4d-6e4a014d7ec0.png)

Demikian pula saat kita men-transfer file `ncc.txt` dari client ke server, request-nya juga tercatat di Wireshark. Dengan syntax yang sama dengan sebelumnya, kita bisa cari paketnya menggunakan `tcp contains ncc.txt`
![image](https://user-images.githubusercontent.com/78243059/158627475-63325a67-3587-47d2-b921-dfe26fbd8c80.png)

Request tersebut mengandung port 21 dibuktikan dengan membuka detail paket pada section Transmission Control Protocol. Request bisa berasal dari atau menuju ke port 21.
![image](https://user-images.githubusercontent.com/78243059/158628538-67db7857-bfd5-4d93-8595-ab6f8ca2b6a2.png)
