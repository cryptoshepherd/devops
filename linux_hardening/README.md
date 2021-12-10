# Auto Update Vulns
sudo apt install unattended-upgrades


sudo dpkg-reconfigure --priority=low unattended-upgrades --> YES

/etc/apt/apt.conf.d$ cat 20auto-upgrades 

APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";

/etc/apt/apt.conf.d$ cat 50unattended-upgrades

To Test changes in 50unattended-upgrades:

/etc/apt/apt.conf.d$ sudo unattended-upgrade --dry-run --debug


# New User and Groups 

useradd satoshi -m -s /bin/bash -c "satoshi's vision"
usermod -aG sudo,adm,docker satoshi
passwd 'STRONGPASSWD'


# SSH Key instead passwd for clients

ssh-keygen -b 4096 -C "satoshi@satohivision.local"
ssh-copy-id -i .ssh/id_rsa.pub remoteuser@remoteserver

# SSHD config file
PermitRootLogin no
PasswordAuthentication no


# File2ban
sudo apt-get install fail2ban
sudo systemctl enable fail2ban.service
sudo nano /etc/fail2ban/jail.local


´´´
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
findtime = 300
bantime = 3600
ignoreip = 127.0.0.1


sudo systemctl restart fail2ban.service


sudo fail2ban-client status
sudo fail2ban-client status sshd
sudo iptables -L
sudo fail2ban-client set sshd unbanip 192.168.5.25

