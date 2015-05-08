# OpenSIPS Installation

## About

Info   | Value
------ | -----
Update | 1505072330
Author | [Anton Raharja](http://antonraharja.com)

This document explains how to install OpenSIPS and configure it for VoIP ID.

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
apt-get install build-essential flex bison zlib1g-dev libncurses5-dev libssl-dev libfrontier-rpc-perl libmysqlclient-dev pkg-config
```

### Step 3: Compile and install OpenSIPS

Execute below commands correctly and in order to compile and install OpenSIPS:

```
TLS=1 make
TLS=1 make include_modules="db_mysql auth_db" modules
TLS=1 make include_modules="db_mysql auth_db" install
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

Setup init script for OpenSIPS:

```
cd /opt/src/opensips/opensips-1.9.1-tls
cp packaging/debian/opensips.init /etc/init.d/
chmod +x /etc/init.d/opensips.init
cp packaging/debian/opensips.default /etc/default/opensips
chmod -x /etc/default/opensips
update-rc.d opensips.init defaults 99
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
