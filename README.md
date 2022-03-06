# LinuxPrivilegeEscalation

Bu dökümanı, linux işletim sistemlerine yönelik yetki yükseltme açıklarının analizlerini gerçekleştirmek üzere kopya kağıdı olması üzerine kaleme aldım.
Bu içerik temel ve bir kaba kılavuzdur. Linux değişken olduğundan, her komut her sistem üzerinde çalışmayabilir.


**Sistem Bilgisi**

**Dağıtım türü nedir ? Hangi sürüm ?**

```
cat /proc/version || uname -a 2> /dev/null
lsb_release -a 2> /dev/null
cat /etc/*-release 
cat /etc/lsb-release 
cat /etc/redhat-release
cat /etc/issue
```
![3](https://user-images.githubusercontent.com/101067919/156942673-09f5be4b-b9df-444e-814b-1575e64fbfb2.png)


**Çekirdek sürümü nedir ?**

```
cat /prov/version
uname -a 
uname -mrs
rpm -q kernel
msesg | grep Linux
ls /boot | grep vmlinuz-
```
![4](https://user-images.githubusercontent.com/101067919/156942862-254dbd1a-2ded-416b-aec9-0e171046fafb.png)

**Çevresel değişken analizleri**

```
cat /etc/bash.bashrc
cat /etc/
env
set
```
![5](https://user-images.githubusercontent.com/101067919/156943101-4e52f412-fe01-42a9-95ee-0dd82c9c52aa.png)

**Uygulama ve Hizmetler**

```
ps auxf 
ps auxf |grep root (hangi hizmetlerin root tarafından çalıştırıldığını görüntülemek için)
ps -ef
ps -ef | grep root (hangi hizmetlerin root tarafından çalıştırıldığını görüntülemek için)
top
cat /etc/services
```
![6](https://user-images.githubusercontent.com/101067919/156943957-c2559240-f6c9-40f8-a840-cf115fefe6ad.png)

**Bir metin belgesi içerisinde saklanabilecek kullanıcı adı ve/veya şifre var mı ?**
```
grep -i user [file]
grep -i pass [file]
grep -C 5 "password" [file]
```

**Yüklü uygulamalar neler, Çalışıyor mu ? Sürümleri ne ?**
```
ls -la /usr/bin/
ls -la /sbin/
dpkg -l
ls -la /var/cache/apt/archives
ls -la /var/cache/yum
```
![7](https://user-images.githubusercontent.com/101067919/156944636-a196add4-16b4-4b70-8ea0-e1e8bb938989.png)


**İletişim ve Ağ**

**NIC kontrolü**
```
/sbin/ifconfig -a
cat /etc/network/interfaces
```
![8](https://user-images.githubusercontent.com/101067919/156944974-ac0421e5-fc4e-4b3f-ab35-fe3f0f1dceb1.png)

**DHCP, DNS ve Ağ Geçidi**
```
cat /etc/resolv.conf
cat /etc/networks
hostname
dnsdomainname
```
![9](https://user-images.githubusercontent.com/101067919/156945093-e9e0ef7e-f452-4968-a13d-27be38a5c263.png)

**Başka hangi kullanıcılar ve ana bilgisayarlar sistem ile etkileşimde bulunuyor ?**
```
w
last
netstat
```
![10](https://user-images.githubusercontent.com/101067919/156945228-c0dc350f-80b9-4dad-b37b-7cdc7edf45f0.png)

**Önbellek kontrolü IP/Mac adresleri**
```
arp
route
/sbin/route -nee
```
![11](https://user-images.githubusercontent.com/101067919/156945373-10c4902f-92f4-428c-9b9c-115b444f8c2e.png)

**Kullanıcı bilgilerine erişme**

**Yetki öğrenme vb. için kullanılabilir.**
```
id
who
last
sudo -l
cat /etc/sudoers
```

**Hangi hassas dosyalar bulunabilir?**
```
cat /etc/passwd
cat /etc/group
cat /etc/shadow
ls -la /var/mail/
ls -la /root/
ls -la /home/
```

**Şifre, veritabanı ve yapılandırma dosyaları...**
```
cat /var/apache2/config.inc
cat /var/lib/mysql/mysql/user.MYD
cat /root anaconda-ks.cfg
```

**Özel anahtar bilgileri**
```
cat ~/.ssh/authorized_keys
cat ~/.ssh/identity.pub
cat ~/.ssh/identity
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa.pub
cat ~/.ssh/id_dsa
cat /etc/ssh/ssh_config
cat /etc/ssh/sshd_config
cat /etc/ssh/ssh_host_dsa_key.pub
cat /etc/ssh/ssh_host_dsa_key
cat /etc/ssh/ssh_host_rsa_key.pub
cat /etc/ssh/ssh_host_rsa_key
cat /etc/ssh/ssh_host_key.pub
cat /etc/ssh/ssh_host_key
```

**Dosya Sistemleri**
```
ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null
ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null
find /etc/ -readable -type f 2>/dev/null  
find /etc/ -readable -type f -maxdepth 1 2>/dev/null
```

**/var/**
```
ls -alh /var/log
ls -alh /var/mail
ls -alh /var/spool
ls -alh /var/spool/lpd
ls -alh /var/lib/pgsql
ls -alh /var/lib/mysql
cat /var/lib/dhcp3/dhclient.leases
```
**Günlük dosya analizi**
```
cat /etc/httpd/logs/access_log
cat /etc/httpd/logs/access.log
cat /etc/httpd/logs/error_log
cat /etc/httpd/logs/error.log
cat /var/log/apache2/access_log
cat /var/log/apache2/access.log
cat /var/log/apache2/error_log
cat /var/log/apache2/error.log
cat /var/log/apache/access_log
cat /var/log/apache/access.log
cat /var/log/auth.log
cat /var/log/chttp.log
cat /var/log/cups/error_log
cat /var/log/dpkg.log
cat /var/log/faillog
cat /var/log/httpd/access_log
cat /var/log/httpd/access.log
cat /var/log/httpd/error_log
cat /var/log/httpd/error.log
cat /var/log/lastlog
cat /var/log/lighttpd/access.log
cat /var/log/lighttpd/error.log
cat /var/log/lighttpd/lighttpd.access.log
cat /var/log/lighttpd/lighttpd.error.log
cat /var/log/messages
cat /var/log/secure
cat /var/log/syslog
cat /var/log/wtmp
cat /var/log/xferlog
cat /var/log/yum.log
cat /var/run/utmp
cat /var/webmin/miniserv.log
cat /var/www/logs/access_log
cat /var/www/logs/access.log
ls -alh /var/lib/dhcp3/
ls -alh /var/log/postgresql/
ls -alh /var/log/proftpd/
ls -alh /var/log/samba/
```
