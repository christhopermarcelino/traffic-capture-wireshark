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
