# artixinstall
Fully automated Artix Linux installer for my testing setup

# Usage
1. Boot the Artix Installer.
2. Log in as `root`. The password is `artix`.
3. Use one of the methods listed below.
4. Once you get a green success message, reboot.

## Basic Usage
`curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/artixinstall | sh`

## FDE (Full Disk Encryption) Usage
`curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/cryptinstall | sh`

## Automated Install
This method works for all installation methods mentioned above.

`curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/<artix | crypt>install | sh -s -- [drive [grubtarget]]`
