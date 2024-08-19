This is my fork of the project modified for modern linux and python.

# PVE VDI Client

This project's focus is to create a simple VDI client intended for mass deployment. This VDI client connects directly to Proxmox VE and allows users to connect (via Spice) to any VMs they have permission to access.

Defining multiple Proxmox clusters is possible and can allow end users to easily select which 'server group' they wish to connect to:

![Login Screen](screenshots/login.png)

![Login Screen with OTP](screenshots/login-totp.png)

![VDI View](screenshots/vdiview.png)

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
