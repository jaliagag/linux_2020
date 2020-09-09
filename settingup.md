# Setting up CentOS

source: <https://www.youtube.com/watch?v=iNKignLc_XM>

```bash
# check centos version
cat /etc/centos-release
# or
cat /etc/redhat-release

# installed epel-release repository - source: https://www.shellhacks.com/epel-repo-centos-8-7-6-install/
rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# set static ip addr
vi /etc/sysconfig/network-scripts/ifcfg-<networkAdapterName>

# https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-configure-static-ip-address-in-centos-7-rhel-7-fedora-26.html
# set values as
BOOTPROTO="static"
ONBOOT="yes"
IPADDR="<whateverIPYouWant>192.168.0.123"
NETMASK="255.255.255.0"
GATEWAY="192.168.0.1"
DNS1="8.8.8.8"
DNS2="8.8.4.4"

# restart the network
service network restart

# install net-tools
yum install -y net-tools

# we can now use ifconig
# check host name
echo $HOSTNAME
hostname

# edit hostname
vi /etc/hostname

# update all
yum update -y

# command line web process links
yum install -y links

# install apache webserver
yum install -y httpd

# allow HTTP service through the firewall
firewall-cmd --add-service=http

# reload firewall to apply changes
firewall-cmd --reload

# start httpd service
systemctl start httpd.service

# make httpd service start automatically on system start
systemctl enable httpd.service

# verify apache's httpd service
links 127.0.0.1

# MariaDB installation
yum -y install mariadb-server mariadb

# start mariadb
systemctl start mariadb.service

# make mariadb start on system start
systemctl enable mariadb.service

# allow mariadb service through firewall
firewall-cmd --add-service=mysql

# secure mariadb server - choose "y" for every option
/usr/bin/mysql_secure_installation

# SSH server is already installed - configure SSH
vi /etc/ssh/ssh_config

# Modify protocol line should look like this 
Protocol 2

# Installing GCC - GNU Compiler Collection
yum install -y gcc

gcc --version

# Install Java
yum install -y java

java -version

# install wget
yum install -y wget

# install telnet
yum install -y telnet

# Install epel repository
wget https://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm

# 7zip installation - unzip/unrar files
yum -y install p7zip

# to access NTFS and windows file servers
yum install -y ntfs-3g

# vsftp server - secure file transfer
yum install -y vsftpd

# edit config file
vi /etc/vsftpd/vsftpd.conf

# anonymus enable should be no
anonymous_enable=NO
local_enable=YES
chroot_local_users=YES

# allow services through the firewall
firewall-cmd --add-prot=21/tcp
firewall-cmd --reload
systemctl restart vsftpd
systemctl enable vsftpd

# install sudo
visudo

# selinux-policy
yum -y install selinux-policy
getenforce # enforcing
setenforce 0 # permissive
setenforce 1 # enforcing

# rootkithunter - scan rootkit, sort of anyvirus
yum -y install rkhunter
rkhunter --check

#
# Pelado nerd <https://www.youtube.com/watch?v=IDDmqlN-hF0>
# install ssh server
yum install -y openssh-server

systemctl enable ssh.service

# generar un certificado
ssh-keygen

# copiar certificado público en el servidor
cat .ssh/id_rsa.pub

# Copiar todo el certificado
# ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDh5qapn3lYwTUJ7PyEiq908NJOOW2f5hGpeva3xUTC6/Kty6aE0jSayhHRE2TnaZhSm7jBDYQGrlHXMSrHqs2Do+3CKZnepHka9ryrHWdgR9s6BPtVy8gRkjpPjCqNkpzlnFBo3fOaNjKmfzqu9owCINQVYKswDLOGud0iH7B6PdzWi6B8mA8GNgceJ6B/bDWsNnm9v1AFGUWlZjsIAGu+cU0PWKpmg0yFbfcxYeOdAv/ZsOxisW95WOXB6uNFch8l311CVSPf6TvjP6NwDzmLiCUXuQNjQcGKoGHsJF3MWCYZyDqd8fLnt9XKfAHbAo6Y0+jBFDzQPE5UKe0wSYO5 root@bestCentosEver
# pegarlo en el servidor 
vi .ssh/authorized_keys

# No debería tener login
# Otra forma más copada
ssh-copy-id root@<ip>:

# Correr un comando en el servidor sin iniciarlo
ssh -t root@<ip> <comando a correr>

# crear un proxy SOCKS
ssh -D 9999 root@<ip>

# nginx
apt-get install -y nginx

# we can now use the public ip to loginto the nginx web-server

cd /etc/nginx
# Sites-available: 
cp default jose.copado.com
vi jose.copado.com

# en la línea server name
server_name jose.copado.com;
root /var/www/jose;

# eliminamos listen 80 default_server y ponemos:

# Sites-enabled: tiene un link simbolico, que apunta a otro lado.
ln -s ../sites-available/jose.copado.com .

# recargar nginx
nginx -s reload

```

```bash
# Connecting to the internet:
nmcli d
nmuti

# ver los usuarios
w 
# fecha actual
date
# calendario
cal
 # cambiar la contraseña del usuario
passwd
#Cambio de hora en servidores
hwclock–set –date=”2013/06/13 16:02:15″
# Ver log de errores del sistema
dmesg
# Para ubicar la version del sistema operativo en linux:
lsb_release –a
# Muestra los datos del Kernell:
uname – a 
#Muestra los datos de las aplicaciones instaladas:
rpm -qa | grep (nombre de la aplicación)
# Para revisar version de  Linux:
cat /etc/issue
# Revisar versión del sistema operativo Linux
more /proc/version
# Ver capacidad de File Systems en servidores en GB
df -h 
# Montar un pen drive como partición
mount /dev/sdb1 /mnt/stickusb
# Ubicar los archivos
find / -name + NOMBREDELARCHIVO

# /etc/fstab información de nuestros FS, punto de montura, tipo de FS se agrega ahí
# ampliar
# volume group display
vgdisplay
# Free PE size, espacio libre que podemos usar par asignar a otros volúmenes
# info de cada uno del los FS
lgdisplay
# extender el logical volume
lvextend -L+1G /dev/root-vg/tmp1
resize2fs /dev/root-vg/tmp1
```

