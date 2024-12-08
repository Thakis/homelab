
# Tailscale Installation on Raspbian Bookworm

## Video Tutorial
[Tailscale Installation Guide](https://www.youtube.com/watch?v=YTjYXii4WzI)

## Installation Steps

### 1. Add Tailscale's GPG Key
```bash
sudo mkdir -p --mode=0755 /usr/share/keyrings
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
```

### 2. Add Tailscale Repository
```bash
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

### 3. Install Tailscale
```bash
sudo apt-get update && sudo apt-get install tailscale
```

### 4. Start Tailscale
```bash
sudo tailscale up
```

## What Each Step Does

- **Add GPG Key**: Adds the official Tailscale repository key to verify package authenticity
- **Add Repository**: Configures the Tailscale package repository for Raspbian Bookworm
- **Install Tailscale**: Updates package lists and installs Tailscale
- **Start Tailscale**: Initiates the Tailscale connection and begins authentication

## Post-Installation

- You will be prompted to log in to your Tailscale account
- Follow the authentication instructions in the terminal or via the provided URL

## Official Resources

- [Tailscale Raspbian Packages](https://pkgs.tailscale.com/stable/#raspbian-bookworm)
- [Tailscale Documentation](https://tailscale.com/kb/installation)

## Notes

- Ensure you have an active internet connection
- Requires sudo privileges
- Compatible with Raspbian Bookworm