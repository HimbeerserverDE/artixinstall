# artixinstall

Fully automated Artix Linux installer. Only supports en_US language
but any timezone and keymap (derived from selection in the installer menu).
Capable of encrypting installations and using the linux-hardened kernel.

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

**WARNING: The EFI partition cannot be encrypted. This probably doesn't matter
as long as nobody has physical access to the machine, but make sure
not to store any information in /boot/efi by accident.**

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/cryptuefiinstall | sh
```

## Automated Install

This method works for all installation methods mentioned above.

```
curl -fsSL https://raw.githubusercontent.com/HimbeerserverDE/artixinstall/main/<artix | uefi | crypt | cryptuefi>install | sh -s -- [drive [grubtarget]]
```

The UEFI scripts will ignore the GRUB target as they skip it completely.

# Quirks

## No UEFI boot entries on Dell Latitude E5270

For some unknown reason this laptop refuses to list or boot any entries
created by `efibootmgr`. This most likely can't be fixed in this script.
A workaround is to add the entries from the UEFI setup menu
(select the EFI partition, it should be the first partition on the OS drive):

### Traditional Install

* Artix Linux: `\EFI\artix\artix-linux.efi`
* Artix Linux (fallback initramfs): `\EFI\artix\artix-linux-fallback.efi`

### Encrypted Install

* Artix Linux: `\EFI\artix\artix-linux-hardened.efi`
* Artix Linux (fallback initramfs): `\EFI\artix\artix-linux-hardened-fallback.efi`

# Partition Layout

## BIOS

BIOS installations follow this disk layout:

* /boot: ext4, 1 GiB
* /: btrfs, 100% - 1 GiB, compress=zstd, subvol=/root

If FDE is used both partitions are LUKS2 containers. The boot partition uses
PBKDF2 as its key derivation function.

## UEFI

UEFI installations follow this disk layout:

* /boot/efi: fat32, 1 GiB
* /: btrfs, 100% - 1 GiB, compress=zstd, subvol=/root
