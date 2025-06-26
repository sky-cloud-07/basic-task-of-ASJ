![image](https://github.com/user-attachments/assets/fd051558-4073-47a1-b88c-00f9d3055194)# Basic Task Of ASJ/Firmansyah Teacher/11 Grade/
Ini adalah contoh projek dasar untuk anak SMK jurusan TKJ dalam mata pelajaran Administrasi Sistem Jaringan (ASJ)

# TUTORIAL KONFIGURASI DNS, FTP, FILE, WEB, DATABASE SERVER dan MAIL SERVER
## Penginstalan debian 7 di VM
1. Folder select "iso linux debian 7"
2. iso image "debian dvd 1" 
3. Hardware 2048 mb
4. Hard disk 8 gb  

_start - normal start_

1. Setting up the country, languange, and etc
2. Hostname "ur name/debian"
3. Domain name "kosongkan"
4. pw "12345678"
5. **enter**
6. full name "enter ur long name"
7. username "enter ur long name"
8. pw "12345678"
9. choose western
10. **enter** use entire disk 
11. **enter** SCSI3
12. **enter** All files in one partion
13. **enter** finish partioning
14. **yes** write changes to disks
15. **no** scan another cd or dvd
16. **no** network mirror
17. **_eror_** just continue
18. **no** participate on package usage survey
19. just give _star_ to "standar system utilities and maybe laptop (optional)
20. **yes** install the grup boot loader


## COMMAND KONFIGURASI DNS 
_(pastikan dvd kosong)_
1. login "root"
2. pw 12345678
3. nano /etc/network/interfaces

auto eth0
iface eth0 inet static 
address 200.100.1.23
netmask 255.255.255.0

auto eth0:1 
iface eth0:1 inet static 
address 200.100.1.24
netmask 255.255.255.0

3. service networking restart
4. ifconfig (untuk mengecek apakah ip nya sudah masuk atau belum)

**INSTALASI PACKAGE DNS NYA**

5. apt-get install bind9 
6. y
7. masukin dvd 1 nya
8. **enter**
9. nano /etc/bind/named.conf 
paling bawah ketikan 

zone "hanif.com"{
type master;
file "/etc/bind/db.hanif";
};

zone "irsyad.or.id"{
type master;
file "/etc/bind/db.irsyad";
};

zone "1.100.200.in-addr.arpa"{
type master;
file "/etc/bind/db.200";
};


10. cd /etc/bind/
11. cp db.local db. hanif
12. cp db.local db.irsyad 
13. cp db.127 db.200
14. nano db.hanif
    
    ![image](https://github.com/user-attachments/assets/6d0b8a3f-dbcc-4352-8a69-ba6e7dd59e2f)

16. nano db.irsyad
    
    ![image](https://github.com/user-attachments/assets/13ce6550-0812-43dd-9cbf-ce1e9a38fb23)

18. nano db.200

    ![image](https://github.com/user-attachments/assets/d04f9029-ffa1-4d3d-a3b1-8db9e1183480)

20. nano /etc/resolv.conf

search hanif.com
nameserver 200.100.1.23
search irsyad.or.id
nameserver 200.100.1.24

18. service bind9 restart
19. nslookup hanif.com
20. nslookup irsyad.or.id
21. nslookup 200.100.1.23
22. nslookup 200.100.1.24

## KONFIGURASI FTP SERVER 
1. Ganti dvd2 
2. apt-cdrom ident
3. apt-cdrom add
4. apt-get install proftpd
5. y
6. Ganti ke DVD 1
7. **Enter** 
8. Ganti ke DVD 2
9. **Enter**
10. Pilih standalone. Enter
11. nano /etc/proftpd/proftpd.conf
12. Di bagian server name kasih hanif.com

Scroll paling bawah 

<Anonymous /fileftp>
User	 Admin      
</Anonymous>

<Anonymous /fileftp>
User       anonymous      admin
</Anonymous>

13. mkdir /filetfp
14. chmod -R 777 /fileftp/
15. cd /fileftp/
16. mkdir file1 file2 file3 
17. useradd -d /fileftp/ admin
18. passwd admin
19. pw: 12345678
20. service proftpd restart


## KONFIGURASI WEB SERVER 
1. apt-get install apache2 php5
2. y
3. Ganti dvd 1
4. nano /etc/apache2/sites-available/default

    ![image](https://github.com/user-attachments/assets/53f52036-ec89-4b64-9d8e-d8c946ea7df4)

5. service apache2 restart
6. nano /var/www/index.html

    ![image](https://github.com/user-attachments/assets/4b8d143a-3c94-44ca-a256-146dbd0b52e2)


## KONFIGURASI DATABASE SERVER
1. apt-get install mysql-server mysql-client
2. y
3. masukin pw 12345678
4. apt-get install phpmyadmin
5. y
6. centang apache2
7. yes
8. pw 12345678
9. pergi ke tools vb - create vb host only adapter
10. ke setting, virtual network, di adapter 1, **ubah nat** jadi **host only adapter** 
untuk **promiscuous** mode allow all. Cable harus **connected**. 

11. Pergi ke control panel - ke network and sharing center. 
Cari jaringan host only adapter
Ubah ip nya menjadi _200.100.1.22, 200.100.1.23_. lalu ok. 

12. Pergi ke winscp. Login sebagai ftp, host name 200.100.1.23
13. Coba koneksi ke chrome. Coba login ke php. 
14. Ke winscp. Pindahkan file wordpress zip dan surat zip ke direktori yang sudah dibuat. ubah surat **zip** menjadi _rar_. 

15. cd /fileftp/
16. ls
17. mv wordpress(tab) /var/www/
18. ls
19. cd /var/www/
20. ls
21. apt-get install unzip 
22. unzip wordpress(tab)
23. cd wordpress/
24. cp wp-config-sample.php wp-config.php
25. nano wp-config.php

    ![image](https://github.com/user-attachments/assets/556e80df-df1f-4d26-b094-ce366644e396)

26. cd /var/www/
27. ls
28. cd /fileftp/
29. ls
30. mv SURAT.rar /var/www/	
31. cd /var/www/
32. ls
33. apt-get install unzip 
34. ls
35. unzip SURAT.rar
36. ls
37. mysql -u root -p
38. create database surat;
39. show databases;
40. exit;
41. cd /etc/apache2/sites-enabled/
42. ls
43. cp 000-default surat
44. ls
45. nano surat
setelah var www, tambahkan surat. 

 ![image](https://github.com/user-attachments/assets/4a09f8f6-8bf0-4a91-9bf7-dd264304024f)

46. cd /var/www/SURAT/HOME
47. nano koneksi.php
48. service apache2 restart
49. Masuk Kembali ke chromenya, ke database, login aja, pilih surat di sebelah kiri, ke impor , choose file, db.surat lalu kirim
50. buka tab baru lalu tes 200.100.1.23/SURAT/


## KONFIGURASI MAIL SERVER
1. cd
2. nano /etc/apt/sources.list
lalu cek ada berapa dvd nya. ctrl - x
3. eject (untuk mengeluarkan recent dvd)
4. _masukin dvd 3_
5. apt-cdrom ident
6. apt-cdrom add
7. nano /etc/apt/sources.list
8. apt-get install postfix courier-imap courier-pop squirrelmail
9. y
10. ganti dvd 1
11. pilih ok
12. _internet site_
13. mail.yourname.com
14. ganti dvd 2
15. enter
16. _create the directories for web-based administration_ pilih **yes**
17. ganti dvd 3
18. maildirmake /etc/skel/Maildir
19. nano /etc/postfix/main.cf
20. scrool paling bawah, lalu ketikkan
home_mailbox = Maildir/
dpkg-reconfigure postfix
21. **ok**
22. _internet site_
23. mail.yourname.com
24. biarkan kosong
25. periksa di bagian depan nya ada mail atau engga. (harus ada mail)
26. _force synchronous_ pilih **no** aja
27. kosongin aja
28. _use procmail_ pilih **no** juga
29. biarkan aja 0
30. kosongin aja
31. pilih IPV4, **ok**
32. cd /etc/bind
33. ls
34. nano db.yourname
35. di bagian bawah tambahkan
    mail	IN	A	200.100.1.23
36. cd /etc/apache2/sites-available/
37. ls
38. cp default mail
39. ls
40. nano mail
41. baris **server alias** hapus aja semua
42. di bagian server name. www - ganti jadi **mail**
43. bagian documentroot /var/www ganti menjadi
    documentRoot /usr/share/squirrelmail, begitu pula dengan bagian
    direktori

    ![image](https://github.com/user-attachments/assets/aaa55fb8-da2e-4799-a720-cad67e0f0756)

44. nano /etc/squirrelmail//apache.conf
45. scrool kebawah, sesuiakan informasi seperti ini

     ![image](https://github.com/user-attachments/assets/fa495b8a-d4c9-49a3-ab0a-dcf422738b97)

46. nano /etc/apache2/apache2.conf
47. scrool paling bawah ketikkan
48. _include /etc/squirrelmail/apache.conf_
49. service postfix restart
50. serice bind9 restart
51. service apache2 restart
52. service courier-imap restart
53. ke chrome
54. Masuk ke chrome
55. 200.100.1.23/squirrelmail/src/redirect.php
Pergi ke laman login
56. Masuk Kembali ke linux untuk menambahkan user 

adduser hanif1
pw. 12345678
fullname. Hanif1
sisanya kosongkan saja

Masukkan lagi untuk 
adduser hanif2
pw.12345678
fullname. Hanif2
Sisanya kosongkan saja

57. Login di chrome sebagai user hanif1
Pergi ke bagian **compose**
Kirim pesan ke hanif2
Dengan subject **bebas.** 

Lalu kirim pesan ngasal

Sign out
Lalu masuk sebagai user hanif2
Liat pesan terkirim 
Pilih **string subject=menyapa**
Lalu balas dengan cara **klik reply**
	
Stelah itu liat apakah ada balasan di user hanif1




