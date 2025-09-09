# HellPott
Team: Laurin, Yassin & Luca

## Was ist HellPot?

HellPot ist ein *endloser Honeypot* – entwickelt, um HTTP-Bots (zum Beispiel solche, die `robots.txt` ignorieren) in eine Art digitalen Albtraum zu locken. Anstatt eine normale Webseite auszuliefern, erzeugt HellPot einen nahezu echten, endlosen Datenstrom, der die Bots dazu verleitet, immer weiter zu konsumieren, bis ihre "Seele… aufhört zu existieren".
Dahinter steckt eine Markov-Kette, die Fragmente aus Friedrich Nietzsches *The Birth of Tragedy* („Hellenism and Pessimism“) generiert und mit `fasthttp` an die Bots ausliefert.

Zusätzliche technische Features:

* **TOML-Konfiguration** – erlaubt einfache Anpassung
* **JSON-Logging** – strukturierte Ausgabe der Anfragen und Aktionen
* **Hohes Performance-Potenzial** – effizient und ressourcenschonend betrieben

## Funktionen & Nutzen

* **Täuschung von Bots** – HellPot tarnt sich als „echte“ Webseite, verzögert Bots und verschwendet deren Ressourcen.
* **Bot-Falle** – Besonders geeignet für Bot-Traffic, der automatisiert agiert und wenig auf Konformität achtet (z. B. das Ignorieren von `robots.txt`).
* **Leistungsüberlegenheit** – dank `fasthttp` und effizienter Implementierung besonders performant

## Installation auf Ubuntu


```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git make build-essential
```

```bash
wget https://go.dev/dl/go1.22.6.linux-amd64.tar.gz
```

### Nach `/usr/local` entpacken

```bash
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.6.linux-amd64.tar.gz
```

### Go in die Umgebungsvariablen aufnehmen

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

### Installation prüfen

```bash
go version
```

```bash
git clone https://github.com/yunginnanet/HellPot.git
cd HellPot
make
```

Nach dem `make`-Befehl liegt das Binary im Projektordner (`./HellPot`).

### Default starten (YOLO-Modus)

```bash
./HellPot
```

Beim ersten Start wird automatisch eine Config unter
`~/.config/HellPot/config.toml` erstellt.

### Im Browser testen

Standardmässig läuft HellPot auf Port **8080**.
Öffne:

```
http://localhost:8080/wp-login.php
```

### Unit-File erstellen

```bash
sudo nano /etc/systemd/system/hellpot.service
```

### Inhalt einfügen

```ini
[Unit]
Description=HellPot Honeypot
After=network.target

[Service]
ExecStart=/home/kuba/HellPot/HellPot
Restart=always
User=kuba
WorkingDirectory=/home/kuba/HellPot
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=hellpot

[Install]
WantedBy=multi-user.target
```

### Service aktivieren

```bash
sudo systemctl daemon-reload
sudo systemctl enable hellpot
sudo systemctl start hellpot
```

### Status prüfen

```bash
systemctl status hellpot
```

HellPot schreibt strukturierte Logs (JSON).

```bash
journalctl -u hellpot -f
```

## Demo

![HellPot Demo](hellpot.png)