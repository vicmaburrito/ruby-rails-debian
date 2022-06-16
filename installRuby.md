# To Install VM and Debian 11 distribution:

## [Click Here](https://www.youtube.com/watch?v=6PTjoSBdjok&t=132s&ab_channel=FacultadAutodidacta)

## To install sudo on Debian

```bash
 $ su
 $ apt-get install sudo
 $ nano /etc/sudoers
```
* Below of ```%sudo   ALL=(ALL:ALL) ALL``` : 
  ```bash
  yourUsername ALL=(ALL:ALL) ALL
  ```

* Then run
  ```bash
  sudo apt-get update 
  sudo apt-get upgrade
  ```

# Debian Swap

* 1 : ``` $ cat /proc/sys/vm/swappiness```
* 2 : ``` $ sudo nano /etc/sysctl.conf```
  - On nano editor, go to the bottom of the page and add ```vm.swappiness=10```
* 3 : Reboot your system and run again the first command

# Installing Ruby 

## First, we need to make sure your Linux distribution is up to date

```
  sudo apt update
  sudo apt upgrade
```

## Install Packages and Libraries
```bash
$ sudo apt install gcc make libssl-dev libreadline-dev zlib1g-dev libsqlite3-dev
```

### if you don't have git, just run:
```bash
$ sudo apt install git
```

## Install rbenv
```bash
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
$ exit
```

### Install ruby-build
```bash
$ mkdir -p "$(rbenv root)"/plugins
$ git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```
### Run:
```bash
$ rbenv -v
# Output: rbenv 1.2.0-14-xxxxx
```

## Install Ruby
```bash
  $ rbenv install 2.7.4 --verbose
```
  * Then
  ```bash
   $ rbenv global 2.7.4
   $ ruby -v 
   # Output: 
   # ruby 2.7.4pxxx (xxxx revision xxxxx)[x86_64-linux]
   ```

# Install Rails
```bash
 $ gem install rails -v 6.0.4.8
 $ rails -v
 # Output:
 # Rails 6.0.4.8
```
 
# Installing MariaDB 

## Install MariaDB
```bash
sudo apt install mariadb-server 
```

## Configure MariaDB on Debian
```bash
sudo mysql_secure_installation 
```

* Then 
   - Switch to unix_socket authentication [Y/N] n
   - Change the root password? [Y/N] n
   - Remove anonymus users? [Y/N] y
   - Disallow root login remotely? [Y/N] y
   - Remove test database and access to it? [Y/N] y
   - Reload privilege tables now? [Y/N] y

## Create Privileges User with Authentication
```bash
$ sudo mysql
```
```sql
- CREATE USER 'yourUsername'@'localhost' IDENTIFIED BY '_pa$$w0rd_';
- GRANT ALL ON *.* TO 'yourUsername'@'localhost' WITH GRANT OPTION;
- FLUSH PRIVILEGES;  
- EXIT
```
## To test the status of MariaDB
```bash
$ sudo systemctl status mariadb
$ sudo systemctl start mariadb 
```



If you already have a mysql installed on your local environment maybe you will find a troubles like this: 
```bash
“ERROR 2002 (HY000): Can’t connect to local MySQL server through socket ‘/var/run/mysqld/mysqld.sock’ (2)”
```
We will remove mysql with the following commands
```bash
$ sudo apt-get remove --purge mysql-server mysql-client $ mysql-common -y
$ sudo apt-get autoremove -y
$ sudo apt-get autoclean
$ sudo rm -rf /etc/mysql
$ sudo find / -iname 'mysql*' -exec rm -rf {} \;
```
