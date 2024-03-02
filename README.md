#PERINTAH BUAT CASA OS

#SET IP STATIC


sudo nano /etc/network/interfaces


# Ethernet adapter 0
auto eth0
allow-hotplug eth0
#no-auto-down eth0
iface eth0 inet static
address 192.168.100.10
netmask 255.255.255.0
gateway 192.168.100.1
dns-nameservers 192.168.100.1
#dns-nameservers 1.1.1.1 8.8.8.8


#PERINTAH INSTALL APACHE DAN KAWAN KAWAN

# Catat dulu IP Address STB. Misalnya:  192.168.88.220
  Login ke putty, setelah itu lakukan proses instalasi paket 
  berikut secara berurutan:
 
1. Update dan upgrade
   apt update
   apt upgrade
 
2. MariaDB (Pengganti MySQL) 
   apt-get -y install mariadb-server mariadb-client
   mysql_secure_installation
 
3. Apache web server
   apt-get -y install apache2
   #cek apakah apache sudah berjalan: buka browser ketik: ip stb
 
4. PHP 7
   apt-get -y install php7.0 libapache2-mod-php7.0
   apt-get -y install php7.0-mysql php7.0-curl
   service apache2 restart
   #cek apakah php sudah berjalan dengan menulis script berikut:
   nano /var/www/html/info.php
   <?php
   phpinfo();
   #buka browser ketik: ip stb/info.php
 
5. phpMyAdmin
   apt-get -y install phpmyadmin
   sudo ln -s /usr/share/phpmyadmin /var/www/html/
   #buat akun admin phpmyadmin
   sudo mysql -u root
   CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
   FLUSH PRIVILEGES;
   exit
   service apache2 restart
   #buka browser ketik: ip stb/phpmyadmin
 
6. Upload mikbotam ke webserver dan setting conneksi database 
   dan API ROS
 
   #Script chown filder mikbotam:
   chown -R www-data:www-data [folder mikbotam]
 
7. Menjalankan scrip bot telegram
   cd /var/www/html/mikbotam/Saldo
   php Core_Saldo_Nonsaldo.php
 
8. AutorRun script
   sleep 10 && cd /var/www/html/mikbotam/Saldo && php Core_Saldo_Nonsaldo.php > /dev/null 2>&1&


