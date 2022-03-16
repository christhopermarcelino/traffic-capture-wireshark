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

Request tersebut mengandung port 21 dibuktikkan dengan membuka detail paket pada section Transmission Control Protocol. Request bisa berasal dari atau menuju ke port 21.
![image](https://user-images.githubusercontent.com/78243059/158628538-67db7857-bfd5-4d93-8595-ab6f8ca2b6a2.png)
