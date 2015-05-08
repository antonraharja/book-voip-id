# OpenSIPS Installation

## About

Info   | Value
------ | -----
Update | 1505081000
Author | [Anton Raharja](http://antonraharja.com)
Tester | [Asoka Wardhana](http://asokawardhana.web.id/)

This document explains how to install OpenSIPS and configure it for VoIP ID. This manual contains special steps required to get OpenSIPS to work with VoIP ID, that means it is not meant for standalone or general purpose OpenSIPS installation.

### Step 1: Get OpenSIPS and prepare it

Get OpenSIPS 1.9.1 and extract it:

```
mkdir -p /opt/src/opensips
cd /opt/src/opensips
wget -c http://opensips.org/pub/opensips/1.9.1/src/opensips-1.9.1_src.tar.gz
tar -zxf opensips-1.9.1_src.tar.gz
cd opensips-1.9.1-tls
ls -l
```

### Step 2: Install development packages

```
apt-get install build-essential flex bison pkg-config zlib1g-dev libncurses5-dev libssl-dev libfrontier-rpc-perl libmysqlclient-dev libxml2-dev libpcre3-dev
```

### Step 3: Compile and install OpenSIPS

Execute below commands correctly and in order to compile and install OpenSIPS:

```
TLS=1 make
TLS=1 make include_modules="db_mysql auth_db dialplan presence" modules
TLS=1 make include_modules="db_mysql auth_db dialplan presence" install
```

### Step 3: Verify installation

Verify that OpenSIPS binaries are exists in `/usr/local/sbin`, look for `opensips*` and `osip*` binary files:

```
ls -l /usr/local/sbin/
```

Make sure that all default and required extra modules are copied to OpenSIPS module directory:

```
ls -l /usr/local/lib/opensips/modules/
```

And also make sure that default configuration files exists, look for `opensips.cfg`:

```
ls -l /usr/local/etc/opensips
```

### Step 4: Init script

Setup init script for OpenSIPS, run below commands correctly and in order:

```
cd /opt/src/opensips/opensips-1.9.1-tls
cp packaging/debian/opensips.init /etc/init.d/
chmod +x /etc/init.d/opensips.init
cp packaging/debian/opensips.default /etc/default/opensips
chmod -x /etc/default/opensips
update-rc.d opensips.init defaults 99
mkdir -p /var/run/opensips
groupadd opensips
useradd -M -s /usr/sbin/nologin -g opensips opensips
```

Edit `/etc/init.d/opensips.init` and change these parts:

- search for *PATH* and add `/usr/local/sbin` to *PATH*. Eg: `PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin`
- search for *DAEMON* and change `DAEMON=/usr/sbin/opensips` to `DAEMON=/usr/local/sbin/opensips`
- search for `/etc/opensips/opensips.cfg` and then change it to `/usr/local/etc/opensips/opensips.cfg`

Edit `/etc/default/opensips` and change *RUN_OPENSIPS=no* to *RUN_OPENSIPS=yes*.

Starts OpenSIPS:

```
/etc/init.d/opensips.init start
```

Verify that OpenSIPS is running:

```
ps ax | grep opensips
netstat -lnptu | grep opensips
```

### Step 5: Init DB tables for OpenSIPS

Edit `opensipsctlrc` to get `opensipsdbctl` to work, we will use this binary to init DB tables for OpenSIPS:

```
vi /usr/local/etc/opensips/opensipsctlrc
```

In `opensipsctlrc` you need to make adjustments to match your MySQL setup. In this manual here are options you need to change (make sure that you have removed the comment mark):

```
DBENGINE=MYSQL
DBHOST=localhost
DBNAME=opensips
DBRWUSER=root
DBRWPW="password"
DBROOTUSER="root"
```

Init DB tables for OpenSIPS, answer `y` to all install tables questions:

```
opensipsdbctl reinit
```

### Step 6: Init CDR for OpenSIPS

```
cd /opt/git/voip-id
mysql -uroot -p opensips < contrib/opensips-cdrs/cdrs.mysql.sql
mysql -uroot -p opensips < contrib/opensips-cdrs/opensips_cdrs.mysql.sql
```

### Step 7: Use supplied config file from VoIP ID

```
cd /opt/git/voip-id
ls -l contrib/opensips-cfg/opensips.cfg
cp /usr/local/etc/opensips/opensips.cfg /usr/local/etc/opensips/opensips.cfg.dist
cp contrib/opensips-cfg/opensips.cfg /usr/local/etc/opensips/
```

Edit new `/usr/local/etc/opensips/opensips.cfg` and make these changes:

- Edit the file and look for IP addresses, usually they are marked with comment *CUSTOMIZE ME* beside them. Change IP `192.168.1.150` to your OpenSIPS server IP address.
- Edit the file and look for MySQL username and password, usually they are also marked with comment *CUSTOMIZE ME* beside them. Change `root:password` to your MySQL server access to OpenSIPS database.

Verify configuration:

```
opensips -c
```
Restart OpenSIPS:

```
/etc/init.d/opensips.init restart
```

Verify that OpenSIPS is running:

```
ps ax | grep opensips
netstat -lnptu | grep opensips
```

### Step 8: Setup cron scripts

This step explains how to install cron scripts that integrate OpenSIPS and VoIP ID.

```
cd /opt/git/voip-id
cp -rR contrib/cron-scripts-for-opensips/voip-id/ /usr/local/sbin
```

Configure cron scripts, change DB access options:

```
cd /usr/local/sbin/voip-id/
vi config.php
```

Verify cron scripts installation, those scripts must not popup anything or any errors:

```
cd /usr/local/sbin/voip-id/
./run-service-sync.sh 
./run-service-cleaner.sh 
```

Setup cron, the sync script runs every minute, the cleaner script runs once a day every 1 AM:

```
crontab -e
```

In `crontab -e` put these at the end of file, you need to also make sure that you press `ENTER` at the end of the line:

```
* * * * * /usr/local/sbin/voip-id/run-service-sync.sh >/dev/null 2>&1
0 1 * * * /usr/local/sbin/voip-id/run-service-cleaner.sh >/dev/null 2>&1
```
