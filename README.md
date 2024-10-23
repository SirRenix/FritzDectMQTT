# FritzDectMQTT

[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md) | [![de](https://img.shields.io/badge/lang-de-green.svg)](README.de.md)

## Changelog

You can find the full changelog of this project [here](CHANGELOG.md).

---

This script reads data from DECT sockets connected to a Fritzbox via the HTTP API fritzconnection and sends it to an **MQTT Broker**. The project is primarily designed for use on a Raspberry Pi but can be run on any Linux machine with Python 3.10 or higher. Also it is possible to run the script in an Docker Container.

---

## Features

- **MQTT Protocol**: Sends data from connected devices.
- **Structured Code**: Improved code organization for better maintainability.
- **Docker Test Environment**: Tested in a Docker container.
- **Threading**: Parallel processing support.
- **FritzHomeAutomation**: Basic code for controlling sockets integrated.
- **Publisher/Subscriber**: Methods for publishing and receiving MQTT messages.
- **Device Status**: Integrated `GetDeviceStats` for socket information.
- **Status**: The project is still in the testing phase.

---

## Planned Changes

- English README and multi-language support.
- Documentation of Docker functionality with an MQTT server.
- Expand code documentation.
- Improve error handling to cover more cases.
- Docker install docu (QNAP NAS)

---

## Setup Instructions

1. Fill in **_secrets.yaml** with Fritzbox credentials and rename to `secrets.yaml`.
2. [Set up a Python virtual environment](#python-virtual-environment-setup).
3. [Configure log rotation](#log-rotation).
4. [Set up as a systemd service for auto-start](#systemd-service-setup).

---

### Python Virtual Environment Setup

To create an isolated Python environment for the project:

```bash
#python virtual environment install
sudo apt-get install python3-venv

#move to project directory
cd ~/FritzDectMQTT

# virtual environment init
python -m venv ~/FritzDectMQTT/venv

# activate env
source ~/FritzDectMQTT/venv/bin/activate

# install dependencies
pip install -r requirements.txt

# modify service
The path in `fritzdectmqtt.service` - service file must be changed or modified with your username of the system.

---

### Logfile-Rotation
to avoid the computer system being full of log files or large files.
It is recommended to use logrotate under linux.

install:

    sudo apt install logrotate

copy file ``fritzdectmqtt.logrotate``:

    sudo cp cli/fritzdectmqtt.logrotate /etc/logrotate.d/fritzdectmqtt 

---

### Service (systemctl)
run script as a background service:

# System service copy
sudo cp cli/fritzdectmqtt.service /etc/systemd/system

# activate
sudo systemctl enable fritzdectmqtt.service

# start
sudo systemctl start fritzdectmqtt.service

# check status 
sudo systemctl status fritzdectmqtt.service

# stop
sudo systemctl stop fritzdectmqtt.service

---

*The project is in an early phase, the error detection is still of a basic quality.*
