lsb_release -a

---

sed -i 's|http://archive.ubuntu.com/ubuntu|http://old-releases.ubuntu.com/ubuntu|g' /etc/apt/sources.list
apt-get update

# Zuerst die Paketquellen auf das nächste unterstützte Release umstellen
sed -i 's/mantic/noble/g' /etc/apt/sources.list
sed -i 's/23.10/24.04/g' /etc/apt/sources.list

# Paketlisten aktualisieren
# apt update

# Distribution Upgrade durchführen
apt dist-upgrade -y

# System-Release aktualisieren
do-release-upgrade -f DistUpgradeViewNonInteractive

---

# Release-Information anzeigen
cat /etc/os-release
lsb_release -a
cat /etc/lsb-release

# Kernel-Version
uname -a

---

# Überprüfen, ob alle Pakete korrekt installiert sind
dpkg --audit

# Nach defekten Paketen suchen
apt check

# Paket-Cache und Dependencies prüfen
apt-get check

# Sources.list überprüfen
cat /etc/apt/sources.list
ls /etc/apt/sources.list.d/

# Paketlisten aktualisieren (sollte ohne Fehler laufen)
apt update

---

# Wichtige Systemdateien prüfen
ls -la /etc/passwd /etc/group /etc/shadow

# Grundlegende Services (falls vorhanden)
systemctl status

# Dateisystem-Konsistenz
df -h
mount

---

# Essential packages prüfen
dpkg-query -W -f='${Status}\n' | grep -v "install ok installed" | wc -l

# Sollte 0 zurückgeben - wenn nicht, dann:
dpkg-query -W -f='${Package} ${Status}\n' | grep -v "install ok installed"

# Basis-Tools testen
which bash python3 curl wget
python3 --version