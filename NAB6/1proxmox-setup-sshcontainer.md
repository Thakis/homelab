[Mastering SSH in Proxmox: Step-by-Step Guide for Local LXC Connections and Efficient File Transfers!](https://www.youtube.com/watch?v=XPVdaDJNyuM)

# Proxmox

So if you're using Proxmox you need to open up ssh and run the following commands:

1. Setup a root password

```bash
sudo passwd root
```

2. Enable ssh

```bash
nano /etc/ssh/sshd_config
```

3. Change the following line:

```bash
PermitRootLogin without-password
```

to

```bash
PermitRootLogin yes
```

4. Restart ssh

```bash
systemctl restart sshd
```