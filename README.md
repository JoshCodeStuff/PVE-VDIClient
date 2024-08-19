This is my fork of the project modified for modern linux and python.

## Configuration File

PVE VDI Client **REQUIRES** a configuration file to function. The client searches for this file in the following locations unless overridden with [command line options](#command-line-usage):
* Linux
    * ~/.config/VDIClient/vdiclient.ini
    * /etc/vdiclient/vdiclient.ini
    * /usr/local/etc/vdiclient/vdiclient.ini

## Proxmox Permission Requirements

Users that are accessing VDI instances need to have the following permissions assigned for each VM they access:

* VM.PowerMgmt
* VM.Console
* VM.Audit

## Linux Installation (Raspian)

Run the following commands to install the appropriate prerequisites and properly setup python

    git clone https://github.com/joshpatten/PVE-VDIClient.git
    cd ./PVE-VDIClient/
    python -m venv venv
    source venv/bin/activate
    pip install proxmoxer requests freesimplegui
    sudo chmod +x /usr/local/bin/vdiclient.py
    sudo mkdir -p /etc/vdiclient
    sudo cp vdiclient.ini.example /etc/vdiclient/vdiclient.ini
