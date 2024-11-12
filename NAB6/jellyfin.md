Study Guide for Installing Jellyfin Media Server on Proxmox

 Proxmox HomeServer Teil 30 - Installation von Jellyfin Media Server  = https://www.youtube.com/watch?v=VMfz_1Kd-jk&list=PLRcp6YbTf6Qk3pIZnrKBTEJ8lQl5NZujz


Overview

This guide provides a step-by-step process for installing the Jellyfin Media Server on a Proxmox environment. Jellyfin allows you to centralize your media library, making it accessible from various devices over your network.
Prerequisites

    Proxmox server set up and running.
    Basic knowledge of Linux commands.
    Access to a NAS (Network Attached Storage) for storing media files.

Step-by-Step Installation
1. Create a New Container

    Access Proxmox: Log into your Proxmox server.
    Create Container:
        Assign an ID and hostname.
        Set a password.
        Ensure the container is a privileged container by unchecking the relevant box .

2. Configure Container Settings

    Template: Use Ubuntu 22.04.
    Disk Size: Set to 8 GB, as media files will be stored on the NAS .
    CPU and Memory: Start with 2 CPU cores and 2 GB RAM. Adjust if necessary based on usage .
    Network: Assign a static IP address to avoid issues with changing IPs .

3. Update the Container

    Login: Access the console of the container.
    Update Commands:

    apt-get update
    apt-get upgrade -y
    apt-get autoremove

    This ensures your container is up to date .

4. Install Required Packages

    Create a Mount Point:

    mkdir /mnt/jellyfin

    Install Required Packages:

    apt-get install cifs-utils

    This is necessary for connecting to the NAS .

5. Configure NAS Connection

    Edit fstab:
        Open the fstab file:

        nano /etc/fstab

        Add the following line to mount the NAS:

        //<NAS_IP>/home /mnt/jellyfin cifs username=<username>,password=<password>,uid=1000,gid=1000 0 0

    Replace <NAS_IP>, <username>, and <password> with your NAS details .

6. Mount the NAS

    Mount Command:

    mount -a

    This command will mount all filesystems defined in fstab .

7. Install Jellyfin

    Install Dependencies:

    apt-get install sudo curl

    Install Jellyfin:

    curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash

    This command will automate the installation process .

8. Access Jellyfin

    Start Jellyfin:
        Ensure the service is active:

        systemctl status jellyfin

    Open Web Interface: Navigate to http://<Container_IP>:8096 in your web browser to complete the setup .

9. Configure Media Library

    Add Media: During the setup, specify the directories for your movies, music, and other media .

Conclusion

By following these steps, you can successfully set up a Jellyfin Media Server on your Proxmox server, allowing you to stream your media library across devices. For any issues, refer to the Jellyfin community or documentation for troubleshooting tips .

Feel free to reach out if you have any questions or need further assistance!