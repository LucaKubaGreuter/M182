# Dokumentation: Installation und Härtung von Wazuh auf Ubuntu

## 1. Systemumgebung

* **Systeme:** 2x Ubuntu Server 22.04 LTS

  * Server 1: Wazuh-Manager
  * Server 2: Wazuh-Agent

---

## 2. Installation von Wazuh

* update und upgrade:

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

* Basis-Tools:

  ```bash
  sudo apt install curl apt-transport-https lsb-release gnupg -y
  ```

1. Repository hinzufügen:

   ```bash
   curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
   echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
   sudo apt update
   ```
2. Wazuh-Manager installieren:

   ```bash
   sudo apt install wazuh-manager -y
   ```
3. Filebeat installieren:

   ```bash
   sudo apt install filebeat -y
   ```
4. Wazuh Dashboard installieren:

   ```bash
   sudo apt install wazuh-dashboard -y
   ```
5. Dienste starten und aktivieren:

   ```bash
   sudo systemctl enable --now wazuh-manager filebeat wazuh-dashboard
   ```

### 2.3 Installation des Wazuh-Agents (Server 2)

1. Paketquelle wie bei Server 1 einrichten
2. Wazuh-Agent installieren:

   ```bash
   sudo apt install wazuh-agent -y
   ```
3. Konfiguration anpassen (`/var/ossec/etc/ossec.conf`):

   ```xml
   <server>
     <address>192.168.10.20</address>
     <port>1514</port>
     <protocol>tcp</protocol>
   </server>
   ```
4. Agent beim Manager registrieren:

   ```bash
   sudo /var/ossec/bin/manage_agents
   ```

   * Agent hinzufügen
   * Key generieren und auf Agent eintragen (`/var/ossec/etc/client.keys`)
5. Agent starten:

   ```bash
   sudo systemctl enable --now wazuh-agent
   ```

---

## 3. Härtungsmassnahmen

* Nur notwendige Ports geöffnet:

  ```bash
  sudo ufw allow 22/tcp
  sudo ufw allow 443/tcp
  sudo ufw allow 1514/tcp
  sudo ufw enable
  ```
* Root Login via SSH deaktiviert (`/etc/ssh/sshd_config`)
* Nur Key basiertes SSH-Login erlaubt
* Fail2ban installiert zur Abwehr von Brute Force Angriffen
* Automatische Sicherheitsupdates aktiviert:

  ```bash
  sudo apt install unattended-upgrades
  ```

### 3.2 Wazuh-spezifische Sicherheit

* Dashboard nur über HTTPS erreichbar
* Zugriff auf das Dashboard auf Administrator IP Bereiche beschränkt (via `nginx`/Firewall)
* Wazuh-Agent-Kommunikation ausschliesslich über TLS gesichert
* Standardpasswörter nach Installation geändert

---

## 4. Fazit

Wazuh hat sich in meiner Installation als **umfassendes OpenSource SIEM und Host Intrusion Detection System (HIDS)** gezeigt. Es bietet eine breite Palette an Funktionen: Log Sammlung, Dateiintegritätsüberwachung, Schwachstellenanalyse und Realtime Sicherheitsalarme. Besonders positiv finde ich die gute Integration in bestehende Linux Umgebungen und die zentrale Verwaltung über das Dashboard.

**Gelernt habe ich dabei:**

* Wie wichtig es ist, Systeme schon vor der Installation zu härten
* Wie Agent <-> Manager Kommunikation funktioniert
* Dass Wazuh trotz vieler Features eine saubere und strukturierte Installation ermöglicht
* Dass ein SIEM System nicht nur technische Überwachung bedeutet, sondern auch organisatorische Sicherheitskonzepte voraussetzt

Insgesamt halte ich Wazuh für ein starkes Werkzeug, besonders für kleinere bis mittlere Unternehmen, die ein kostenfreies, aber leistungsstarkes SIEM einsetzen möchten.