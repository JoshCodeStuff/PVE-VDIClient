This is my fork of the project modified for modern linux and python.

# PVE VDI Client

This project's focus is to create a simple VDI client intended for mass deployment. This VDI client connects directly to Proxmox VE and allows users to connect (via Spice) to any VMs they have permission to access.

Defining multiple Proxmox clusters is possible and can allow end users to easily select which 'server group' they wish to connect to:

![Login Screen](screenshots/login.png)

![Login Screen with OTP](screenshots/login-totp.png)

![VDI View](screenshots/vdiview.png)

## Configuration File

PVE VDI Client **REQUIRES** a configuration file to function. The client searches for this file in the following locations unless overridden with [command line options](#command-line-usage):

* Windows
    * %APPDATA%\VDIClient\vdiclient.ini
    * %PROGRAMFILES%\VDIClient\vdiclient.ini
* Linux
    * ~/.config/VDIClient/vdiclient.ini
    * /etc/vdiclient/vdiclient.ini
    * /usr/local/etc/vdiclient/vdiclient.ini

Please refer to [vdiclient.ini.example](https://github.com/joshpatten/PVE-VDIClient/blob/main/vdiclient.ini.example) for all available config file options

If you encounter any issues feel free to submit an issue report.

## Proxmox Permission Requirements

Users that are accessing VDI instances need to have the following permissions assigned for each VM they access:

* VM.PowerMgmt
* VM.Console
* VM.Audit

## Command Line Usage

No command line options are required for default behavior. The following command line options are available:

    usage: vdiclient.py [-h] [--list_themes] [--config_type {file,http}] [--config_location CONFIG_LOCATION]
                        [--config_username CONFIG_USERNAME] [--config_password CONFIG_PASSWORD] [--ignore_ssl]
    
    Proxmox VDI Client
    
    options:
      -h, --help            show this help message and exit
      --list_themes         List all available themes
      --config_type {file,http}
                            Select config type (default: file)
      --config_location CONFIG_LOCATION
                            Specify the config location (default: search for config file)
      --config_username CONFIG_USERNAME
                            HTTP basic authentication username (default: None)
      --config_password CONFIG_PASSWORD
                            HTTP basic authentication password (default: None)
      --ignore_ssl          HTTPS ignore SSL certificate errors (default: False)

If `--config_type http` is selected, pass the URL in the `--config_location` parameter

## Linux Installation

Run the following commands on a Debian/Ubuntu Linux system to install the appropriate prerequisites

    git clone https://github.com/joshpatten/PVE-VDIClient.git
    cd ./PVE-VDIClient/
    python -m venv venv
    source venv/bin/activate
    pip install proxmoxer requests freesimplegui
    sudo chmod +x /usr/local/bin/vdiclient.py
    sudo mkdir -p /etc/vdiclient
    sudo cp vdiclient.ini.example /etc/vdiclient/vdiclient.ini
