# Raspberry Pi NFS Mounting and Backup Guide

## Reference
[Linux Tips and Tricks Installation Guide](https://www.linux-tips-and-tricks.de/en/installation/)

## Prerequisites
- Raspberry Pi
- NFS Server (in this example, a Synology DS923+ NAS)
- Network connectivity

## Step 1: Mount NFS Share

### Manually Mount NFS Share
```bash
sudo mount -t nfs 192.168.178.53:/volume2/raspberry /mnt/nfs_ds923
```

### Permanent Mount Configuration
Add to `/etc/fstab`:
```
192.168.178.53:/volume2/raspberry /mnt/nfs_ds923 nfs defaults 0 0
```

## Step 2: Perform Backup

### Run Backup Script
```bash
sudo bash ./raspiBackup.sh /mnt/nfs_ds923
```

## Configuration

### Backup Configuration File
Location: `/usr/local/etc/raspiBackup.conf`

## Key Components

- **NFS Mount Point**: `/mnt/nfs_ds923`
- **NFS Server IP**: 192.168.178.53
- **NFS Share Path**: `/volume2/raspberry`

## Troubleshooting

- Ensure NFS server is accessible
- Check network connectivity
- Verify mount permissions
- Confirm NFS service is running on the server

## Recommended Practices

- Create the mount point directory before mounting
- Use `sudo` for mount operations
- Regularly test backup integrity
- Keep backup configuration secure

## Notes

- Adjust IP address and paths to match your specific network setup
- Ensure you have necessary permissions to mount and backup
- Consider automating the backup process with cron jobs

## Additional Resources

- [NFS Mount Documentation](https://linux.die.net/man/5/nfs)
- [Raspberry Pi Backup Strategies](https://www.raspberrypi.com/documentation/computers/configuration.html)