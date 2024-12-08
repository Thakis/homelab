> To map an NFS (Network File System) share to your Raspberry Pi, you need to follow a series of steps. This process involves installing the necessary software, configuring the NFS server and client, and then mounting the NFS share. Here’s a step-by-step guide:

### 1. Install NFS Utilities

> Ensure that both the NFS server (if you have control over it) and the Raspberry Pi have the necessary NFS utilities installed.

#### On the NFS Server:
Install the NFS server package. This step is required only if you are setting up your own NFS server.
```sh
sudo apt update
sudo apt install nfs-kernel-server
```

#### On the Raspberry Pi (NFS Client):
Install the NFS client package.
```sh
sudo apt update
sudo apt install nfs-common
```

### 2. Configure the NFS Server

> If you are administering the NFS server, configure the directories you want to share.

1. **Edit the Exports File:**
   Open the exports file to define the directories to be shared.
   ```sh
   sudo nano /etc/exports
   ```

2. **Add Export Entries:**
   Add a line for each directory you want to share. For example:
   ```sh
   /path/to/share 192.168.1.0/24(rw,sync,no_subtree_check)
   ```
   - `/path/to/share`: The directory you want to share.
   - `192.168.1.0/24`: The network allowed to access the share.
   - `(rw,sync,no_subtree_check)`: Options to control the behavior of the NFS share.

3. **Export the Shared Directories:**
   Apply the changes by exporting the shared directories.
   ```sh
   sudo exportfs -a
   ```

4. **Restart the NFS Server:**
   Restart the NFS service to apply the new configuration.
   ```sh
   sudo systemctl restart nfs-kernel-server
   ```

### 3. Mount the NFS Share on the Raspberry Pi

> On the Raspberry Pi, you will mount the NFS share to a local directory.

1. **Create a Mount Point:**
   Create a directory where the NFS share will be mounted.
   ```sh
   sudo mkdir -p /mnt/nfs_share
   ```

2. **Mount the NFS Share:**
   Mount the NFS share to the directory you created.
   ```sh
   sudo mount -t nfs SERVER_IP:/path/to/share /mnt/nfs_share
   ```
   - `SERVER_IP`: The IP address of the NFS server.
   - `/path/to/share`: The directory on the NFS server that is shared.
   - `/mnt/nfs_share`: The local directory where you want to mount the NFS share.

3. **Verify the Mount:**
   Ensure the NFS share is mounted correctly.
   ```sh
   df -h
   ```

### 4. Automate Mounting at Boot

> To ensure the NFS share mounts automatically at boot, add an entry to the `/etc/fstab` file.

1. **Edit the fstab File:**
   Open the `/etc/fstab` file.
   ```sh
   sudo nano /etc/fstab
   ```

2. **Add the NFS Entry:**
   Add a line for the NFS mount.
   ```sh
   SERVER_IP:/path/to/share /mnt/nfs_share nfs defaults 0 0
   ```

3. **Test the fstab Configuration:**
   Unmount the NFS share and test the fstab configuration.
   ```sh
   sudo umount /mnt/nfs_share
   sudo mount -a
   ```

### Conclusion

> By following these steps, you should be able to map an NFS share to your Raspberry Pi, providing a reliable and Linux-compatible network storage solution for your backups.

For further reference, consult:
- [NFS HowTo on Ubuntu](https://help.ubuntu.com/community/SettingUpNFSHowTo)
- [NFS Configuration Guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-22-04)

This approach should help you avoid the limitations of CIFS and provide a robust solution for your backup needs.