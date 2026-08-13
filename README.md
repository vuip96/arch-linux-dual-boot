# Arch Linux Dual Boot with Windows 11

A hands-on Linux system administration project documenting a **manual Arch Linux installation alongside Windows 11** using **UEFI, GRUB, disk partitioning, networking, package management and command-line troubleshooting**.

The goal was to build a working dual-boot environment without removing the existing Windows installation or user data.

![Completed GRUB menu with Arch Linux and Windows Boot Manager](images/grub-valmis.jpg)

---

## Project Overview

I installed Arch Linux manually on the same laptop as an existing Windows 11 installation.

The project involved:

- preserving the existing Windows partitions
- creating a dedicated Linux `ext4` partition
- reusing the existing EFI System Partition
- installing and configuring Arch Linux from the command line
- configuring Wi-Fi and NetworkManager
- installing GRUB as the bootloader
- detecting Windows Boot Manager with `os-prober`
- diagnosing and fixing a boot configuration problem
- verifying that both operating systems booted successfully

The final system presents a GRUB menu at startup, allowing either **Arch Linux** or **Windows Boot Manager** to be selected.

> **Note:** The commands and device names shown in this repository document my own installation. Partition names such as `/dev/nvme0n1p5` are system-specific and should not be copied blindly to another machine.

---

## Result

The completed system achieved the following:

- Arch Linux boots successfully.
- Windows 11 remains fully functional.
- GRUB detects both operating systems.
- Arch Linux uses its own `ext4` partition.
- Both systems use the existing UEFI/EFI boot environment.
- Networking, the user account and package updates were tested successfully.

---

## Technologies and Tools

- **Arch Linux**
- **Windows 11**
- **UEFI / EFI System Partition**
- **GRUB**
- **Rufus**
- **iwctl**
- **NetworkManager**
- **pacman**
- **os-prober**
- **mkinitcpio**
- **Linux command line**
- **ext4**
- **NVMe storage**

---

## Installation Workflow

### 1. Boot Media and UEFI

The Arch Linux installation media was created on a USB drive using Rufus.

Secure Boot was disabled in the BIOS/UEFI settings so that the installation media could boot correctly in UEFI mode.

UEFI mode was verified with:

```bash
cat /sys/firmware/efi/fw_platform_size
```

The output `64` confirmed that the installer had booted in 64-bit UEFI mode.

---

### 2. Network Configuration

Wi-Fi was configured in the Arch installation environment with `iwctl`.

Connectivity was verified with:

```bash
ping -c 3 archlinux.org
```

This confirmed that the installer had working internet access before package installation.

---

### 3. Disk and Partition Management

The existing storage layout was inspected using:

```bash
lsblk -f
```

The Windows partitions were preserved. A separate Linux partition, `/dev/nvme0n1p5`, was created and formatted as `ext4`.

![Disk layout showing Windows partitions and the Arch Linux ext4 partition](images/levyosiot-lsblk.jpg)

For this installation, the Linux root partition and the existing EFI partition were mounted as follows:

```bash
mount /dev/nvme0n1p5 /mnt
mkdir -p /mnt/efi
mount /dev/nvme0n1p1 /mnt/efi
```

---

### 4. Base System Installation

The Arch Linux base system, kernel, firmware, text editor and network management tools were installed using `pacstrap`:

```bash
pacstrap -K /mnt base linux linux-firmware nano networkmanager
```

The filesystem table was then generated and the installed system entered with `arch-chroot`:

```bash
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
```

Inside the installed system I configured:

- timezone
- locale
- keyboard layout
- hostname
- user account
- sudo permissions
- networking

---

### 5. GRUB and Windows Dual Boot

GRUB, EFI tools, `os-prober`, sudo and NetworkManager were installed with:

```bash
pacman -S grub efibootmgr os-prober sudo networkmanager
```

GRUB was installed to the EFI environment:

```bash
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=Arch
```

Windows detection was enabled:

```bash
echo GRUB_DISABLE_OS_PROBER=false >> /etc/default/grub
```

The final GRUB configuration was generated with:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

---

## Troubleshooting

The most useful part of this project from a system-administration perspective was troubleshooting the first boot.

### Problem

After the initial installation, GRUB detected **Windows Boot Manager**, but **Arch Linux itself was missing from the boot menu**.

![Initial GRUB menu where Arch Linux was missing](images/grub-arch-puuttuu.jpg)

### Diagnosis

The problem was traced to missing Linux kernel and initramfs files under `/boot`.

This meant GRUB had no valid Arch Linux boot entry to generate even though the bootloader itself was installed.

### Fix

The kernel and firmware packages were reinstalled:

```bash
pacman -S linux linux-firmware
```

The initramfs images were regenerated:

```bash
mkinitcpio -P
```

The GRUB configuration was then rebuilt:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

After the fix, GRUB detected the Linux kernel, initramfs and Windows Boot Manager correctly.

![GRUB configuration successfully detecting Arch Linux and Windows](images/grub-konfiguraatio-valmis.jpg)

This troubleshooting step was an important part of the project because it required identifying the difference between a successfully installed bootloader and a bootloader with a valid Linux boot entry.

---

## Final System Verification

After the GRUB issue was resolved:

- Arch Linux booted successfully.
- Login with the normal user account worked.
- Windows 11 still booted through GRUB.
- Network connectivity worked.
- The Arch installation could be updated normally.

![Successful login to the installed Arch Linux system](images/arch-kirjautuminen.jpg)

The installed packages were updated with:

```bash
sudo pacman -Syu
```

---

## What This Project Demonstrates

This project demonstrates practical experience with:

- Linux installation and administration
- command-line system configuration
- disk partitioning and filesystems
- mounting filesystems
- UEFI and EFI boot architecture
- GRUB installation and configuration
- Windows/Linux dual-boot environments
- Linux networking
- package management with `pacman`
- boot troubleshooting
- kernel and initramfs concepts
- preserving an existing operating system during installation
- documenting a technical workflow from start to finish

The most important learning outcome was understanding how the different parts of the Linux boot process connect: **UEFI → EFI System Partition → GRUB → kernel → initramfs → operating system**.

---

## Documentation

A more detailed Finnish-language PDF documents the full installation process, commands, explanations and screenshots.

📄 **[Open the full Arch Linux installation documentation (Finnish)](docs/Arch-Linux-asennus.pdf)**

---

## Repository Structure

```text
arch-linux-dual-boot/
├── docs/
│   └── Arch-Linux-asennus.pdf     # Full Finnish documentation
├── images/
│   ├── arch-kirjautuminen.jpg
│   ├── grub-arch-puuttuu.jpg
│   ├── grub-konfiguraatio-valmis.jpg
│   ├── grub-valmis.jpg
│   └── levyosiot-lsblk.jpg
└── README.md
```

---

## Author

**Pete Vuorela**  
ICT Engineering  
Oulu University of Applied Sciences
