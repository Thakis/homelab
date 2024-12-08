# Homelab and Proxmox Configuration Guides

## Videos

- [Quick and Easy SSL Certificates for Your Homelab!](https://www.youtube.com/watch?v=qlcVx-k-02E&list=WL&index=7)
- [Proxmox HomeServer Part 20: Set Up Wake On LAN](https://www.youtube.com/watch?v=jR7SxIPpw1M&list=WL&index=7)
- [Proxmox HomeServer Part 21: Enable Automatic Restart](https://www.youtube.com/watch?v=Vlwajgn9Yxo&list=PL4FsWECgxEtEn3Zhc4E0PDzd57qtpQeSn&index=5)
- [Don’t run Proxmox without these settings!](https://www.youtube.com/watch?v=VAJWUZ3sTSI)

## Wake On LAN Configuration

To set up Wake On LAN for your Proxmox server:

1. Install `ethtool`:
   ```bash
   apt install ethtool -y
   ```

2. Check your network configuration:
   ```bash
   ip address
   ```

3. Use `ethtool` to verify the network adapter name and configure Wake On LAN:
   ```bash
   ethtool <network_adapter_name>
   ethtool -s <network_adapter_name> wol g
   ```

4. Edit the network interfaces file to make the configuration persistent:
   ```bash
   nano /etc/network/interfaces
   ```
   Add the following line under the respective adapter:
   ```
   post-up /usr/sbin/ethtool -s <network_adapter_name> wol g
   ```

**Note:** Currently, the setup might not be functional despite following all the steps. #WorkInProgress

