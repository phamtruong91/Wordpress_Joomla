Wordpress_Joomla
================

Tìm hiểu về Wordpess và Joomla
---

1. Ý nghĩa và vai trò
1. Thành phần
1. Cài đặt 

1) Ý nghĩa và vai trò
---
* Joomla và WordPress đều là hệ quản trị nội dung mã nguồn mở hàng đầu trong lĩnh vực thiết kế website

2) Thành phần
---

- Linux: Hệ điều hành
- Apache: Phần mềm máy chủ web
- MySQL: Hệ quản trị cơ sở dữ liệu
- PHP: được phát triển như là một ngôn ngữ kịch bản trên máy chủ (server-side scripting language)
- Gói cài đặt Joomla hoặc Wordpress


![LAMP](http://upload.wikimedia.org/wikipedia/commons/8/82/LAMP_software_bundle.svg  "LAMP")

3) Cài đặt
---

__Các bước cài đặt Wordpress trên Ubuntu 14.04__

__Cài đặt LAMP__

2. Chuẩn bị môi trường Ubuntu 14.04
2. Cài đặt PuTTY và đăng nhập vào Ubuntu 14.04 
2. Đổi mật khẩu root
2. Cài đặt Apache
2. Cài đặt MySQL
2. Cài đặt PHP và một số gói cần thiết
2. Thử nghiệm PHP 

__Cài đặt Wordpess__

* Tạo database name và database user
* Tải Wordpress 
* Cài đặt Wordpress 
* Sao chép File vào Document Root
* Hoàn thành cài đặt thông qua giao diện web

__Cài đặt Joomla__

* Tải Joomla
* Cài đặt
* Tạo database và user
* Truy cập cài đặt Joomla

***

__Bước 1. Chuẩn bị môi trường Ubuntu 14.04__

__Bước 2. Cài đặt PuTTY và đăng nhập vào Ubuntu 14.04__

__Bước 3. Đổi mật khẩu root__

__Bước 4. Cài đặt Apache__

```sh
sudo apt-get update
sudo apt-get install apache2
```

__Bước 5. Cài đặt MySQL__

```sh
sudo apt-get install mysql-server php5-mysql
sudo mysql_install_db
sudo mysql_secure_installation
```

__Bước 6. Cài đặt PHP và một số gói cần thiết__

```sh
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
sudo nano /etc/apache2/mods-enabled/dir.conf
```
Sửa thành:

```sh
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
```sh
sudo service apache2 restart
```
```sh
apt-cache search php5-
```
```sh
apt-cache show package_name
```

```sh
sudo apt-get install package1 package2 ...
```


__Bước 7. Thử nghiệm PHP__

```sh
sudo nano /var/www/html/info.php
```
Thêm vào
```sh
<?php
phpinfo();
?>
```

```sh
http://your_server_IP_address/info.php
```

```sh
sudo rm /var/www/html/info.php
```
__Cài đặt Wordpess__

__Tạo database name và database user__

```sh
mysql -u root -p
CREATE DATABASE wordpress;
CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost;
FLUSH PRIVILEGES;
exit
```

__Tải Gói__

Tải WordPress
```sh
cd ~
wget http://wordpress.org/latest.tar.gz

tar xzvf latest.tar.gz

sudo apt-get update
sudo apt-get install php5-gd libssh2-php
```

__Cài đặt__

Cài đặt Wordpess

```sh
cd ~/wordpress
cp wp-config-sample.php wp-config.php
nano wp-config.php
```

Sửa thành

```sh
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'wordpressuser');

/** MySQL database password */
define('DB_PASSWORD', 'password');
```
__Sao chép file vào document root__

```sh
sudo rsync -avP ~/wordpress/ /var/www/html/
cd /var/www/html
sudo chown -R demo:www-data *
mkdir /var/www/html/wp-content/uploads
sudo chown -R :www-data /var/www/html/wp-content/uploads
```

__Hoàn thành cài đặt thông qua giao diện web__

```sh
http://server_domain_name_or_IP
sudo nano /etc/apache2/sites-available/000-default.conf
sudo a2enmod rewrite
sudo service apache2 restart
```

```sh
touch /var/www/html/.htaccess
sudo chown :www-data /var/www/html/.htaccess
chmod 664 /var/www/html/.htaccess
chmod 644 /var/www/html/.htaccess
```

```sh
nano /var/www/html/.htaccess
```

__Cài đặt Joomla__

__Tải Joomla__

```sh
mkdir temp
cd temp
wget http://joomlacode.org/gf/download/frsrelease/17410/76021/Joomla_2.5.7-Stable-Full_Package.tar.gz
sudo tar zxvf Joomla_2.5.7-Stable-Full_Package.tar.gz  -C /var/www
```

__Cài đặt__

```sh
sudo touch /var/www/configuration.php
sudo chmod 777 /var/www/configuration.php
```
__Tạo database và user__

```sh
mysql -u root -p
CREATE DATABASE joomla;
CREATE USER juser@localhost;
SET PASSWORD FOR juser@localhost= PASSWORD("password");
GRANT ALL PRIVILEGES ON joomla.* TO juser@localhost IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
sudo service apache2 restart
```

__Truy cập cài đặt Joomla__

```sh
sudo rm -rf /var/www/installation/
sudo chmod 755 /var/www/configuration.php
```
