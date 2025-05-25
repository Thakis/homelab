# MyJDownloader Installation on Synology NAS

This package enables easy installation and integration of **MyJDownloader** on a Synology NAS system. It is based on the following sources:

- [YouTube Tutorial](https://www.youtube.com/watch?v=FXPuhD3sp7A)
- [SynologyMe Project Download](https://source.synology.me/mybb2/mydownloads.php?action=view_down&did=111)

## Included Features

- Runs on Synology's **local default port 80**
- Requires **email address and password** for [https://my.jdownloader.org/login.html](https://my.jdownloader.org/login.html)
- Allows defining a custom **download path** on the NAS
- Uses **portable Oracle Java 8** (included in the installation)

## Notes

- **No separate Java installation or JAVA_HOME environment variable** is required — the necessary Java runtime is downloaded during installation.

## Backup

- A **backup is created automatically** during an upgrade or uninstallation at `/tmp/backupJD/...`.

## Migration

- Existing server data is **automatically migrated** during an upgrade.

## Permissions – Important Notice

If downloads fail after installation due to **insufficient permissions**, please adjust the **permissions settings** as shown in the [example image](https://source.synology.me/mybb2/attachment.php?aid=200).
