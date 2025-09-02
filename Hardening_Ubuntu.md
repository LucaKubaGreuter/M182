# Hardening Ubuntu

## IST-Zustand

```bash
root@f0bf94e45ca7:/# whoami
root
root@f0bf94e45ca7:/# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1   4116  3200 pts/0    Ss   09:13   0:00 /bin/bash
root          10  0.0  0.1   6408  2432 pts/0    R+   09:13   0:00 ps aux
root@f0bf94e45ca7:/# apt list --upgradable
Listing... Done
root@f0bf94e45ca7:/# ufw
bash: ufw: command not found
root@f0bf94e45ca7:/# ssyslog
bash: ssyslog: command not found
root@f0bf94e45ca7:/# rsyslog
bash: rsyslog: command not found
```

---

## Härtungsmassnahmen

| Massnahme                             | Was wurde gemacht?                                                                                                | Warum ist das sicher?                                 | Wie prüfen?                                         |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- | --------------------------------------------------- |
| System aktualisieren                 | `apt update && apt upgrade -y`                                                                                    | Schliesst bekannte Sicherheitslücken in Paketen        | `apt list --upgradable` → sollte leer sein          |
| Root-Login deaktivieren              | `passwd -l root`                                                                                                  | Verhindert direkten Root-Zugriff                      | `su -` → root-Login funktioniert nicht mehr         |
| Benutzer mit eingeschränkten Rechten | `useradd -m -s /bin/bash secureuser && passwd secureuser && usermod -aG sudo secureuser`                          | Minimiert Risiko, dass Angreifer Root-Rechte erlangen | `whoami` nach Login → `secureuser`                  |
| Firewall aktivieren                  | `apt install ufw -y && ufw default deny incoming && ufw default allow outgoing && ufw allow 22/tcp && ufw enable` | Blockiert unerwünschte Zugriffe                       | `ufw status` → zeigt aktive Regeln                  |
| Logging aktivieren                   | `apt install rsyslog -y && service rsyslog start`                                                                 | Ermöglicht Nachvollziehbarkeit von Ereignissen        | `tail -f /var/log/syslog` → Logs werden geschrieben |
| Nur benötigte Dienste laufen lassen  | Mit `ps aux` geprüft, keine unnötigen Dienste gestartet                                                           | Weniger Angriffsfläche                                | `ss -tuln` → nur notwendige Ports offen             |

---

## 2. Reflexion

* **Welche Risiken habe ich adressiert?**

  * Unnötige Dienste und Pakete entfernt → reduziert Angriffsfläche
  * Root-Login deaktiviert → verhindert sofortige Vollzugriffe
  * Firewall aktiviert → nur autorisierte Zugriffe erlaubt
  * Logging → Angriffe nachträglich nachvollziehbar

* **Wie wirksam sind die Massnahmen?**

  * Gegen bekannte Sicherheitslücken sehr wirksam
  * Reduziert automatisierte Angriffe auf Container stark
  * Absolute Sicherheit gibt es nicht (Zero-Day-Exploits oder Social Engineering sind weiterhin möglich)

* **Was könnte man noch verbessern?**

  * Container read-only mounten
  * Secrets nicht im Container speichern
  * IDS/IPS einsetzen
  * Automatisiertes Patch-Management aufsetzen

* **Fazit**

  * Durch systematische Härtung lässt sich die Angriffsfläche drastisch reduzieren
  * Man lernt, welche Massnahmen priorisiert werden müssen und wie man deren Wirkung überprüft
