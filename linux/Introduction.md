# Linux Filesystem Hierarchy (FHS)

The Linux File System Hierarchy Standard (FHS) defines a standard directory structure used by Linux distributions. Every directory has a specific purpose.

---

## `/` - Root Directory
The top-level directory in Linux. Every file and directory starts from `/`.

**Purpose:**
- Root of the entire filesystem.
- All other directories are located under it.
- Required to boot the operating system before other filesystems are mounted.

---

## `/bin` - Essential User Commands

Contains essential executable commands used by all users.

**Examples:**
- `ls`
- `cp`
- `mv`
- `cat`
- `pwd`
- `bash`

---

## `/boot` - Boot Files

Contains files required to boot Linux.

**Includes:**
- Linux Kernel
- GRUB Bootloader
- Initial RAM Disk (initramfs)

Without this directory, the operating system cannot boot.

---

## `/dev` - Device Files

Contains device files that represent hardware connected to the system.

**Examples:**
- `/dev/sda` → First hard disk
- `/dev/sda1` → First partition
- `/dev/null` → Discards any data written to it
- `/dev/tty` → Terminal device

---

## `/etc` - Configuration Files

Stores system-wide configuration files.

Common files:

- `/etc/passwd` → User account information
- `/etc/shadow` → Encrypted passwords
- `/etc/hosts` → Local hostname resolution
- `/etc/ssh/` → SSH configuration

---

## `/home` - User Home Directories

Each regular user has a personal directory here.

Examples:

```text
/home/alice
/home/bob
```

Used to store:
- Documents
- Downloads
- Desktop files
- Personal configurations

---

## `/lib` - Shared Libraries

Contains shared libraries required by programs and essential system binaries.

Similar to **DLL files** in Windows.

---

## `/media` - Removable Media

Mount point for removable storage devices.

Examples:
- USB drives
- CDs/DVDs
- External hard drives

---

## `/mnt` - Temporary Mount Point

Used to temporarily mount filesystems manually.

Example:

```bash
mount /dev/sdb1 /mnt
```

---

## `/opt` - Optional Software

Stores optional or third-party applications.

Examples:
- Google Chrome
- Burp Suite
- Custom applications

---

## `/root` - Root User Home

Home directory of the **root** (administrator) user.

Example:

```text
/root
```

Do not confuse it with:

```text
/
```

`/` = Root filesystem

`/root` = Root user's home directory

---

## `/sbin` - System Binaries

Contains executables mainly used for system administration.

Examples:
- `shutdown`
- `reboot`
- `fdisk`
- `iptables`

Most commands require root privileges.

---

## `/tmp` - Temporary Files

Stores temporary files created by the operating system and applications.

Characteristics:
- Temporary storage
- May be deleted automatically
- Usually cleared after reboot

---

## `/usr` - User Programs and Resources

Contains user applications, libraries, documentation, and manuals.

Common directories:

- `/usr/bin`
- `/usr/lib`
- `/usr/share`

Most installed software resides here.

---

## `/var` - Variable Data

Stores files whose contents change frequently.

Common directories:

- `/var/log` → Log files
- `/var/www/html` → Web server files
- `/var/mail` → User mailboxes
- `/var/spool` → Queued tasks

Frequently used by system administrators and security professionals for troubleshooting and log analysis.

---

# Summary Table

| Directory | Purpose |
|-----------|---------|
| `/` | Root of the entire filesystem |
| `/bin` | Essential user commands |
| `/boot` | Bootloader and kernel files |
| `/dev` | Device files |
| `/etc` | System configuration files |
| `/home` | Home directories for users |
| `/lib` | Shared libraries |
| `/media` | Removable media mount point |
| `/mnt` | Temporary mount point |
| `/opt` | Optional third-party software |
| `/root` | Home directory of the root user |
| `/sbin` | System administration commands |
| `/tmp` | Temporary files |
| `/usr` | User applications and libraries |
| `/var` | Variable data (logs, mail, web files, etc.) |

