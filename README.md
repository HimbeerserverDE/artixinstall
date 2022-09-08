# artixinstall
Fully automated Artix Linux installer for my testing setup

# Basic Usage
1. Boot the artix installer with language en_US, timezone Europe/Berlin and keymap de.
2. Log in as root (password artix).
3. Now run the script: `curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/artixinstall | sh`

# FDE (Full Disk Encryption) Usage
1. Boot the artix installer with language en_US, timezone Europe/Berlin and keymap de.
2. Log in as root (password artix).
3. Now run the script: `curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/cryptinstall | sh`

# Automated install
This method works for all installation methods mentioned above.

1. Boot the artix installer with language en_US, timezone Europe/Berlin and keymap de.
2. Log in as root (password artix).
3. Run the script with parameters: `curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/<artix | crypt>install | sh -s -- <drive>`
