# ncae-2025

Scripts for NCAE Cyber Games 2025

## 1 First steps

### 1.1 Change to root user (will prevent GUI login):
```sh
sudo su -l
passwd
apt uninstall sudo # or whichever package manager
```

### 1.2 Setup firewall

#### 1.2.1 Generic setup:
```sh
curl https://raw.githubusercontent.com/Liassica/ncae-2025/refs/heads/main/scripts/iptables | bash
```

#### 1.2.2 Extra ports, e.g. SSH (22) & web (80, 443):
```sh
curl https://raw.githubusercontent.com/Liassica/ncae-2025/refs/heads/main/scripts/iptables | bash -S -W
```

#### 1.2.3 Specific host, e.g. SSH from 10.10.10.10:
```sh
curl https://raw.githubusercontent.com/Liassica/ncae-2025/refs/heads/main/scripts/iptables | bash -s 10.10.10.10
```

## 2 Competition services

### 2.1 SSH

#### 2.1.1 Install OpenSSH server if not already installed:
```sh
apt install openssh-server # w/e PM, may be just 'openssh' dep on distro
```

#### 2.1.2 Configure server by editing `/etc/ssh/sshd_config`

The comments aren't necessary in the real config:
```sh
echo "# Force key login
PasswordAuthentication no
AuthenticationMethods publickey

# Disable root SSH access
PermitRootLogin no

# Use root-configured authorized keys
AuthorizedKeysFile /etc/ssh/authorized_keys.d/%u" >> /etc/ssh/ssh_config
```

#### 2.1.3 Set up authorized users

For each scoring user, place their public SSH key in `/etc/ssh/authorized_keys.d/<user>`

#### 2.1.4 Start/restart service:
```sh
systemctl enable --now sshd.service
```
```sh
systemctl restart sshd.service
```

### 2.2 Other services

See the other team members' notes and documentation :)

## 3 Additional hardening

### 3.1 Kernel hardening

#### 3.1.1 sysctl:
```sh
curl https://raw.githubusercontent.com/Liassica/ncae-2025/refs/heads/main/scripts/sysctl | bash
```

#### 3.1.2 kernel command line:
```sh
curl https://raw.githubusercontent.com/Liassica/ncae-2025/refs/heads/main/scripts/cmdline | bash
```
