# VoIP ID Installation

Info   | Value
------ | -----
Update | 1505071200
Author | [Anton Raharja](http://antonraharja.com)

### Install Ubuntu 14.04 server

During installation you need to select these packages:

- OpenSSH server
- LAMP
- Mail server

### Update Ubuntu 14.04 server

```
apt-get update
apt-get upgrade
```

### Install git

```
apt-get install git
```

### Install PHP5 Mcrypt and enable it

```
apt-get install php5-mcrypt
php5enmod mcrypt
service apache2 restart
```

### Enable mod_rewrite

```
a2enmod rewrite
service apache2 restart
```

### Update Apache2 options

For rewrite modules to work properly in this manual you need to change `AllowOverride` option from `None` to `All`.

We will update the default vhost. A better way would be to create a new vhost and configure it properly.

Add below option block to `/etc/apache2/sites-available/000-default.conf`:

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

### Add essential databases

```
mysqladmin -uroot -p create voip_id
mysqladmin -uroot -p create opensips
```

## Get the software and setup

```
mkdir -p /opt/git
cd /opt/git
git clone https://github.com/antonraharja/voip-id.git
cd voip-id
./composer.phar self-update
./composer.phar update
php artisan migrate
```

### Install VoIP ID on Apache2

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
