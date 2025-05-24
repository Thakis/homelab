## in progress

# SSH-Server (falls Remote-Zugriff gewünscht)
apt install -y openssh-server
systemctl enable ssh

# Fail2ban für zusätzliche Sicherheit
apt install -y fail2ban
systemctl enable fail2ban

# System aktualisieren
apt update && apt upgrade -y

# Basis-Tools installieren
apt install -y \
  curl wget git vim nano htop tree \
  unzip zip tar gzip \
  net-tools iputils-ping dnsutils \
  ca-certificates gnupg lsb-release \
  software-properties-common apt-transport-https \
  sudo cron logrotate rsyslog