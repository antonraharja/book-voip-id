# VoIP ID Installation

## About

Info   | Value
------ | -----
Update | 1505071750
Author | [Anton Raharja](http://antonraharja.com)
Tester | [Asoka Wardhana](http://asokawardhana.web.id/)

This document explains how to install VoIP ID software, the web User Interface part.

### Step 1: Install Ubuntu server 14.04 or 15.04

During server installation you need to select these packages:

- OpenSSH server
- LAMP
- Mail server

Run below command when your server installed without LAMP stack:

```
apt-get install apache2 mysql-server mysql-client php5 php5-cli php5-mysql php5-gd
```

### Step 2: Update Ubuntu server 14.04 or 15.04

```
apt-get update
apt-get upgrade
```

### Step 3: Install git

```
apt-get install git
```

### Step 4: Install PHP5 Mcrypt and enable it

```
apt-get install php5-mcrypt
php5enmod mcrypt
service apache2 restart
```

### Step 5: Install composer

```
cd
php -r "readfile('https://getcomposer.org/installer');" | php
mv composer.phar /usr/local/bin/composer
chmod +x /usr/local/bin/composer
```

### Step 6: Enable mod_rewrite

```
a2enmod rewrite
service apache2 restart
```

### Step 7: Update Apache2 options

For rewrite modules to work properly in this manual you need to change `AllowOverride` option from `None` to `All`.

We will update the default vhost. A better way would be to create a new vhost and configure it properly.

Add below option block to `/etc/apache2/sites-available/000-default.conf` (just under `DocumentRoot` option would be fine):

```
<Directory /var/www/html>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
```

Restart apache2, again:

```
service apache2 restart
```

### Step 8: Add essential MySQL databases

```
mysqladmin -uroot -p create voip_id
mysqladmin -uroot -p create opensips
```

### Step 9: Get the software and setup

Get source codes from git repository:

```
mkdir -p /opt/git
cd /opt/git
git clone https://github.com/antonraharja/voip-id.git
cd /opt/git/voip-id
```

Edit database access:

```
vi app/config/database.php
```

Change MySQL username and password on below section:

```
'mysql' => array(
        'driver'    => 'mysql',
        'host'      => 'localhost',
        'database'  => 'voip_id',
        'username'  => 'root',
        'password'  => 'password',
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci',
        'prefix'    => '',
),

'mysql2' => array(
         'driver'    => 'mysql',
         'host'      => 'localhost',
         'database'  => 'opensips',
         'username'  => 'root',
         'password'  => 'password',
         'charset'   => 'utf8',
         'collation' => 'utf8_unicode_ci',
         'prefix'    => '',
),
```

Update composer files and initiate Laravel:

```
composer update
php artisan migrate
```

### Step 10: Install VoIP ID on Apache2

```
mv /var/www/html /var/www/html.dist
ln -s /opt/git/voip-id/public /var/www/html
chown www-data.www-data -R /opt/git/voip-id/
```

### Step 11: Init VoIP ID from browser

From browser visit `http://this_server_IP/init` once.

Edit `app/routes.php` to comment init route at line 8:

```
vi /opt/git/voip-id/app/routes.php
```

### Step 12: Login from browser for the first time

Visit `http://this_server_IP` and login using below access to enter admin menus:

Username | Password
-------- | --------
admin    | admin123
