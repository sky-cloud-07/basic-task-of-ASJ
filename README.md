# basic-task-of-ASJ
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
apt-get install mysql-server mysql-client
y
masukin pw 12345678
apt-get install phpmyadmin
y
centang apache2
yes
pw 12345678
pergi ke tools vb, create vb host only adapter
ke setting virtual network , di adapter 1, ubah nat jadi host only adapter 
untuk promiscuous mode allow all. Cable harus connected. 
Pergi ke control panel, ke network and sharing center. 
Cari jaringan host only adapter. 
Ubah ip nya menjadi 200.100.1.22, 200.100.1.23. lalu ok. 

Pergi ke winscp. Login sebagai ftp-host name 200.100.1.23
Coba koneksi ke chrome. Coba login ke php. 
lalu ke winscp. Pindahkan file wordpress zip dan surat zip . ubah surat zip menjadi rar. 

Cd /fileftp/
Ls
Mv wordpress…  /var/www/
Ls
cd /var/www/
Ls
Apt-get install unzip 
Unzip wordpress…..
Cd wordpress/
Cp wp-config-sample.php wp-config.php
Nano wp-config.php
 
Cd /var/www/
Ls
Cd /fileftp/
Ls
Mv SURAT.rar /var/www/	
Cd /var/www/
Ls
Apt-get install unzip 
Ls
Unzip SURAT.rar
Ls
Mysql -u root -p 
Create database surat;
Show databases;
Exit;
Cd /etc/apache2/sites-enabled/
Ls
Cp 000-default surat 
Ls
Nano surat, setelah var www, tambahkan surat. 

 
Cd /var/www/SURAT/HOME
Nano koneksi.php 
 
Service apache2 restart
Masuk Kembali ke chromenya, ke database, login aja, pilih surat di sebelah kiri, ke impor , chose file, db.surat lalu kirim 
Tes dengan 
200.100.1.23/SURAT/







KONFIGURASI MAIL SERVER
Cd
Nano /etc/apt/sources.list
	Cek ada berapa dvd nya
	Ctrl x
Eject (untuk mengeluarkan recent dvd)
Masukin dvd 3 
Apt-cdrom ident 
Apt-cdrom add
Nano /etc/apt/sources.list
Apt-get install postfix courier-imap courier-pop squirrelmail
Y
Ganti dvd 1
Pilih ok 
Internet site
Mail.Urname.com
Ganti dvd 2
Enter
Create the directories for web-based administration,  lalu yes
Ganti dvd 3
maildirmake /etc/skel/Maildir
nano /etc/postfix/main.cf
scrool paling bawah
ketikkan 
home_mailbox = Maildir/
dpkg-reconfigure postfix
ok
internet site
mail.urname.com
biarkan kosong 
lalu periksa di depan nya ada mailnya engga
force synchronous pilih no aja
biarkan aja
use procmail, pilih no juga
biarkan aja 0
lalu biarkan aja lagi 
setting ipv4, ok 
cd /etc/bind/
ls
nano db.urname
di bagian bawah tambahkan 
mail	IN	A	200.100.1.23

cd /etc/apache2/sites-available/
ls
cp default mail
ls
nano mail
baris server alias hapus aja semua
di bagian server name. www ganti jadi mail 
bagian DocumentRoot /var/www	ganti menjadi     DocumentRoot /usr/share/squirrelmail
di bagian directory ganti juga

 

Nano /etc/squirrelmail//apache.conf
Scrool kebawah 
Sesuaikan informasi seperti ini 
 
Nano /etc/apache2/apache2.conf
Scrool yang paling bawah, ketikkan
Include /etc/squirrelmail/apache.conf


Lalu masukkan syntax
Service postfix restart
Service bind9 restart 
Service apache2 restart 
Service courier-imap restart 


Masuk ke chrome
200.100.1.23/squirrelmail/src/redirect.php
Pergi ke laman login 

Masuk Kembali ke linux untuk menambahkan user 

Adduser hanif1
Pw. 12345678
Fullname. Hanif1
Sisanya kosongkan saja

Masukkan lagi untuk 
Adduser hanif2
Pw.12345678
Fullname. Hanif2
Sisanya kosongkan saja

Login di chrome sebagai user hanif1

Pergi ke bagian compose
Kirim pesan ke hanif2
Dengan subject bebas. 

Lalu kirim pesan ngasal

Sign out
Lalu masuk sebagai user hanif2
Liat pesan terkirim 
Pilih string subject=menyapa
Lalu balas dengan cara klik reply 
	
Stelah itu liat apakah ada balas di user hanif1















