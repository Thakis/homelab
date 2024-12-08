# Thunderbird Docker Container

## Overview
This Docker container provides a lightweight, portable installation of Thunderbird email client with a user-friendly web interface.

## Features
- Thunderbird email client running in a Docker container
- Lightweight and easy to deploy
- Configurable through environment variables
- Supports multiple architectures
- Built-in web interface for easy access

## Supported Architectures
- x86-64
- ARM64
- ARM32v7

## Quick Start

### Docker Run
```bash
docker run -d \
  --name=thunderbird \
  -p 5800:5800 \
  -p 5900:5900 \
  -v /path/to/config:/config \
  -v /path/to/data:/data \
  jlesage/thunderbird
```

### Docker Compose
```yaml
version: '3'
services:
  thunderbird:
    image: jlesage/thunderbird
    container_name: thunderbird
    ports:
      - 5800:5800
      - 5900:5900
    volumes:
      - /path/to/config:/config
      - /path/to/data:/data
    restart: unless-stopped
```

## Environment Variables

### Basic Configuration
- `USER_ID`: User ID owning the config directory (default: `1000`)
- `GROUP_ID`: Group ID owning the config directory (default: `1000`)
- `TZ`: Timezone (e.g., `America/New_York`)

### Display Configuration
- `DISPLAY_WIDTH`: Width of the GUI (default: `1280`)
- `DISPLAY_HEIGHT`: Height of the GUI (default: `720`)
- `DARK_MODE`: Enable dark mode (default: `0`)

### Advanced Settings
- `KEEP_APP_RUNNING`: Keep the application running after crash (default: `0`)
- `APP_NICENESS`: Nice level of the application (default: `0`)

## Volume Mappings
- `/config`: Thunderbird configuration and data
- `/data`: Additional data storage

## Accessing the Interface
- Web Interface: `http://host-ip:5800`
- VNC Viewer: `host-ip:5900`

## Security Considerations
- Use strong, unique passwords
- Keep the container and Thunderbird updated
- Use volumes for persistent data

## Updating the Container
```bash
docker pull jlesage/thunderbird
docker stop thunderbird
docker rm thunderbird
# Then run the container again with the same parameters
```

## Troubleshooting

### Common Issues
- Check docker logs: `docker logs thunderbird`
- Verify volume mappings
- Ensure port 5800 and 5900 are not in use

### Performance Optimization
- Adjust `USER_ID` and `GROUP_ID` to match host system
- Use appropriate timezone settings

## Advanced Configuration

### Custom Thunderbird Preferences
You can add custom preferences by creating a `prefs.js` file in the `/config` volume.

### Extensions and Add-ons
- Install extensions through the Thunderbird interface
- Persistent across container restarts

## Limitations
- No direct system integration
- Requires Docker runtime
- Limited to container's resources

## Contributing
- Report issues on GitHub
- Submit pull requests
- Provide feedback

## Resources
- [Docker Hub Repository](https://hub.docker.com/r/jlesage/thunderbird)
- [GitHub Repository](https://github.com/jlesage/docker-thunderbird)
- [Thunderbird Official Website](https://www.thunderbird.net/)

## License
Check the GitHub repository for specific licensing information.

## Disclaimer
- Use at your own risk
- No warranty provided
- Community-supported project