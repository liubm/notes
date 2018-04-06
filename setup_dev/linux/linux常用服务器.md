1. [PPTP 服务器](#PPTP 服务器)

2. [gitbook](gitbook)

3. [samba](samba)
4. [遗留问题](遗留问题)

   ​
***
##  PPTP 服务器

```shell
#!/bin/bash
#    Setup Simple PPTP VPN server for CentOS 7 on Host1plus
#    Copyright (C) 2015-2016 Danyl Zhang <1475811550@qq.com> and contributors
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.

printhelp() {

echo "
Usage: ./CentOS7-pptp-host1plus.sh [OPTION]
If you are using custom password , Make sure its more than 8 characters. Otherwise it will generate random password for you. 
If you trying set password only. It will generate Default user with Random password. 
example: ./CentOS7-pptp-host1plus.sh -u myusr -p mypass
Use without parameter [ ./CentOS7-pptp-host1plus.sh ] to use default username and Random password
  -u,    --username             Enter the Username
  -p,    --password             Enter the Password
"
}

while [ "$1" != "" ]; do
  case "$1" in
    -u    | --username )             NAME=$2; shift 2 ;;
    -p    | --password )             PASS=$2; shift 2 ;;
    -h    | --help )            echo "$(printhelp)"; exit; shift; break ;;
  esac
done

# Check if user is root
[ $(id -u) != "0" ] && { echo -e "\033[31mError: You must be root to run this script\033[0m"; exit 1; }

export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
clear

yum -y update
yum -y install epel-release
yum -y install firewalld net-tools curl ppp pptpd

echo 'net.ipv4.ip_forward = 1' >> /etc/sysctl.conf
sysctl -p

#no liI10oO chars in password

LEN=$(echo ${#PASS})

if [ -z "$PASS" ] || [ $LEN -lt 8 ] || [ -z "$NAME"]
then
   P1=`cat /dev/urandom | tr -cd abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789 | head -c 3`
   P2=`cat /dev/urandom | tr -cd abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789 | head -c 3`
   P3=`cat /dev/urandom | tr -cd abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789 | head -c 3`
   PASS="$P1-$P2-$P3"
fi

if [ -z "$NAME" ]
then
   NAME="vpn"
fi

cat >> /etc/ppp/chap-secrets <<END
$NAME pptpd $PASS *
END

cat >/etc/pptpd.conf <<END
option /etc/ppp/options.pptpd
#logwtmp
localip 192.168.2.1
remoteip 192.168.2.10-100
END

cat >/etc/ppp/options.pptpd <<END
name pptpd
refuse-pap
refuse-chap
refuse-mschap
require-mschap-v2
require-mppe-128
ms-dns 8.8.8.8
ms-dns 209.244.0.3
proxyarp
lock
nobsdcomp
novj
novjccomp
nologfd
END

ETH=`route | grep default | awk '{print $NF}'`

systemctl restart firewalld.service
systemctl enable firewalld.service
firewall-cmd --set-default-zone=public
firewall-cmd --add-interface=$ETH
firewall-cmd --add-port=22/tcp --permanent
firewall-cmd --add-port=1723/tcp --permanent
firewall-cmd --add-masquerade --permanent
firewall-cmd --permanent --direct --add-rule ipv4 filter INPUT 0 -i $ETH -p gre -j ACCEPT
firewall-cmd --reload

cat > /etc/ppp/ip-up.local << END
/sbin/ifconfig $1 mtu 1400
END
chmod +x /etc/ppp/ip-up.local
systemctl restart pptpd.service
systemctl enable pptpd.service

VPN_IP=`curl ipv4.icanhazip.com`
clear
echo -e "You can now connect to your VPN via your external IP \033[32m${VPN_IP}\033[0m"
echo -e "Username: \033[32m${NAME}\033[0m"
echo -e "Password: \033[32m${PASS}\033[0m"
```

## gitbook
```shell
#! /usr/bin/bash
wget wget https://nodejs.org/dist/v5.4.1/node-v5.4.1.tar.gz
tar -zvxf node-v5.4.1.tar.gz
cd node-v5.4.1
./configure
make
./configure
yum install gcc
yum install gcc-c++
./configure
make
make install
npm install gitbook-cli -g
gitbook -V
```

## samba
```shell
#!/bin/sh
yum -y install samba samba-client
echo -e "thinkive\nthinkive" | smbpasswd -s -a root
mv /etc/samba/smb.conf /etc/samba/smb.conf.bak
touch /etc/samba/smb.conf
cat > /etc/samba/smb.conf  << EOF
[global]
workgroup = WORKGROUP
server string = Samba Server Version %v
netbios name = SambaServer
log file = /var/log/samba/%m.log
max log size = 50
security = user
[thinkive]
path = /
writeable = yes
valid user = root
browseable = yes
EOF
```
## 遗留问题
1. 脚本中应该判断当前系统的版本的操作系统类型
2. 判断当前是否安装该软件
3. 安装软件完成后做一个简单的测试，判断是否安装成功

