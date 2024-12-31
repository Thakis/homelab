# Argon One Raspberry Pi Case Configuration

## Installation

To install the Argon One case software, run the following command:

```bash
curl https://download.argon40.com/argon1.sh | bash
```

## Configuration Commands

- `argonone-config` → Configure fan settings
- `argonone-uninstall` → Uninstall Argon One software

## Customizing Fan Control

Edit the fan configuration file:

```bash
sudo nano /etc/argononed.conf
```

### Sample Fan Configuration

In the configuration file, you can set fan speeds based on temperature:

```
40=10    # At 55°C, set fan to 10% speed
60=55    # At 60°C, set fan to 55% speed
65=100   # At 65°C, set fan to 100% speed
```

After modifying the configuration, restart the service:

```bash
sudo systemctl restart argononed.service
```

## Reference

- Original configuration guide: [Argon One Case PDF](https://www.helmuthinterthuer.de/images/download/argon_one_case.pdf)

## Notes

- Ensure you have appropriate cooling for your Raspberry Pi
- Adjust temperature and fan speed values according to your specific needs and environment