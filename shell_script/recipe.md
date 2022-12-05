## Sudo Root - Le super utilisateur + Vérification
```
su
apt install sudo
apt update
apt upgrade
```
```
sudo usermod -aG sudo username
getent group sudo
sudo whoami
```
## Visudo 
Avertissement : ne modifiez jamais ce fichier en utilisant un éditeur de texte normal ! À la place, utilisez toujours la commande visudo !
```
cd /var/log/
sudo mkdir sudo
cd sudo
sudo touch sudo.log
sudo visudo
```
```
Defaults     passwd_tries=3
Defaults     badpass_message="Mauvais mot de passe, reesayez !"
Defaults     logfile="/var/log/sudo/sudo.log"
Defaults     log_input
Defaults     log_output
Defaults     requiretty
```
## UFW
```
sudo aa-status (apparmor)
sudo apt install ufw
sudo ufw enable
```
add 4242 in virtual box setup

## OPEN SSH
```
sudo apt install openssh-server
sudo systemctl status ssh
sudo nano etc/ssh/sshd_config
```
change 22 pour 4242
```
sudo systemctl restart ssh
sudo ufw allow 4242
sdo systemctl restart ssh
sudo systemctl status ssh
```
## Security
```
sudo nano /etc/login.defs
```
```
#PASS_MAX_DAYS 30
#PASS_MIN_DAYS 2
#PASS_WARN_AGE 7
```
```
sudo apt install libpam-pwquality
sudo nano /etc/security/pwquality.conf
```
```
#DIFFOK = 7
#MINLEN = 10
#DCREDIT -1
#UCREDIT = -1
#LCREDIT = -1
#MAXREPEAT = 3
#USERCHECK = 1
#RETRY = 3
#ENFORCE_FOR_ROOT
```
## Scripting log
```
sudo apt install net-tools
sudo touch monitoring.sh
sudo chmod 755 monitoring.sh
```
```
#!/bin/bash
ARCH=$(uname -srvmo)
CPU=$$(grep 'physical id' /proc/cpuinfo | uniq | wc -l)
VCPU=$(grep '^processor' /proc/cpuinfo | uniq | wc -l)
RAM_TOTAL=$(free -m | grep Mem | awk '{print $2}')
RAM_USED=$(free -m | grep Mem | awk '{print $3}')
RAM_PER=$(free -m | grep Mem | awk '{printf("%.f%%"), $3 / $2 * 100}')
DISK_TOTAL=$(df -h --total | grep total | awk '{print $2}')
DISK_USED=$(df -h --total | grep total | awk '{print $3}')
DISK_PER=$(df -k --total | grep total | awk '{print $5}')
CPU_LOAD=$(top -bn1 | grep '^Cpu' | xargs | awk '{printf "%.1f%%\n", $2 + $4}')
LAST_BOOT=$$(who -b | awk '{print($3 " " $4)}')
LVM=$(lsblk | grep "lvm" | wc -l)
LVM_USE=$(if [ $LVM -eq 0 ]; then echo no; else echo yes; fi)
TCP=$(cat /proc/net/sockstat{,6} | awk '$1 =="TCP:"{print $3}')
USER_LOG=$(who | wc -l)
IP_ADRESS=$(hostname -I)
MAC_ADDR=$(ip link show | grep link/ether | awk '{print $2}')
SUDO_LOG=$(journalctl _COM=sudo | grep COMMAND | wc -l)
echo -ne "#Architecture: $ARCH\n"
echo -ne "#CPU physical: $CPU\n"
echo -ne "#vCPU: $VCPU\n"
echo -ne "#Memory usage: ${RAM_USED}/${RAM_TOTAL}MB ($RAM_PER)\n"
echo -ne "#Disk usage: $DISK_USED/$DISK_TOTAL ($DISK_PER)\n"
echo -ne "#CPU load: $CPU_LOAD\n"
echo -ne "#Last boot: $LAST_BOOT\n"
echo -ne "#LVM use: $LVM_USE\n"
echo -ne "#Connections TCP : $TCP ESTABLISHED\n:"
echo -ne "#User log: $USER_LOG\n";
echo -ne "#Network: IP $IP_ADDR ($MAC_ADDR)\n"
echo -ne "#Sudo : $SUDO_LOG cmd\n"
```
## CRON
```
sudo systemctl enable cron
sudo crontab -e
```
```
*/10 * * * * bash /root/sleep.sh && bash /root/monitoring.sh | wall
```
```
sudo apt install bc
sudo touch sleep.sh
sudo chmod 755 sleep.sh
sudo nano sleep.sh
```
```
#!bin/bash
# Trouver les minutes et secondes de l'heure de démarrage
BOOT_MIN=$(uptime -s | cut -d ":" -f 2)
BOOT_SEC=$(uptime -s | cut -d ":" -f 3)
# Calculer le nombre de secondes entre le démarrage et la 10eme minute de l'heure la plus proche# Ex: if boot time was 11:43:36
# Ex: si l'heure de démarrage était 11:43:36
# 43 % 10 = 3 minutes depuis la 40eme minute de l'heure
# 3 * 60 = 180 secondes depuis la 40eme minute de l'heure
# 180 + 36 = 216 secondes entre le démarrage et la 10eme minute de l'heure la plus proche
DELAY=$(bc <<< $BOOT_MIN%10*60+$BOOT_SEC)
# Attendre ce nombre de minutes
sleep $DELAY
```
```
sudo apt install curl
```
## UPHP. (php-common, php-cgi, php-cli et php-mysql)
```
sudo curl -sSL https://packages.sury.org/php/README.txt | sudo bash -x
sudo apt update
sudo apt upgrade
sudo apt install php8.1
sudo apt install php-common php-cgi php-cli php-mysql
sudo apt update
sudo apt upgrade
```
## WEB SERVER
make sure to be root
```
systemctl status apache2
sudo apt purge apache2
sudo apt install lighttpd
sudo systemctl start lighttpd
sudo systemctl enable lighttpd
sudo systemctl status lighttpd
add port 8080 / 80 VM
sudo ufw allow http
```
## Testing Lighttpd Server
Browser : http://127.0.0.1:8080/
```
cd /var/www/html
sudo touch info.php
sudo nano info.php
```
```
<?php
phpinfo();
?>
```
```
sudo lighty-enable-mod fastcgi
sudo lighty-enable-mod fastcgi-php
sudo service lighttpd force-reload
```
## Checknew page
Browser : http://127.0.0.1:8080/info.php

## MARIADB
```
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
systemctl status mariadb
sudo mysql_secure_installation

Enter current password for root (enter for none): <Entrée>
Switch to unix_socket authentication [Y/n]: Y
Set root password? [Y/n]: Y
New password: *****
Re-enter new password: *****
Remove anonymous users? [Y/n]: Y
Disallow root login remotely? [Y/n]: Y
Remove test database and access to it? [Y/n]:  Y
Reload privilege tables now? [Y/n]:  Y

$ sudo systemctl restart mariadb
```
```
$ mysql -u root -p
```
```
MariaDB [(none)]> CREATE DATABASE wordpress_db;
MariaDB [(none)]> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'WPpassw0rd';
MariaDB [(none)]> GRANT ALL ON wordpress_db.* TO 'admin'@'localhost' IDENTIFIED BY 'WPpassw0rd' WITH GRANT OPTION;
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> EXIT;
```
## Wordpress
```
 sudo apt install wget
 sudo apt install tar
 ```
 ```
wget http://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
sudo mv wordpress/* /var/www/html/
rm -rf latest.tar.gz wordpress/
```
