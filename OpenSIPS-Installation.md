# OpenSIPS Installation

Info   | Value
------ | -----
Update | 1505071330
Author | [Anton Raharja](http://antonraharja.com)

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
TLS=1 make include_modules="db_mysql" modules
TLS=1 make include_modules="db_mysql" install
```

### Step 3: Verify installation

Verify that OpenSIPS binaries are exists in /usr/local/sbin, we should see `opensips*` and `osip*` binary files:

```
ls -l /usr/local/sbin/
```

We also need to make sure that all default and required extra modules are copied to OpenSIPS module directory:

```
ls -l /usr/local/lib/opensips/modules/
```
