# Jarkom-Modul-5-I04-2022

**Module 5 Practicum Report**

Group Members:

+ Farzana Afifah Razak - 5025201130
+ Muhammad Azka Aysar Santoso - 5025201150
+ Raihan Farid - 5025201141


## 1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Strix menggunakan iptables, tetapi Loid tidak ingin menggunakan MASQUERADE.

- Topologi menggunakan VLSM 
![image](https://user-images.githubusercontent.com/81352414/206863677-f1d9c123-5316-4bff-9e38-c8361656c2f1.png)

- Berikut adalah tabel dari perhitungan subnetting
![image](https://user-images.githubusercontent.com/81352414/206863724-1787f0f9-f8d8-419d-bdf8-46b9c190a957.png)

- iptables paling bawah sudah tidak menggunakan ```masquerade```
![image](https://user-images.githubusercontent.com/81352414/206863811-d9949d04-e431-448e-a321-73b436df8039.png)

- Hasil dari ping google
![image](https://user-images.githubusercontent.com/81352414/206863828-bb2aa23b-9a82-4418-8bab-9e043f4e7583.png)

## 2. Kalian diminta untuk melakukan drop semua TCP dan UDP dari luar Topologi kalian pada server yang merupakan DHCP Server demi menjaga keamanan.

- Buka dan jalankan ```WISE``` yang isinya seperti berikut
![image](https://user-images.githubusercontent.com/81352414/206863936-2b8c3681-8438-4091-8f26-55e8aa1c35c0.png)

- Lalu di ```BlackBell``` kita masukkan command ```nmap -sU -p 67 10.38.7.131``` yang mana itu adalah dhcp dari ```WISE```. Terlihat bahwa di sana tertulis ```Filtered``` yang menandakan bahwa berhasil
![image](https://user-images.githubusercontent.com/81352414/206864008-119637dd-6d13-44d0-9162-2aa8e6f9ea87.png)

## 3. Loid meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

- Buka dan jalankan soal no3 yang berisi bahwa kita disuruh untuk membatasi untuk 2 paket saja secara bersamaan
![image](https://user-images.githubusercontent.com/81352414/206864114-132512d8-5340-4b1b-91e7-acd07d9325f0.png)

- Lalu kita ```ping 10.38.7.131``` yang mana itu adalah dhcp dari ```WISE``` di ```Desmond```, ```Briar```, dan ```Forger```

- Ini berhasil dijalankan di ```Desmond``` 
![image](https://user-images.githubusercontent.com/81352414/206864197-fed814f5-6cd9-4f8d-a5ea-d64faeb1f187.png)
 
 - Dan ini juga berhasil dijalankan di   ```Briar```
 ![image](https://user-images.githubusercontent.com/81352414/206864237-6c9f16e5-c5e0-4649-8c6c-239d0676ac54.png)

- Unruk yang di ```Forger``` karna limitnya hanya 2 maka untuk yang ke 3 tidak akan jalan yang menandakan bahwa benar
![image](https://user-images.githubusercontent.com/81352414/206864304-e67bebef-31f2-454b-9804-f6af76249dc1.png)

## 4. Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.

- Buka dan jalankan soal4 di ```Eden```, lalu diisi tanggal dan waktu yang bisa diakses
![image](https://user-images.githubusercontent.com/81352414/206864446-e3d3fa86-a516-47c5-892f-8c23ef45eb59.png)

- Lalu di ```Garden``` kita jalankan soal no4 dan kita coba untuk akses di jam kerja yaitu ```7 Dec 2022 jam 12:00```
![image](https://user-images.githubusercontent.com/81352414/206864513-823c52e4-a5bc-420c-9145-3e40bfc2ba5a.png)

- Dan kita ping dhcp ```Garden``` di ```Briar``` dan berhasil mengakses menuju web server
![image](https://user-images.githubusercontent.com/81352414/206864557-2aad93d4-5d88-4b5c-810b-c168de48069d.png)

- Lalu kita coba ping di luar jam kerja, maka hasilnya tidak akan bisa
![image](https://user-images.githubusercontent.com/81352414/206864594-cab15f60-0fc5-4665-b970-990bbb3913cb.png)

## 5. Karena kita memiliki 2 Web Server, Loid ingin Ostania diatur sehingga setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan.

- Pertama kita bash soal5 di ```Eden```
![image](https://user-images.githubusercontent.com/81352414/206864634-1809f800-ffa8-4694-9bdc-16a3b5fd05ce.png)

- Lalu di ```Garden``` kita disuruh untuk install apache dan mengisi index.htmlnya dan jangan lupa portnya ditambah 443
![image](https://user-images.githubusercontent.com/81352414/206864683-1af94c3b-70d3-4db7-8c37-bb0e09f21266.png)

- Setelah itu kita ```nano .bashrc``` untuk melihat isinya yang telah ditambahkan 443. Fungsinya adalah untuk menjalankan secara otomatis sehingga ketika file ditambahkan maka otomatis akan masuk ke apache. Begitu juga di ```SSS```
![image](https://user-images.githubusercontent.com/81352414/206864736-d3a45c30-6acf-4149-b2ab-aad7585ec766.png)

- Lalu buka ```Blackbell``` dan coba ```garden``` dengan ```curl 10.38.7.138``` untuk mengetes port 443 apakah berjalan atau tidak dan hasilnya berjalan 
![image](https://user-images.githubusercontent.com/81352414/206864905-bf956159-388c-4b6e-98cd-c628ef5cf9d3.png)

## 6. Karena Loid ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.
