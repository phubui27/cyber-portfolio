# Chapter 11 – Linux Filesystem & File Management

## 1. Core Concept
Linux follows the principle **“Everything is a file”**.
- Files, directories, devices, kernel information, and processes are all accessed via the filesystem.
- The filesystem is organized as a **single hierarchical tree**, starting at `/` (root).

---

## 2. Filesystem Hierarchy (FHS – Must Know)

| Directory | Purpose |
| :--- | :--- |
| `/` | Root of the filesystem |
| `/home` | Home directories for normal users |
| `/root` | Home directory of the root user |
| `/etc` | System-wide configuration files |
| `/var` | Variable data (logs, spool, cache) |
| `/bin` | Essential user commands |
| `/sbin` | Essential system administration commands |
| `/usr/bin` | Main executable programs |
| `/usr/sbin` | Non-essential system daemons |
| `/lib`, `/lib64` | Shared libraries and kernel modules |
| `/boot` | Kernel and bootloader (GRUB) files |
| `/dev` | Device nodes |
| `/proc` | Pseudo-filesystem (process & kernel info) |
| `/sys` | Kernel and hardware info |
| `/run`, `/media`, `/mnt` | Mounted removable or temporary filesystems |

---

## 3. Mounting & Partitions

### Mount / Unmount

sudo mount /dev/sda5 /home
sudo umount /home
A filesystem must be mounted to be accessible.

Mounting on a non-empty directory hides existing contents.

Automatic mounts are defined in '/etc/fsta4b'

## 4. Network Filesystem (NFS)

Server Side
Configuration file: /etc/exports

Service management:
sudo systemctl start nfs
sudo systemctl enable nfs

Client Side:
sudo mount server:/projects /mnt/nfs/projects

## 5. File Comparison & Change Management
diff
Compare text files: diff file1 file2

| Common options | Explain |
| :--- | :--- |
|-c | context output |
|-r | recursive |
|-q | quiet (only report differences) |
|-i | ignore case |
|-w | ignore whitespace |

## 6. File Type Identification

file:
file filename
Determines the real file type by examining contents.

Linux does not rely on file extensions.

## 7. Backup & Synchronization
cp
Simple local copy only.
rsync -av --progress sourcedir destdir
rsync --dry-run -av sourcedir destdir
Efficient incremental backup and synchronization.

Supports remote systems.

Warning: Dangerous if misused → always test with --dry-run.

## 8. Compression Utilities

| Tool  | Characteristics |
| :--- | :--- |
| gzip | "Fast, widely used" |
| bzip2 | "Better compression, mostly legacy" |
| xz | "Best compression, slower" |
| zip | Mainly for Windows compatibility |

---

## 9. Archiving with tar

Create archive: tar cf backup.tar mydir

Archive with compression:

tar zcf backup.tar.gz mydir   # gzip

tar jcf backup.tar.bz2 mydir  # bzip2

tar Jcf backup.tar.xz mydir   # xz

Extract: tar xf backup.tar.gz

## 10. Disk-to-Disk Copying (WARNING)

dd: dd if=/dev/sda of=sda.mbr bs=512 count=1

Copies raw disk or partition data.

One incorrect command can destroy data permanently.

Use only when fully understood.

## 11. Key Takeaways
Filesystem knowledge is foundational for Linux-based roles.

Understand structure before memorizing commands.

rsync, tar, diff, and patch are real-world tools.

Pseudo-filesystems (/proc, /sys) expose live system state.

Regular backups are mandatory for system reliability.