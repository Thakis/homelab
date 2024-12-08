# Raspberry Pi Ultimate Setup Guide

## 1. Install Raspberry Pi OS
- Download and install from: [Raspberry Pi Official Software](https://www.raspberrypi.com/software/)

## 2. Set Fixed DNS
Edit `/etc/resolv.conf` and add:
```
nameserver 1.1.1.2
nameserver 1.0.0.2
```
More details: [Change DNS Server Guide](https://learnubuntu.com/change-dns-server/)

## 3. System Update
```bash
apt-get update && apt-get upgrade -y && apt autoremove -y
```

## 4. Secure SSH Server
Edit SSH configuration:
```bash
nano /etc/ssh/sshd_config
```
Modify these lines:
- `PermitRootLogin No`
- Change SSH port to `65437`

Restart SSH service:
```bash
/etc/init.d/ssh restart
```
Reference: [SSH Security Video Guide](https://www.youtube.com/watch?v=64XS0HzoS_U)