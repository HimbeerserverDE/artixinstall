# artixinstall

Fully automated Artix Linux installer. Only supports en_US language
but any timezone and keymap (derived from selection in the installer menu).

# Usage

1. Boot the Artix Installer.
2. Log in as `root`. The password is `artix`.
3. Use one of the methods listed below.
4. Once you get a green success message, reboot.

## Basic Usage (BIOS / MBR)

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/artixinstall | sh
```

## FDE (Full Disk Encryption) Usage (BIOS / MBR)

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/cryptinstall | sh
```

## Basic Usage (UEFI / GPT)

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/uefiinstall | sh
```

## FDE (Full Disk Encryption) Usage (UEFI / GPT)

**WARNING: The EFI partition cannot be encrypted.**

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/cryptuefiinstall | sh
```

## Automated Install

This method works for all installation methods mentioned above.

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/<artix | uefi | crypt | cryptuefi>install | sh -s -- [drive [grubtarget]]
```

# Partition Layout

## BIOS

BIOS installations follow this disk layout:

* /boot: ext4, 256 MiB
* /: btrfs, 100% - 256 MiB, compress=zstd, subvol=/root

If FDE is used both partitions are LUKS2 containers. The boot partition uses
PBKDF2 as its key derivation function.

## UEFI

UEFI installations follow this disk layout:

* /boot/efi: fat32, 256 MiB
* /boot: ext4, 256 MiB
* /: btrfs, 100% - 512 MiB, compress=zstd, subvol=/root
