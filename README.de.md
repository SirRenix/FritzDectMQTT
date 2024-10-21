# FritzDectMQTT

Dieses Script liest per HTTP-API "fritzconnection" die Daten von an einer Fritzbox angeschlossenen DECT-Steckdosen aus und sendet sie an einen **MQTT Broker**. Das Projekt ist primär für den Einsatz auf einem Raspberry Pi konzipiert, kann aber auf jedem Linux-Rechner mit Python 3.10+ verwendet werden oder Docker Container.

---

## Funktionsübersicht Stand 10.2024

- **MQTT Protokoll**: Implementierung für das Senden von Steckdosendaten.
- **Strukturierter Code**: Verbesserung der Code-Organisation für bessere Wartbarkeit.
- **Docker-Testumgebung**: Script in Docker-Container getestet.
- **Threading**: Unterstützung für parallele Abläufe.
- **FritzHomeAutomation**: Basiscode zum Schalten von Steckdosen integriert.
- **Publisher/Subscriber**: Methoden für das Versenden und Empfangen von MQTT-Nachrichten.
- **Gerätestatus**: Integration von `GetDeviceStats` für Steckdoseninformationen.
- **Aktueller Status**: Das Projekt befindet sich noch in der Testphase.

---

## Geplante Änderungen

- README und Dokumentation auf Englisch sowie Mehrsprachigkeit.
- Dokumentation der Docker-Funktionalität in Verbindung mit einem MQTT-Server.
- Erweiterung der Code-Dokumentation.
- Verbesserung der Fehlerbehandlung, um alle möglichen Fehlerfälle abzudecken.
- Docker installations Anleitung (QNAP NAS)

---

## Einrichtung

1. **_secrets.yaml**: Datei mit den Fritzbox-Zugangsdaten ausfüllen und in `secrets.yaml` umbenennen.
2. **Virtuelles Python-Environment**: [Anleitung weiter unten](#python-virtuelles-environment-venv-einrichten).
3. **Logfile-Rotation**: [Anleitung zur Einrichtung](#logfile-rotation).
4. **Systemdienst einrichten**: Automatischer Start des Scripts über `systemctl`. [Details](#service-systemctl).

---

### Python Virtuelles Environment (venv) einrichten

Um eine isolierte Python-Umgebung für das Projekt zu erstellen:

```bash
# Python virtual environment installieren
sudo apt-get install python3-venv

# In das Projektverzeichnis wechseln
cd ~/FritzDectMQTT

# Virtuelles environment initialisieren
python -m venv ~/FritzDectMQTT/venv

# Environment aktivieren
source ~/FritzDectMQTT/venv/bin/activate

# Abhängigkeiten installieren
pip install -r requirements.txt

# Service anpassen
Der Pfad in der `fritzdectmqtt.service` - Datei muss entsprechend dem Usernamen angepasst werden.

---

### Logfile-Rotation
Um zu vermeiden, dass das Filesystem des Rechners durch die Logfiles voll läuft, wird die Logrotate Funktionalität des 
Linux-OS verwendet.

Falls ``logrotate`` noch nicht installiert ist, installiere es:

    sudo apt install logrotate

Kopiere das File ``fritzdectmqtt.logrotate``:

    sudo cp cli/fritzdectmqtt.logrotate /etc/logrotate.d/fritzdectmqtt 

---
### Service (systemctl)
Um das Script als Hintergrunddienst laufen zu lassen:


# Systemdienst umkopieren
sudo cp cli/fritzdectmqtt.service /etc/systemd/system

# Aktivieren
sudo systemctl enable fritzdectmqtt.service

# Starten
sudo systemctl start fritzdectmqtt.service

# Status prüfen
sudo systemctl status fritzdectmqtt.service

# Stoppen
sudo systemctl stop fritzdectmqtt.service


---

*Das Projekt ist in einer frühen Phase, die Fehlererkennung ist noch in einer relativ rudimentären Qualität.*