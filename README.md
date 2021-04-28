vagrant-oracle12.1
==================

Vagrant + Oracle Linux 7 + Oracle Database 11g Release 2 (12.1.0.2) Enterprise Edition | Simple setup of a single instance database.

Download
--------

Download the Oracle Database 12c Release 1 (12.1.0.2) software from My Oracle Support and extract it to the same directory as the Vagrantfile. It should be a subdirectory named `database`.

* p21419221_121020_Linux-x86-64_2of10.zip
* p21419221_121020_Linux-x86-64_1of10.zip

Set environment variables
-------------------------

Copy the file `dotenv.sample` to a file named `.env` and rewrite the contents as needed.

```shell
ORACLE_BASE=/u01/app/oracle
ORACLE_CHARACTERSET=AL32UTF8
ORACLE_HOME=/u01/app/oracle/product/12.1.0.2/dbhome_1
ORACLE_PASSWORD=oracle
ORACLE_PDB=pdb1
ORACLE_SID=orcl
```

Vagrant configuration
---------------------

If you need to use a proxy, first install vagrant-proxyconf and set environment variables for vagrant-proxyconf.

### If the host is macOS or Linux ###

```console
export http_proxy=http://proxy.example.com:80
export https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

export VAGRANT_HTTP_PROXY=http://proxy.example.com:80
export VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
export VAGRANT_FTP_PROXY=http://proxy.example.com:80
export VAGRANT_NO_PROXY=localhost,127.0.0.1
```

### If the host is Windows ###

```console
SET http_proxy=http://proxy.example.com:80
SET https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

SET VAGRANT_HTTP_PROXY=http://proxy.example.com:80
SET VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
SET VAGRANT_FTP_PROXY=http://proxy.example.com:80
SET VAGRANT_NO_PROXY=localhost,127.0.0.1
```

Vagrant up
----------

When you run `vagrant up`, the following will work internally.

* Download and boot Oracle Linux 7
* Install the Oracle Preinstallation RPM
* Create directories
* Set environment variables
* Set password for oracle user
* Install Oracle Database
* Create a listener
* Create a database

```console
vagrant up
```

Example of use
--------------

Connect to the guest OS.

```console
vagrant ssh
```

Connect to the CDB Root.

```console
sudo su - oracle
sqlplus system/oracle
SHOW CON_NAME
```

Connect to a PDB and access the sample table.

```console
sqlplus system/oracle@localhost/pdb1
SHOW CON_NAME
SELECT * FROM hr.employees WHERE rownum <= 10;
```

Author
------

[Shinichi Akiyama](https://github.com/shakiyam)

License
-------

[MIT License](https://opensource.org/licenses/MIT)
