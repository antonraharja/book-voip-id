# VoIP ID Installation

## About

This document explains how to install VoIP ID software.

Info   | Value
------ | -----
Update | 1505071750
Author | [Anton Raharja](http://antonraharja.com)
Author | [Asoka Wardhana](http://asokawardhana.web.id/)

### Step 1: Install Ubuntu 14.04 server

During installation you need to select these packages:

- OpenSSH server
- LAMP
- Mail server

### Step 2: Update Ubuntu 14.04 server

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

### Step 5: Enable mod_rewrite

```
a2enmod rewrite
service apache2 restart
```

### Step 6: Update Apache2 options

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

### Step 7: Add essential databases

```
mysqladmin -uroot -p create voip_id
mysqladmin -uroot -p create opensips
```

### Step 8: Get the software and setup

Get source codes from git repository:

```
mkdir -p /opt/git
cd /opt/git
git clone https://github.com/antonraharja/voip-id.git
```

Edit database access:

```
vi voip-id/app/config/database.php
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
./composer.phar self-update
./composer.phar update
php artisan migrate
```

### Step 9: Install VoIP ID on Apache2

```
mv /var/www/html /var/www/html.dist
ln -s /opt/git/voip-id/public /var/www/html
```

### Almost done, init VoIP ID

Visit `http://this_server_IP/init` once.

Visit `http://this_server_IP` and login using below access to enter admin menus:

Username | Password
-------- | --------
admin    | admin123
