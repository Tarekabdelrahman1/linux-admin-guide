# Linux Administration Guide and Troubleshooting Manual

## Table of Contents

- [Chapter 1: Introduction and Conventions](#chapter-1-introduction-and-conventions)
  - [Scope](#scope)
  - [Prerequisites](#prerequisites)
  - [Command and Placeholder Conventions](#command-and-placeholder-conventions)
- [Chapter 2: Core Linux Administration](#chapter-2-core-linux-administration)
  - [Processes, File Descriptors, and Sockets](#processes-file-descriptors-and-sockets)
  - [Inodes, Hard Links, and Directories](#inodes-hard-links-and-directories)
  - [Log Rotation with logrotate](#log-rotation-with-logrotate)
  - [Installing and Updating Software Packages](#installing-and-updating-software-packages)
  - [Service and SSH Checks Used with Port Examples](#service-and-ssh-checks-used-with-port-examples)
- [Chapter 3: Practical Troubleshooting Method](#chapter-3-practical-troubleshooting-method)
  - [The Core Workflow](#the-core-workflow)
  - [Start with These Commands](#start-with-these-commands)
  - [Capture a Baseline](#capture-a-baseline)
- [Chapter 4: Troubleshooting Command Reference](#chapter-4-troubleshooting-command-reference)
  - [System Identity, Uptime, and Recent Changes](#system-identity-uptime-and-recent-changes)
  - [systemd Service Troubleshooting](#systemd-service-troubleshooting)
  - [Journal and Log Analysis](#journal-and-log-analysis)
  - [CPU, Load Average, and Process Analysis](#cpu-load-average-and-process-analysis)
  - [Memory and Swap Troubleshooting](#memory-and-swap-troubleshooting)
  - [Disk Space, Inodes, Filesystems, and I/O](#disk-space-inodes-filesystems-and-i-o)
  - [Network Interface, Routing, and Port Troubleshooting](#network-interface-routing-and-port-troubleshooting)
  - [DNS Troubleshooting](#dns-troubleshooting)
  - [Firewall and Packet Filtering](#firewall-and-packet-filtering)
  - [Permissions, ACLs, Ownership, and SELinux](#permissions-acls-ownership-and-selinux)
  - [Boot, Kernel, and Emergency-Mode Troubleshooting](#boot-kernel-and-emergency-mode-troubleshooting)
  - [LVM Troubleshooting](#lvm-troubleshooting)
  - [Package and Repository Troubleshooting](#package-and-repository-troubleshooting)
  - [Time Synchronization Troubleshooting](#time-synchronization-troubleshooting)
  - [SELinux and Linux Security Deep Dive](#selinux-and-linux-security-deep-dive)
  - [Linux Storage Deep Dive](#linux-storage-deep-dive)
- [Chapter 5: Realistic Troubleshooting Scenarios](#chapter-5-realistic-troubleshooting-scenarios)
  - [Scenario 1: A systemd Service Will Not Start](#scenario-1-a-systemd-service-will-not-start)
  - [Scenario 2: The Service Is Running but the Port Is Unreachable](#scenario-2-the-service-is-running-but-the-port-is-unreachable)
  - [Scenario 3: High Load Average but CPU Is Not Busy](#scenario-3-high-load-average-but-cpu-is-not-busy)
  - [Scenario 4: One Process Uses 100% CPU](#scenario-4-one-process-uses-100-cpu)
  - [Scenario 5: The Server Is Running Out of Memory](#scenario-5-the-server-is-running-out-of-memory)
  - [Scenario 6: df Says the Filesystem Is Full but du Does Not](#scenario-6-df-says-the-filesystem-is-full-but-du-does-not)
  - [Scenario 7: “No Space Left on Device” but Disk Space Is Available](#scenario-7-no-space-left-on-device-but-disk-space-is-available)
  - [Scenario 8: Disk I/O Is Slow](#scenario-8-disk-i-o-is-slow)
  - [Scenario 9: A Filesystem Became Read-Only](#scenario-9-a-filesystem-became-read-only)
  - [Scenario 10: DNS Resolution Fails](#scenario-10-dns-resolution-fails)
  - [Scenario 11: SSH Troubleshooting by Failure Type](#scenario-11-ssh-troubleshooting-by-failure-type)
  - [Scenario 12: SELinux Blocks an Application](#scenario-12-selinux-blocks-an-application)
  - [Scenario 13: DNF Cannot Reach a Repository](#scenario-13-dnf-cannot-reach-a-repository)
  - [Scenario 14: The Host Boots into Emergency Mode](#scenario-14-the-host-boots-into-emergency-mode)
  - [Scenario 15: An LVM Filesystem Is Full](#scenario-15-an-lvm-filesystem-is-full)
  - [Scenario 16: The Server Has an IP Address but Cannot Reach the Network](#scenario-16-the-server-has-an-ip-address-but-cannot-reach-the-network)
  - [Scenario 17: A Process Is a Zombie](#scenario-17-a-process-is-a-zombie)
  - [Scenario 18: A Process Cannot Open a File](#scenario-18-a-process-cannot-open-a-file)
  - [Scenario 19: Log Rotation Runs but Disk Space Does Not Drop](#scenario-19-log-rotation-runs-but-disk-space-does-not-drop)
  - [Scenario 20: An Application Is Slow but Not Obviously Broken](#scenario-20-an-application-is-slow-but-not-obviously-broken)
  - [Scenario 21: A Named ACL User Still Gets Permission denied](#scenario-21-a-named-acl-user-still-gets-permission-denied)
  - [Scenario 22: A File Works Before mv but Fails in Its New SELinux Location](#scenario-22-a-file-works-before-mv-but-fails-in-its-new-selinux-location)
  - [Scenario 23: A Web Service Cannot Read Content Under /srv](#scenario-23-a-web-service-cannot-read-content-under-srv)
  - [Scenario 24: A Service Cannot Bind to a Custom Port](#scenario-24-a-service-cannot-bind-to-a-custom-port)
  - [Scenario 25: A User Is in wheel but sudo Fails](#scenario-25-a-user-is-in-wheel-but-sudo-fails)
  - [Scenario 26: Repeated SSH Authentication Failures](#scenario-26-repeated-ssh-authentication-failures)
  - [Scenario 27: Determine Who Changed a Security File](#scenario-27-determine-who-changed-a-security-file)
  - [Scenario 28: systemd Hardening Breaks a Service](#scenario-28-systemd-hardening-breaks-a-service)
  - [Scenario 29: An Unexpected Setuid or Capability Binary Appears](#scenario-29-an-unexpected-setuid-or-capability-binary-appears)
  - [Scenario 30: Return SELinux from Permissive to Enforcing](#scenario-30-return-selinux-from-permissive-to-enforcing)
  - [Scenario 31: A Newly Attached Disk Does Not Appear](#scenario-31-a-newly-attached-disk-does-not-appear)
  - [Scenario 32: A New Partition Exists in fdisk but Not in /dev](#scenario-32-a-new-partition-exists-in-fdisk-but-not-in-dev)
  - [Scenario 33: A Server Enters Emergency Mode Because of /etc/fstab](#scenario-33-a-server-enters-emergency-mode-because-of-etc-fstab)
  - [Scenario 34: df Is Full but du Shows Much Less Data](#scenario-34-df-is-full-but-du-shows-much-less-data)
  - [Scenario 35: “No Space Left on Device” with Free Blocks](#scenario-35-no-space-left-on-device-with-free-blocks)
  - [Scenario 36: Extend an XFS LVM Filesystem Without Downtime](#scenario-36-extend-an-xfs-lvm-filesystem-without-downtime)
  - [Scenario 37: The Virtual Disk Grew but the Filesystem Did Not](#scenario-37-the-virtual-disk-grew-but-the-filesystem-did-not)
  - [Scenario 38: The Filesystem Suddenly Became Read-Only](#scenario-38-the-filesystem-suddenly-became-read-only)
  - [Scenario 39: An LVM Logical Volume Is Missing After Reboot](#scenario-39-an-lvm-logical-volume-is-missing-after-reboot)
  - [Scenario 40: A Thin Pool Is Almost Full](#scenario-40-a-thin-pool-is-almost-full)
  - [Scenario 41: RAID1 Is Degraded](#scenario-41-raid1-is-degraded)
  - [Scenario 42: umount Reports “Target Is Busy”](#scenario-42-umount-reports-target-is-busy)
  - [Scenario 43: Disk I/O Latency Causes High Load Average](#scenario-43-disk-i-o-latency-causes-high-load-average)
  - [Scenario 44: A Hung NFS Mount Freezes Commands](#scenario-44-a-hung-nfs-mount-freezes-commands)
  - [Scenario 45: An LV Was Extended but df Did Not Change](#scenario-45-an-lv-was-extended-but-df-did-not-change)
  - [Scenario 46: A Snapshot Became Invalid](#scenario-46-a-snapshot-became-invalid)
  - [Scenario 47: The Wrong Disk Was Almost Selected for Formatting](#scenario-47-the-wrong-disk-was-almost-selected-for-formatting)
- [Chapter 6: Quick Reference](#chapter-6-quick-reference)
  - [Compact Troubleshooting Workflows](#compact-troubleshooting-workflows)
  - [Command Index](#command-index)
  - [Important Files Index](#important-files-index)
  - [Useful One-Liners for Fast Triage](#useful-one-liners-for-fast-triage)
- [Chapter 7: Troubleshooting Safety Rules](#chapter-7-troubleshooting-safety-rules)
  - [Signal escalation for a process](#signal-escalation-for-a-process)
- [Chapter 8: Document Maintenance and Change Log](#chapter-8-document-maintenance-and-change-log)
  - [Maintenance Process](#maintenance-process)
  - [Future Update Log](#future-update-log)
  - [Troubleshooting Update Log](#troubleshooting-update-log)

> **Document status:** Living technical reference
> **Checkpoint date:** 2026-07-27
> **Last updated:** 2026-07-28
> **Audience:** RHCSA review through RHCE and advanced Linux administration
> **Primary platform:** RHEL-family systems, with commands applicable to many modern Linux distributions

---

<a id="chapter-1-introduction-and-conventions"></a>
# Chapter 1: Introduction and Conventions

This guide is a practical reference for Linux administration, incident triage, and root-cause analysis. It combines command explanations, operational examples, safety guidance, and realistic troubleshooting scenarios.

<a id="scope"></a>
## Scope

The manual covers process inspection, file descriptors, sockets, filesystems, storage, package management, `systemd`, logging, networking, SELinux, security hardening, and production troubleshooting.

<a id="prerequisites"></a>
## Prerequisites

- Working knowledge of the Linux shell and basic filesystem navigation.
- A user account with `sudo` access for administrative commands.
- A non-production lab or recovery plan for storage, security, and service-management exercises.
- Distribution-specific utilities installed as required, such as `lsof`, `sysstat`, `bind-utils`, `tcpdump`, and SELinux administration tools.

> **Warning:** Several commands in this guide can stop services, alter security policy, modify storage, or destroy data when used with the wrong target. Verify hostnames, paths, devices, and service impact before making changes.

<a id="command-and-placeholder-conventions"></a>
## Command and Placeholder Conventions

| Convention | Meaning |
|---|---|
| `PID`, `PORT`, `DEVICE`, `INTERFACE` | Replace with a real process ID, port, block device, or network interface. |
| `service_name` | Replace with the actual `systemd` unit name. |
| **`/path/to/file`** | Replace with the real file or directory path. |
| `command_name`, `package_name` | Replace with the command or package being investigated. |

> **Tip:** Begin with read-only inspection commands. Capture evidence before changing configuration, restarting services, or rebooting the host.

<a id="chapter-2-core-linux-administration"></a>
# Chapter 2: Core Linux Administration

This chapter explains the core objects and tools used throughout the troubleshooting sections.

<a id="processes-file-descriptors-and-sockets"></a>
## Processes, File Descriptors, and Sockets

### Process Inspection

#### List all running processes

```bash
ps aux
```

Alternative full-format view:

```bash
ps -ef
```

#### Find a process by name

```bash
pgrep sshd
```

Show the PID and command name:

```bash
pgrep -a sshd
```

Another option:

```bash
pidof sshd
```

#### Inspect a specific process

```bash
ps -fp PID
```

Example:

```bash
ps -fp 1058
```

---

### File Descriptors

A **file descriptor**, or **FD**, is a small integer used by a process to refer to an open kernel object.

The object behind an FD may be:

- A regular file
- A directory
- A socket
- A pipe
- A terminal
- A device
- An anonymous kernel object

The application generally works with the FD number. The kernel maintains the information about the real object behind it.

Standard file descriptors:

| FD | Standard name | Default purpose |
|---:|---|---|
| `0` | `stdin` | Input |
| `1` | `stdout` | Normal output |
| `2` | `stderr` | Error output |

#### View the open FDs of a process

```bash
ls -l /proc/PID/fd/
```

Example:

```bash
ls -l /proc/1058/fd/
```

#### Resolve the object behind one FD

```bash
readlink /proc/PID/fd/FD
```

Example:

```bash
readlink /proc/1058/fd/3
```

#### Inspect FD information maintained by the kernel

```bash
cat /proc/PID/fdinfo/FD
```

Example:

```bash
cat /proc/1058/fdinfo/3
```

#### List everything opened by a process

```bash
lsof -p PID
```

Example:

```bash
lsof -p 1058
```

#### Show processes using a particular file

```bash
lsof /path/to/file
```

Example:

```bash
lsof /var/log/messages
```

#### Show deleted files that are still open

```bash
lsof +L1
```

This is useful when disk space is not released because a process still holds an FD to a deleted file.

---

### Sockets

A **socket** is a kernel communication endpoint.

Sockets can be used for:

- Network communication
- Communication between local processes
- TCP
- UDP
- Unix domain sockets

A network socket is still accessed by a process through a file descriptor.

#### Show the process using TCP or UDP port 22

```bash
lsof -i :22
```

Example output discussed:

```text
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    1058 root    3u  IPv4  ...
```

Meaning:

- `sshd`: Process name
- `1058`: PID
- `root`: Process owner
- `3u`: FD number `3`, open for reading and writing
- `IPv4`: IPv4 socket
- Port `22`: SSH service port

#### Show listening TCP sockets

```bash
ss -lnt
```

Include owning processes:

```bash
ss -lntp
```

#### Show all TCP connections

```bash
ss -antp
```

#### Show listening UDP sockets

```bash
ss -lnup
```

#### Filter for port 22

```bash
ss -lntp 'sport = :22'
```

A simpler text filter:

```bash
ss -lntp | grep ':22'
```

#### Identify a process using a TCP port

```bash
fuser -v 22/tcp
```

#### Inspect Unix domain sockets

```bash
ss -lx
```

Include process information:

```bash
ss -lxnp
```

---

### Useful **`/proc`** Process Paths

| Path | Purpose |
|---|---|
| **`/proc/PID/fd/`** | Symbolic links for the process's open FDs |
| **`/proc/PID/fdinfo/`** | Detailed FD information |
| **`/proc/PID/status`** | Human-readable process status |
| **`/proc/PID/cmdline`** | Process command line |
| **`/proc/PID/environ`** | Process environment variables |
| **`/proc/PID/maps`** | Process memory mappings |
| **`/proc/PID/net/`** | Process network namespace information |

Useful commands:

```bash
cat /proc/PID/status
```

```bash
tr '\0' ' ' < /proc/PID/cmdline
```

```bash
tr '\0' '\n' < /proc/PID/environ
```

---

<a id="inodes-hard-links-and-directories"></a>
## Inodes, Hard Links, and Directories

### View Inode Numbers

```bash
ls -li
```

For a specific file:

```bash
ls -li filename
```

Using `stat`:

```bash
stat filename
```

Important `stat` fields include:

- Inode number
- Link count
- Ownership
- Permissions
- Size
- Timestamps

---

### Create a Hard Link

```bash
ln source_file hardlink_name
```

Example:

```bash
ln report.txt report-hardlink.txt
```

Both names point to the same inode.

Confirm:

```bash
ls -li report.txt report-hardlink.txt
```

#### Remove one hard-link name

```bash
rm hardlink_name
```

The data remains available while at least one hard link exists or a process still has the inode open.

#### Find files by inode number

```bash
find /path -inum INODE_NUMBER
```

Example:

```bash
find / -xdev -inum 123456 2>/dev/null
```

#### Find regular files with more than one hard link

```bash
find /path -xdev -type f -links +1
```

---

### Why a New Directory Has Link Count 2

Create a directory:

```bash
mkdir testdir
```

Inspect its link count:

```bash
ls -ld testdir
```

A new directory normally begins with link count `2` because:

1. Its name in the parent directory points to the directory inode.
2. Its internal `.` entry points to the same directory inode.

The internal `..` entry points to the parent directory, not to the new directory itself.

#### Demonstration

```bash
mkdir parent
```

```bash
stat parent
```

Then create a child:

```bash
mkdir parent/child
```

Check again:

```bash
stat parent
```

The parent directory's link count normally increases by one because the child's `..` entry points back to the parent.

#### Show directory entries, including `.` and `..`

```bash
ls -la directory_name
```

---

### Symbolic Links Compared with Hard Links

#### Create a symbolic link

```bash
ln -s target link_name
```

Example:

```bash
ln -s /var/log/messages messages-link
```

#### Inspect the symbolic link

```bash
ls -l messages-link
```

Resolve its target:

```bash
readlink messages-link
```

Resolve the complete canonical path:

```bash
readlink -f messages-link
```

#### Key Differences

| Hard link | Symbolic link |
|---|---|
| Another name for the same inode | A separate file containing a path |
| Usually cannot cross filesystems | Can cross filesystems |
| Normally cannot link directories | Can point to directories |
| Remains valid if another filename is removed | Can become broken if target disappears |

### `cp` Compared with `mv`

Both commands can make a pathname appear in a new location, but they do very different work at the filesystem level.

### Basic Commands

Copy one file:

```bash
cp source_file destination_file
```

Move or rename one file:

```bash
mv source_file destination_file
```

Copy a directory recursively:

```bash
cp -r source_directory destination_directory
```

A safer metadata-preserving directory copy:

```bash
cp -a source_directory destination_directory
```

Move a directory:

```bash
mv source_directory destination_directory
```

---

### Behavioral Differences

#### `cp`

`cp` creates another filesystem object at the destination and copies data into it.

Normally:

- The source remains in place.
- The destination receives a different inode.
- The destination is an independent file.
- Changing the destination does not change the source.
- Copying a large file requires reading and writing its data.
- Metadata preservation depends on the options used.

Verify the inode difference:

```bash
cp original.txt copied.txt
ls -li original.txt copied.txt
```

The inode numbers should normally be different.

#### `mv` on the same filesystem

When source and destination are on the same filesystem, `mv` normally performs a rename operation.

Normally:

- File data is not copied.
- The inode remains the same.
- The operation is usually very fast, even for a large file.
- The old pathname disappears.
- The new pathname points to the same inode.
- Open file descriptors continue to refer to that inode.

Verify:

```bash
ls -li largefile
mv largefile /same/filesystem/newname
ls -li /same/filesystem/newname
```

The inode should remain the same.

#### `mv` across different filesystems

A single rename cannot cross filesystem boundaries.

When the destination is on another filesystem, `mv` effectively has to:

1. Copy the source to the destination filesystem.
2. Preserve supported metadata.
3. Remove the original after the copy succeeds.

Consequences:

- The destination receives a new inode.
- The operation takes time proportional to the data size.
- It needs enough free space on the destination.
- A failure can leave the original in place and may leave partial destination work, depending on the failure point and implementation.
- Open file descriptors still refer to the old source inode until it is finally removed and all references are closed.

Check whether two paths are on the same filesystem:

```bash
df -T /source/path /destination/path
```

A more precise mount check:

```bash
findmnt -T /source/path
findmnt -T /destination/path
```

Compare device IDs:

```bash
stat -c '%d %n' /source/path /destination/path
```

Different device IDs mean the paths are on different mounted filesystems.

---

### Practical comparison

| Behavior | `cp` | `mv` on same filesystem | `mv` across filesystems |
|---|---|---|---|
| Source remains | Yes | No | No after successful copy |
| Data copied | Yes | Normally no | Yes |
| Inode preserved | No | Yes | No |
| Fast for a huge file | Depends on size | Usually yes | Depends on size |
| Needs destination free space | Yes | Usually only directory metadata | Yes |
| Open FDs keep using original inode | Source remains independently | Yes, through renamed inode | Yes, through old inode until closed |
| Directory option needed | `-r` or `-a` | No special recursive option | No special recursive option |
| Metadata preservation | Depends on options | Mostly preserved because it is the same inode | `mv` attempts to preserve supported metadata |

---

### Metadata behavior

A plain copy:

```bash
cp source destination
```

copies file contents but does not necessarily preserve every piece of metadata exactly.

The new destination is normally owned by the user performing the copy. Timestamps and extended metadata may differ.

Preserve mode, ownership, and timestamps where permitted:

```bash
cp -p source destination
```

Archive mode:

```bash
cp -a source destination
```

`cp -a` is commonly used for administrative copies because it recursively attempts to preserve:

- Permissions
- Ownership
- Timestamps
- Symbolic links
- Extended attributes
- ACLs
- SELinux labels, when supported
- Hard-link relationships among source files copied together

Always verify critical metadata after a migration:

```bash
stat source destination
getfacl source destination
ls -lZ source destination
```

---

### Hard-link behavior

Suppose two names point to the same inode:

```bash
ln file1 file2
ls -li file1 file2
```

Copy only one of them:

```bash
cp file1 file3
```

`file3` normally gets a new inode and is no longer part of the original hard-link set.

```bash
ls -li file1 file2 file3
```

A same-filesystem `mv` only renames one directory entry, so it preserves the inode and the hard-link relationship.

When copying a directory tree containing multiple hard links, use archive mode if preserving those relationships matters:

```bash
cp -a source_tree/ destination_tree/
```

Then verify:

```bash
find destination_tree -xdev -type f -links +1 -ls
```

---

### Symbolic-link behavior

Inspect a symbolic link:

```bash
ls -l link_name
readlink link_name
```

Move it:

```bash
mv link_name new_link_name
```

`mv` moves the symbolic link itself, not the target.

For copying, behavior depends on options and whether recursion is involved. To preserve symbolic links as symbolic links during an administrative tree copy, use:

```bash
cp -a source_tree/ destination_tree/
```

or explicitly:

```bash
cp -P source_link destination_link
```

Verify afterward:

```bash
ls -l destination_link
readlink destination_link
```

---

### Existing destination files

Ask before overwrite:

```bash
cp -i source destination
mv -i source destination
```

Never overwrite an existing destination:

```bash
cp -n source destination
mv -n source destination
```

Show each operation:

```bash
cp -v source destination
mv -v source destination
```

For important data, do not rely on shell aliases to provide `-i`. Write the option explicitly.

Check aliases:

```bash
type cp
type mv
```

---

### Copying directory contents correctly

This:

```bash
cp -a source_directory destination_directory
```

can create `destination_directory/source_directory`, depending on whether the destination already exists.

To copy the contents of a directory, including hidden entries:

```bash
cp -a source_directory/. destination_directory/
```

Using `source_directory/*` is incomplete because the shell glob normally excludes hidden names such as `.config`.

Preview paths first:

```bash
printf '%s\n' source_directory/.*
```

Be careful because shell patterns involving `.*` can be error-prone. `source_directory/.` with `cp -a` is the safer common pattern for copying all contents.

---

### SELinux difference between copying and moving

This difference is important on SELinux systems.

#### Copying

A newly created destination file can receive a context based on the destination directory's labeling rules.

Check:

```bash
cp /tmp/index.html /var/www/html/
ls -lZ /var/www/html/index.html
```

#### Moving on the same filesystem

A same-filesystem move preserves the existing inode, so it also preserves the inode's current SELinux label.

A file moved from **`/tmp`** into a web directory may therefore keep an inappropriate label:

```bash
mv /tmp/index.html /var/www/html/
ls -lZ /var/www/html/index.html
```

Restore the expected destination context:

```bash
restorecon -v /var/www/html/index.html
```

For a whole tree:

```bash
restorecon -Rv /var/www/html/
```

Therefore, when content is moved between security-sensitive directory trees, always verify its SELinux context.

---

### Open file descriptors and renamed files

A process does not access an already-open file by repeatedly looking up its pathname. It uses its file descriptor.

Example workflow:

```bash
lsof /path/to/application.log
mv /path/to/application.log /path/to/application.log.old
```

A process that already had the file open can continue writing to the same inode through its FD even though the pathname changed.

Check:

```bash
lsof -p PID
ls -li /path/to/application.log.old
```

This behavior is one reason log rotation must signal a service to close and reopen its log file.

Copying the file does not redirect the process's existing FD to the copy.

---

### Safer administrative examples

Create a backup while preserving metadata:

```bash
cp -a /etc/service.conf /etc/service.conf.$(date +%F-%H%M%S).bak
```

Rename a configuration file on the same filesystem:

```bash
mv /etc/service.conf /etc/service.conf.disabled
```

Copy a directory tree and verify before deleting the source:

```bash
cp -a /source/tree/. /destination/tree/
diff -qr /source/tree /destination/tree
```

For large or resumable transfers, `rsync` may be more suitable:

```bash
rsync -aHAX --info=progress2 /source/tree/ /destination/tree/
```

Important `rsync` options:

| Option | Meaning |
|---|---|
| `-a` | Archive behavior |
| `-H` | Preserve hard links |
| `-A` | Preserve ACLs |
| `-X` | Preserve extended attributes |

Verify the destination before removing the original.

---

### Determine Whether `mv` Renamed or Copied a File

Compare filesystem device IDs:

```bash
stat -c 'device=%d inode=%i path=%n' /source/path
stat -c 'device=%d inode=%i path=%n' /destination/path
```

Before moving, save the source inode:

```bash
stat -c '%d:%i' source_file
```

After a same-filesystem move:

```bash
stat -c '%d:%i' destination_file
```

The device and inode pair should match.

Across filesystems, the pair changes because a new inode is created.
---

<a id="log-rotation-with-logrotate"></a>
## Log Rotation with `logrotate`

### What `logrotate` Does

`logrotate` manages text log files by:

- Renaming or rotating old logs
- Keeping a configured number of historical copies
- Compressing old logs
- Creating a new log file
- Running scripts before or after rotation
- Rotating based on time or file size

It does **not** automatically rotate every log file on the system.

It rotates logs defined in:

1. The main configuration file.
2. Files included by the main configuration, normally under **`/etc/logrotate.d/`**.

---

### Important Files and Directories

| Path | Purpose |
|---|---|
| **`/etc/logrotate.conf`** | Main configuration |
| **`/etc/logrotate.d/`** | Package- and service-specific configurations |
| **`/var/lib/logrotate/logrotate.status`** | Rotation state file on many systems |
| **`/var/lib/logrotate/status`** | Alternative state-file path on some systems |
| **`/usr/sbin/logrotate`** | Main executable |
| **`/usr/lib/systemd/system/logrotate.service`** | Systemd service unit on many distributions |
| **`/usr/lib/systemd/system/logrotate.timer`** | Systemd timer unit on many distributions |

Inspect the main configuration:

```bash
cat /etc/logrotate.conf
```

List included configurations:

```bash
ls -l /etc/logrotate.d/
```

Search for include directives:

```bash
grep -nE '^[[:space:]]*include' /etc/logrotate.conf
```

Search all configured log paths:

```bash
grep -R --line-number --include='*' '^/' /etc/logrotate.conf /etc/logrotate.d/
```

---

### Check How `logrotate` Is Triggered

On systemd-based systems:

```bash
systemctl status logrotate.timer
```

List timer details:

```bash
systemctl list-timers logrotate.timer
```

Inspect the service:

```bash
systemctl status logrotate.service
```

View its logs:

```bash
journalctl -u logrotate.service
```

Show recent timer activity:

```bash
journalctl -u logrotate.timer
```

Some older systems may run it from cron:

```bash
ls -l /etc/cron.daily/logrotate
```

---

### Test a Configuration Safely

Debug mode:

```bash
logrotate -d /etc/logrotate.conf
```

`-d` shows what would happen without performing the rotations.

Verbose mode:

```bash
logrotate -v /etc/logrotate.conf
```

Force rotation:

```bash
logrotate -f /etc/logrotate.conf
```

Force and display details:

```bash
logrotate -vf /etc/logrotate.conf
```

Test one service configuration:

```bash
logrotate -d /etc/logrotate.d/sshd
```

Use force carefully in production because it performs rotation even if normal conditions are not met.

---

### Common Directives

```conf
daily
weekly
monthly
yearly
```

Rotate based on age:

```conf
daily
```

Rotate based on size:

```conf
size 100M
```

Keep a number of old copies:

```conf
rotate 7
```

Compress old files:

```conf
compress
```

Delay compression until the following rotation:

```conf
delaycompress
```

Ignore a missing log:

```conf
missingok
```

Do not rotate empty logs:

```conf
notifempty
```

Create a replacement file:

```conf
create 0640 root root
```

Run a script after rotation:

```conf
postrotate
    systemctl reload service-name
endscript
```

Run one shared script for a group of logs:

```conf
sharedscripts
```

Copy then truncate the active file:

```conf
copytruncate
```

`copytruncate` can be useful when an application cannot reopen its log, but it has a small race window where log lines may be lost.

---

### Example Configuration

```conf
/var/log/myapp/*.log {
    daily
    rotate 7
    compress
    delaycompress
    missingok
    notifempty
    create 0640 myapp myapp
    sharedscripts
    postrotate
        systemctl reload myapp.service >/dev/null 2>&1 || true
    endscript
}
```

Debug the configuration:

```bash
logrotate -d /etc/logrotate.d/myapp
```

Force a test rotation:

```bash
logrotate -vf /etc/logrotate.d/myapp
```

---

### Troubleshooting `logrotate`

#### Validate syntax

```bash
logrotate -d /etc/logrotate.conf
```

#### Check the last rotation state

```bash
cat /var/lib/logrotate/logrotate.status
```

Alternative:

```bash
cat /var/lib/logrotate/status
```

#### Check ownership and permissions

```bash
ls -l /var/log/application.log
```

```bash
namei -l /var/log/application.log
```

#### Check whether a service reopened its log

```bash
lsof /var/log/application.log
```

#### Find processes holding deleted logs

```bash
lsof +L1
```

#### Check SELinux context

```bash
ls -Z /var/log/application.log
```

#### Restore the default context if needed

```bash
restorecon -v /var/log/application.log
```

---

<a id="installing-and-updating-software-packages"></a>
## Installing and Updating Software Packages

The primary package stack on modern RHEL-family systems is:

- `dnf`: High-level package manager
- `rpm`: Low-level RPM package database and package tool
- Repositories: Sources from which packages and metadata are obtained

`yum` is commonly available as a compatibility command and may point to DNF.

---

### Repository Inspection

#### List enabled repositories

```bash
dnf repolist
```

List all repositories:

```bash
dnf repolist all
```

Show detailed repository information:

```bash
dnf repoinfo
```

#### List repository configuration files

```bash
ls -l /etc/yum.repos.d/
```

Display a repository file:

```bash
cat /etc/yum.repos.d/example.repo
```

#### Show the repositories used for a package

```bash
dnf info package_name
```

Detailed package/repository query:

```bash
dnf repoquery --info package_name
```

---

### Search for Packages

```bash
dnf search keyword
```

Example:

```bash
dnf search nginx
```

Search package names and summaries:

```bash
dnf search all keyword
```

Show package information:

```bash
dnf info package_name
```

List all matching packages:

```bash
dnf list package_name
```

List installed packages:

```bash
dnf list installed
```

List available packages:

```bash
dnf list available
```

---

### Install Packages

```bash
dnf install package_name
```

Example:

```bash
dnf install httpd
```

Install multiple packages:

```bash
dnf install package1 package2 package3
```

Automatically answer yes:

```bash
dnf -y install package_name
```

Install a local RPM while resolving dependencies:

```bash
dnf install ./package-file.rpm
```

Install from an absolute path:

```bash
dnf install /path/to/package-file.rpm
```

---

### Remove Packages

```bash
dnf remove package_name
```

Equivalent command:

```bash
dnf erase package_name
```

Preview dependencies that are no longer needed:

```bash
dnf autoremove --assumeno
```

Remove unused dependencies:

```bash
dnf autoremove
```

---

### Check for Updates

```bash
dnf check-update
```

A return code of `100` normally means updates are available; this is not necessarily an error.

List upgrades:

```bash
dnf list updates
```

Show advisories:

```bash
dnf updateinfo
```

List security advisories:

```bash
dnf updateinfo list security
```

Show advisory details:

```bash
dnf updateinfo info
```

---

### Update Packages

Update all packages:

```bash
dnf upgrade
```

Common equivalent:

```bash
dnf update
```

Update one package:

```bash
dnf upgrade package_name
```

Apply security-related updates:

```bash
dnf upgrade --security
```

Refresh metadata first:

```bash
dnf upgrade --refresh
```

---

### Reinstall, Downgrade, and Version Selection

Reinstall:

```bash
dnf reinstall package_name
```

Downgrade to an older available version:

```bash
dnf downgrade package_name
```

Show all available versions:

```bash
dnf --showduplicates list package_name
```

Install a specific version:

```bash
dnf install package_name-version
```

Example format:

```bash
dnf install nginx-1.24.0
```

Exact package naming depends on the repository and architecture.

---

### Find Which Package Provides a File or Command

Find the package providing an existing file:

```bash
rpm -qf /path/to/file
```

Example:

```bash
rpm -qf /usr/bin/ls
```

Search repositories for a path or command:

```bash
dnf provides '/usr/bin/command'
```

Example:

```bash
dnf provides '/usr/bin/semanage'
```

Wildcard search:

```bash
dnf provides '*/semanage'
```

---

### RPM Queries

Check whether a package is installed:

```bash
rpm -q package_name
```

List all installed packages:

```bash
rpm -qa
```

Search installed packages:

```bash
rpm -qa | grep -i keyword
```

Show package information:

```bash
rpm -qi package_name
```

List files installed by a package:

```bash
rpm -ql package_name
```

List package configuration files:

```bash
rpm -qc package_name
```

List package documentation files:

```bash
rpm -qd package_name
```

Show package scripts:

```bash
rpm -q --scripts package_name
```

Show package dependencies:

```bash
rpm -qR package_name
```

Determine the owner of a file:

```bash
rpm -qf /path/to/file
```

---

### Inspect an RPM File Before Installing It

Package information:

```bash
rpm -qpi package-file.rpm
```

List included files:

```bash
rpm -qpl package-file.rpm
```

List scripts:

```bash
rpm -qp --scripts package-file.rpm
```

List requirements:

```bash
rpm -qpR package-file.rpm
```

Verify the signature:

```bash
rpm -K package-file.rpm
```

---

### Direct RPM Installation

Install:

```bash
rpm -ivh package-file.rpm
```

Upgrade or install:

```bash
rpm -Uvh package-file.rpm
```

Freshen only if already installed:

```bash
rpm -Fvh package-file.rpm
```

Remove:

```bash
rpm -e package_name
```

Prefer `dnf install ./package-file.rpm` for normal administration because DNF resolves dependencies.

Avoid forcing installations unless performing controlled recovery:

```bash
rpm --nodeps
```

```bash
rpm --force
```

These options can leave the package database or system dependencies in an inconsistent state.

---

### Verify Installed Package Files

Verify all files from a package:

```bash
rpm -V package_name
```

Verify all installed packages:

```bash
rpm -Va
```

Common verification markers may indicate changes to:

- Size
- Mode
- Checksum
- Device numbers
- Symbolic-link target
- Owner
- Group
- Modification time
- Capabilities

Inspect configuration files from a package:

```bash
rpm -V package_name | grep ' c '
```

---

### DNF Transaction History

List transaction history:

```bash
dnf history
```

Show one transaction:

```bash
dnf history info TRANSACTION_ID
```

Undo a transaction:

```bash
dnf history undo TRANSACTION_ID
```

Redo a transaction:

```bash
dnf history redo TRANSACTION_ID
```

Rollback to an earlier transaction state:

```bash
dnf history rollback TRANSACTION_ID
```

History operations must be reviewed carefully because repositories may no longer contain the exact older package versions.

---

### Cache and Metadata

Show cache directories:

```bash
ls -l /var/cache/dnf/
```

Clean cached metadata and packages:

```bash
dnf clean all
```

Rebuild cache:

```bash
dnf makecache
```

Force metadata refresh during a command:

```bash
dnf --refresh repolist
```

---

### Package Groups and Modules

List package groups:

```bash
dnf group list
```

Show group information:

```bash
dnf group info "Group Name"
```

Install a group:

```bash
dnf group install "Group Name"
```

List module streams where supported:

```bash
dnf module list
```

Show a module:

```bash
dnf module info module_name
```

Enable a stream:

```bash
dnf module enable module_name:stream
```

Install a module stream:

```bash
dnf module install module_name:stream
```

Module behavior varies by RHEL-family release.

---

### Important Package-Management Files

| Path | Purpose |
|---|---|
| **`/etc/dnf/dnf.conf`** | Main DNF configuration |
| **`/etc/yum.conf`** | YUM configuration or compatibility configuration |
| **`/etc/yum.repos.d/*.repo`** | Repository definitions |
| **`/var/cache/dnf/`** | DNF metadata and package cache |
| **`/var/lib/rpm/`** | RPM database |
| **`/etc/pki/rpm-gpg/`** | Common location for repository GPG keys |
| **`/var/log/dnf.log`** | DNF log |
| **`/var/log/dnf.rpm.log`** | RPM operations performed through DNF |
| **`/var/log/yum.log`** | Package log on older systems |
| **`/usr/bin/dnf`** | DNF command |
| **`/usr/bin/rpm`** | RPM command |

Inspect DNF configuration:

```bash
cat /etc/dnf/dnf.conf
```

Inspect repository definitions:

```bash
grep -R --line-number -E '^\[|^name=|^baseurl=|^mirrorlist=|^metalink=|^enabled=|^gpgcheck=' /etc/yum.repos.d/
```

Inspect package logs:

```bash
less /var/log/dnf.log
```

```bash
less /var/log/dnf.rpm.log
```

---

### Repository and GPG Troubleshooting

#### Confirm system time

Incorrect time can cause TLS and repository metadata failures.

```bash
timedatectl
```

#### Test DNS resolution

```bash
getent hosts repository.example.com
```

#### Test HTTPS connectivity

```bash
curl -I https://repository.example.com/
```

#### Clean and recreate metadata

```bash
dnf clean all
```

```bash
dnf makecache
```

#### Show detailed DNF output

```bash
dnf -v repolist
```

More debugging:

```bash
dnf -d 10 repolist
```

#### Import an RPM GPG key

```bash
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-name
```

List imported public keys:

```bash
rpm -qa 'gpg-pubkey*'
```

Show key information:

```bash
rpm -qi gpg-pubkey-PACKAGE_ID
```

Do not disable GPG checking as a normal fix. First validate the repository, key, package source, and system time.

---

<a id="service-and-ssh-checks-used-with-port-examples"></a>
## Service and SSH Checks Used with Port Examples

Because port `22` and `sshd` were used in the FD/socket example, these checks are useful.

### Check SSH service status

```bash
systemctl status sshd
```

### Show recent SSH service logs

```bash
journalctl -u sshd
```

Follow logs live:

```bash
journalctl -fu sshd
```

### Confirm the listening socket

```bash
ss -lntp | grep ':22'
```

### Confirm the process and its FDs

```bash
pgrep -a sshd
```

```bash
lsof -i :22
```

```bash
ls -l /proc/PID/fd/
```

---

<a id="chapter-3-practical-troubleshooting-method"></a>
# Chapter 3: Practical Troubleshooting Method

Effective troubleshooting is evidence-driven. Use a repeatable workflow, make the smallest safe change, and verify the original user-visible symptom after remediation.

> **Note:** A reboot may hide evidence without correcting the root cause. Collect logs, process state, resource data, and recent-change information first.

Good troubleshooting is not random command execution. Use a repeatable process.

<a id="the-core-workflow"></a>
## The Core Workflow

1. **Define the symptom precisely**
   - What is failing?
   - What exact error appears?
   - Who is affected?
   - When did it begin?
   - Is the failure permanent or intermittent?

2. **Determine the scope**
   - One user or every user?
   - One service or the whole host?
   - One network path or every destination?
   - One filesystem or all storage?

3. **Collect evidence before changing anything**
   - Service state
   - Logs
   - Resource usage
   - Network state
   - Recent package or configuration changes

4. **Build a hypothesis**
   - Configuration problem
   - Dependency problem
   - Resource exhaustion
   - Permission or SELinux denial
   - Network or DNS failure
   - Storage or filesystem problem

5. **Test the smallest safe hypothesis**
   - Use read-only commands first.
   - Change one variable at a time.
   - Avoid rebooting before evidence is collected.

6. **Apply the least disruptive fix**
   - Reload before restart when supported.
   - Restart one service before rebooting the host.
   - Restore the intended configuration instead of applying broad workarounds.

7. **Verify the result**
   - Check the service locally.
   - Check it remotely.
   - Recheck logs.
   - Confirm that the original user-visible symptom is gone.

8. **Document the root cause and prevention**
   - What failed?
   - Why did it fail?
   - What fixed it?
   - What monitoring or configuration change prevents recurrence?

---

<a id="start-with-these-commands"></a>
## Start with These Commands

```bash
date
hostnamectl
uptime
who
w
last -x | head -20
systemctl --failed
journalctl -p warning..alert -b
df -hT
df -i
free -h
ip -br address
ip route
ss -lntup
```

What they reveal:

| Command | Main question answered |
|---|---|
| `date` | Is system time reasonable? |
| `hostnamectl` | Which host and operating system am I on? |
| `uptime` | How long has the system been running and what is its load? |
| `who`, `w` | Who is logged in and what are they doing? |
| `last -x` | Were there recent reboots, shutdowns, or run-level changes? |
| `systemctl --failed` | Which systemd units are currently failed? |
| `journalctl -p warning..alert -b` | What important warnings occurred during this boot? |
| `df -hT` | Are filesystems full and what types are they? |
| `df -i` | Are inodes exhausted? |
| `free -h` | Is memory pressure obvious? |
| `ip -br address` | Are interfaces up and addressed? |
| `ip route` | Is there a usable route and default gateway? |
| `ss -lntup` | Which TCP and UDP sockets are listening? |

---

<a id="capture-a-baseline"></a>
## Capture a Baseline

Before making changes, save useful state:

```bash
mkdir -p /root/troubleshooting
```

```bash
date > /root/troubleshooting/baseline.txt
hostnamectl >> /root/troubleshooting/baseline.txt
uptime >> /root/troubleshooting/baseline.txt
systemctl --failed >> /root/troubleshooting/baseline.txt
df -hT >> /root/troubleshooting/baseline.txt
df -i >> /root/troubleshooting/baseline.txt
free -h >> /root/troubleshooting/baseline.txt
ip -br address >> /root/troubleshooting/baseline.txt
ip route >> /root/troubleshooting/baseline.txt
ss -lntup >> /root/troubleshooting/baseline.txt
```

Capture the journal for the current boot:

```bash
journalctl -b > /root/troubleshooting/journal-current-boot.txt
```

Capture one service:

```bash
systemctl status service_name --no-pager -l \
  > /root/troubleshooting/service-status.txt
```

```bash
journalctl -u service_name -b --no-pager \
  > /root/troubleshooting/service-journal.txt
```

This allows comparison after a change and prevents useful evidence from being lost.

---

<a id="chapter-4-troubleshooting-command-reference"></a>
# Chapter 4: Troubleshooting Command Reference

Use this reference to select commands by subsystem. Each section starts with low-risk inspection and progresses toward deeper diagnostics or corrective actions.

<a id="system-identity-uptime-and-recent-changes"></a>
## System Identity, Uptime, and Recent Changes

### Show host identity and OS information

```bash
hostnamectl
```

Useful for confirming:

- Correct server
- Hostname
- Operating system
- Kernel
- Architecture
- Virtualization type

### Show the running kernel

```bash
uname -r
```

Full information:

```bash
uname -a
```

### Show operating-system release information

```bash
cat /etc/os-release
```

### Show uptime and load averages

```bash
uptime
```

The three load numbers represent approximately:

- Last 1 minute
- Last 5 minutes
- Last 15 minutes

Load average includes tasks using CPU and tasks stuck in uninterruptible sleep, commonly waiting for I/O.

### Show recent boots and shutdowns

```bash
last -x | head -30
```

Show recorded boots:

```bash
journalctl --list-boots
```

Inspect the previous boot:

```bash
journalctl -b -1
```

### Show recent package transactions

```bash
dnf history
```

Show details:

```bash
dnf history info TRANSACTION_ID
```

### Find recently modified configuration files

Example for **`/etc`**:

```bash
find /etc -xdev -type f -mtime -2 -printf '%TY-%Tm-%Td %TH:%TM %p\n' \
  2>/dev/null | sort
```

Files modified in the last 60 minutes:

```bash
find /etc -xdev -type f -mmin -60 -ls 2>/dev/null
```

Use timestamps as clues, but do not assume every recent change caused the failure.

---

<a id="systemd-service-troubleshooting"></a>
## `systemd` Service Troubleshooting

### Show failed units

```bash
systemctl --failed
```

### Show detailed status

```bash
systemctl status service_name
```

Do not rely only on the final line. Read:

- `Loaded`
- `Active`
- Main PID
- Exit status
- Recent log lines
- Unit-file path

Display full lines without truncation:

```bash
systemctl status service_name --no-pager -l
```

### Determine whether the unit is enabled

```bash
systemctl is-enabled service_name
```

### Determine whether it is active

```bash
systemctl is-active service_name
```

### Display the complete unit definition

```bash
systemctl cat service_name
```

This includes:

- Vendor unit
- Drop-in overrides
- Local modifications

### Show important runtime properties

```bash
systemctl show service_name \
  -p ActiveState \
  -p SubState \
  -p Result \
  -p MainPID \
  -p ExecMainCode \
  -p ExecMainStatus \
  -p FragmentPath
```

### Show dependencies

```bash
systemctl list-dependencies service_name
```

Reverse dependencies:

```bash
systemctl list-dependencies --reverse service_name
```

### Verify unit-file syntax

```bash
systemd-analyze verify /etc/systemd/system/service_name.service
```

### Reload unit files after editing them

```bash
systemctl daemon-reload
```

This makes systemd reread unit files. It does not restart the service.

### Reload a service configuration

```bash
systemctl reload service_name
```

Use when the service supports reload.

### Restart a service

```bash
systemctl restart service_name
```

### Clear a recorded failed state

```bash
systemctl reset-failed service_name
```

This does not fix the root cause. It only clears the failed marker.

### View service logs

```bash
journalctl -u service_name
```

Current boot only:

```bash
journalctl -u service_name -b
```

Follow live:

```bash
journalctl -fu service_name
```

Last 100 lines:

```bash
journalctl -u service_name -n 100 --no-pager
```

Since a specific time:

```bash
journalctl -u service_name --since "30 minutes ago"
```

---

<a id="journal-and-log-analysis"></a>
## Journal and Log Analysis

### Show the current boot

```bash
journalctl -b
```

### Show the previous boot

```bash
journalctl -b -1
```

### Show kernel messages

```bash
journalctl -k
```

Current boot kernel messages:

```bash
journalctl -k -b
```

### Filter by severity

Emergency through error:

```bash
journalctl -p emerg..err -b
```

Warnings and more severe:

```bash
journalctl -p warning..alert -b
```

### Filter by executable

```bash
journalctl /usr/sbin/sshd
```

### Filter by PID

```bash
journalctl _PID=PID
```

### Filter by UID

```bash
journalctl _UID=1000
```

### Show precise timestamps

```bash
journalctl -o short-precise
```

### Show verbose metadata

```bash
journalctl -o verbose -n 1
```

### Show disk usage of the journal

```bash
journalctl --disk-usage
```

### Verify journal integrity

```bash
journalctl --verify
```

### Common text-log commands

Follow a file:

```bash
tail -f /var/log/file.log
```

Show the last 100 lines:

```bash
tail -n 100 /var/log/file.log
```

Search case-insensitively:

```bash
grep -i 'error' /var/log/file.log
```

Search recursively with line numbers:

```bash
grep -RniE 'error|fail|denied|timeout' /var/log/application/
```

Show context around matches:

```bash
grep -n -B 3 -A 5 'error' /var/log/file.log
```

Follow only matching lines:

```bash
tail -F /var/log/file.log | grep --line-buffered -iE 'error|fail'
```

---

<a id="cpu-load-average-and-process-analysis"></a>
## CPU, Load Average, and Process Analysis

### Show interactive process activity

```bash
top
```

Useful keys inside `top`:

- `P`: Sort by CPU
- `M`: Sort by memory
- `1`: Show individual CPUs
- `H`: Show threads
- `c`: Show full command lines
- `k`: Send a signal
- `q`: Quit

### Alternative interface if installed

```bash
htop
```

### Show processes sorted by CPU

```bash
ps -eo pid,ppid,user,stat,ni,pri,psr,%cpu,%mem,etime,comm,args \
  --sort=-%cpu | head -30
```

Field meanings:

| Field | Meaning |
|---|---|
| `PID` | Process ID |
| `PPID` | Parent process ID |
| `STAT` | Process state |
| `NI` | Nice value |
| `PRI` | Scheduler priority |
| `PSR` | CPU currently or recently used |
| `%CPU` | CPU utilization |
| `%MEM` | Percentage of physical memory |
| `ETIME` | Elapsed runtime |
| `ARGS` | Full command line |

### Show process hierarchy

```bash
pstree -ap
```

For one process:

```bash
pstree -ap PID
```

### Monitor one process repeatedly

```bash
watch -n 1 'ps -p PID -o pid,ppid,stat,%cpu,%mem,etime,wchan:32,cmd'
```

### Show per-process CPU statistics

If `sysstat` is installed:

```bash
pidstat 1
```

One process:

```bash
pidstat -p PID 1
```

Threads of one process:

```bash
pidstat -t -p PID 1
```

### Show per-CPU utilization

```bash
mpstat -P ALL 1
```

Important fields:

- `%usr`: User-space CPU
- `%sys`: Kernel CPU
- `%iowait`: CPU idle while waiting for I/O
- `%steal`: Time taken by the hypervisor from a virtual CPU
- `%idle`: Idle time

### Show broad system activity every second

```bash
vmstat 1
```

Important columns:

| Column | Meaning |
|---|---|
| `r` | Runnable tasks waiting for CPU |
| `b` | Tasks blocked in uninterruptible sleep |
| `si` | Swap-in rate |
| `so` | Swap-out rate |
| `bi` | Blocks read from storage |
| `bo` | Blocks written to storage |
| `us` | User CPU |
| `sy` | System CPU |
| `wa` | I/O wait |
| `st` | Virtualization steal time |

Ignore the first line when evaluating current rates because it often represents averages since boot.

### Show historical CPU activity

```bash
sar -u 1 5
```

Per-CPU:

```bash
sar -P ALL 1 5
```

Run queue and load:

```bash
sar -q 1 5
```

### Show process state

```bash
ps -o pid,ppid,stat,wchan:32,cmd -p PID
```

Common process states:

| State | Meaning |
|---|---|
| `R` | Running or runnable |
| `S` | Interruptible sleep |
| `D` | Uninterruptible sleep, often I/O |
| `T` | Stopped or traced |
| `Z` | Zombie |
| `I` | Idle kernel thread |

### Trace system calls

Attach to a process:

```bash
strace -f -tt -T -p PID
```

Meanings:

- `-f`: Follow child processes
- `-tt`: Precise timestamps
- `-T`: Time spent in each system call
- `-p`: Attach to PID

Trace a new command:

```bash
strace -f -o /tmp/command.strace command arguments
```

Trace only file-related calls:

```bash
strace -f -e trace=file -p PID
```

Trace network calls:

```bash
strace -f -e trace=network -p PID
```

Count system calls:

```bash
strace -c -p PID
```

Attaching can affect performance. Use carefully on sensitive production processes.

### Profile CPU hot spots

If `perf` is installed and permitted:

```bash
perf top
```

Profile one process for 30 seconds:

```bash
perf record -F 99 -p PID -g -- sleep 30
```

Review:

```bash
perf report
```

---

<a id="memory-and-swap-troubleshooting"></a>
## Memory and Swap Troubleshooting

### Show memory summary

```bash
free -h
```

Focus on `available`, not only `free`.

Linux intentionally uses unused memory for cache. Low `free` memory alone is not proof of a problem.

### Show detailed memory counters

```bash
cat /proc/meminfo
```

Useful fields:

- `MemAvailable`
- `Cached`
- `Buffers`
- `SwapTotal`
- `SwapFree`
- `Dirty`
- `Writeback`
- `Slab`
- `SReclaimable`
- `PageTables`
- `HugePages_Total`

### Show processes sorted by resident memory

```bash
ps -eo pid,ppid,user,%mem,rss,vsz,etime,comm,args \
  --sort=-rss | head -30
```

- `RSS`: Physical memory currently resident
- `VSZ`: Virtual address-space size

### Show memory map of one process

```bash
pmap -x PID
```

Summary:

```bash
pmap -x PID | tail -1
```

### Show process status memory fields

```bash
grep -E 'VmPeak|VmSize|VmRSS|VmData|VmSwap|Threads' /proc/PID/status
```

### Monitor one process's memory repeatedly

For a specific PID:

```bash
watch -n 2 "grep -E 'VmRSS|VmSize|VmData|VmSwap' /proc/35942/status"
```

Replace `35942` with the real PID.

Highlight fields that change between refreshes:

```bash
watch -d -n 2 "grep -E 'VmRSS|VmSize|VmData|VmSwap' /proc/PID/status"
```

`watch -n 2` reruns the command every two seconds. This is useful when investigating a suspected memory leak or checking whether a process's memory stabilizes after startup.

The values in **`/proc/PID/status`** are normally shown in KiB.

| Field | Practical meaning |
|---|---|
| `VmSize` | Total virtual address space mapped by the process. It includes code, libraries, heap, stacks, memory-mapped files, reserved mappings, and other virtual regions. It does not mean all of this memory is currently stored in RAM. |
| `VmRSS` | Resident Set Size: the process's pages currently resident in physical RAM. It may include private and shared resident pages. |
| `VmData` | Size of the process's writable private data mappings, commonly including the heap and data segments. It is virtual allocation; some pages may be resident, swapped, or not physically allocated yet. |
| `VmSwap` | Anonymous private memory belonging to the process that is currently stored in swap. |

Important relationship:

- `VmSize` is the broad virtual-memory total.
- `VmRSS` measures what is currently resident in RAM.
- `VmData` describes virtual writable data and heap mappings; it is **not** guaranteed to be fully resident and should not be treated as a direct subset of the current `VmRSS` value.
- Shared pages can make process-level memory totals misleading when values from many processes are simply added together.

For a more detailed mapping breakdown:

```bash
pmap -x PID
```

For proportional memory accounting when supported:

```bash
cat /proc/PID/smaps_rollup
```

Useful fields in `smaps_rollup` include:

- `Rss`
- `Pss`
- `Private_Clean`
- `Private_Dirty`
- `Shared_Clean`
- `Shared_Dirty`
- `Swap`

`Pss`, or Proportional Set Size, divides shared memory proportionally between the processes using it and is often better than RSS when estimating one process's real share of memory.

### Limit virtual memory with `ulimit -v`

```bash
ulimit -v MAX_KIB
```

Example: set a soft virtual-memory limit of 1 GiB for the current shell and programs started from it:

```bash
ulimit -v 1048576
```

Show the current limit:

```bash
ulimit -v
```

Remove the soft limit when the hard limit permits it:

```bash
ulimit -v unlimited
```

`ulimit -v` controls the maximum virtual address space, represented by the `RLIMIT_AS` resource limit.

Practical behavior:

- The limit applies to the current shell.
- Child processes started by that shell normally inherit it.
- It does not apply retroactively to unrelated processes that are already running.
- It limits virtual address space, not only physical RAM or RSS.
- When the process reaches the limit, operations such as `malloc()`, `brk()`, or `mmap()` may fail with an out-of-memory error.
- A program may fail before its RSS reaches the configured value because libraries, stacks, mapped files, and reserved address ranges are also counted in virtual memory.
- Shell startup files should not receive an aggressive global limit without testing, because many unrelated commands may inherit it.

Show both soft and hard limits:

```bash
ulimit -Sv
ulimit -Hv
```

Inspect the current shell's kernel resource limits:

```bash
grep -i 'Max address space' /proc/$$/limits
```

Inspect another process:

```bash
grep -i 'Max address space' /proc/PID/limits
```

Where available, inspect or modify a running process with `prlimit`:

```bash
prlimit --pid PID --as
```

Example limit of 1 GiB:

```bash
prlimit --pid PID --as=1073741824
```

Unlike `ulimit -v`, `prlimit --as` normally uses bytes. Changing a running production process's limit can cause allocation failures, so test and apply it carefully.

For a systemd-managed service, a cgroup memory limit is often clearer when the goal is to control actual memory consumption:

```bash
systemctl show service_name -p MemoryCurrent -p MemoryMax
```

A persistent `MemoryMax=` setting belongs in a reviewed systemd unit override rather than being applied blindly during an incident.

### Show swap devices

```bash
swapon --show
```

### Show swap and paging activity

```bash
vmstat 1
```

Sustained nonzero `si` and `so` can indicate active swapping.

### Show per-process page faults and memory

```bash
pidstat -r 1
```

### Inspect kernel slab memory

```bash
slabtop
```

### Search for Out-Of-Memory events

```bash
journalctl -k -g 'oom|Out of memory|Killed process'
```

Alternative:

```bash
dmesg -T | grep -iE 'oom|out of memory|killed process'
```

### Show cgroup memory constraints for a service

```bash
systemctl show service_name \
  -p MemoryCurrent \
  -p MemoryPeak \
  -p MemoryMax \
  -p MemoryHigh \
  -p OOMPolicy
```

Properties vary by systemd version.

---

<a id="disk-space-inodes-filesystems-and-i-o"></a>
## Disk Space, Inodes, Filesystems, and I/O

### Show filesystem usage and type

```bash
df -hT
```

### Show inode usage

```bash
df -i
```

A filesystem can fail with “No space left on device” even when blocks are available if all inodes are used.

### Show mounted filesystems clearly

```bash
findmnt
```

One path:

```bash
findmnt -T /path
```

### Show block devices and filesystems

```bash
lsblk -o NAME,MAJ:MIN,SIZE,TYPE,FSTYPE,FSVER,LABEL,UUID,MOUNTPOINTS
```

### Show filesystem identifiers

```bash
blkid
```

### Find large top-level directories

```bash
du -xhd1 / | sort -h
```

For **`/var`**:

```bash
du -xhd1 /var | sort -h
```

`-x` stays on one filesystem.

### Find large files

```bash
find /var -xdev -type f -size +500M \
  -printf '%s %p\n' 2>/dev/null | sort -n
```

Human-readable output with GNU tools:

```bash
find /var -xdev -type f -size +500M -print0 2>/dev/null \
  | xargs -0 du -h | sort -h
```

### Find recently growing files

```bash
find /var -xdev -type f -mmin -60 \
  -printf '%TY-%Tm-%Td %TH:%TM %s %p\n' 2>/dev/null \
  | sort -k3,3n
```

### Find deleted files still held open

```bash
lsof +L1
```

Only a specific filesystem:

```bash
lsof +L1 /var
```

### Show disk latency and utilization

If `sysstat` is installed:

```bash
iostat -xz 1
```

Important fields vary by version, but commonly include:

| Field | Meaning |
|---|---|
| `r/s`, `w/s` | Read/write operations per second |
| `rkB/s`, `wkB/s` | Throughput |
| `await` | Average I/O completion latency |
| `aqu-sz` | Average queue depth |
| `%util` | Time the device was busy |

High `%util` alone is not enough to diagnose a problem. Consider latency, queue depth, device type, and workload.

### Show per-process I/O

```bash
pidstat -d 1
```

### Show tasks currently performing I/O

If installed:

```bash
iotop -oPa
```

### Show disk error messages

```bash
journalctl -k -g 'I/O error|Buffer I/O|blk_update_request|reset|timeout'
```

### Inspect mount options

```bash
findmnt -no TARGET,SOURCE,FSTYPE,OPTIONS /mountpoint
```

### Check open files under a mount

```bash
lsof +f -- /mountpoint
```

### Identify processes using a mount

```bash
fuser -vm /mountpoint
```

### XFS information

```bash
xfs_info /mountpoint
```

Check an unmounted XFS filesystem without modifying it:

```bash
xfs_repair -n /dev/DEVICE
```

Actual repair normally requires the filesystem to be unmounted:

```bash
xfs_repair /dev/DEVICE
```

### ext filesystem check

Read-only check where supported:

```bash
e2fsck -n /dev/DEVICE
```

Repair normally requires the filesystem to be unmounted:

```bash
e2fsck -f /dev/DEVICE
```

> **Warning:** Never run filesystem repair blindly on a mounted read-write filesystem.

---

<a id="network-interface-routing-and-port-troubleshooting"></a>
## Network Interface, Routing, and Port Troubleshooting

### Show interfaces briefly

```bash
ip -br address
```

### Show link state and counters

```bash
ip -s link
```

Look for increasing:

- Errors
- Dropped packets
- Overruns
- Carrier errors

### Show one interface

```bash
ip address show dev INTERFACE
```

```bash
ip link show dev INTERFACE
```

### Show routing table

```bash
ip route
```

### Ask the kernel which route it would use

```bash
ip route get DESTINATION_IP
```

Example:

```bash
ip route get 8.8.8.8
```

This reveals:

- Chosen interface
- Source IP
- Gateway
- Route

### Show policy-routing rules

```bash
ip rule
```

Show every routing table:

```bash
ip route show table all
```

### Test local TCP listeners

```bash
ss -lntp
```

### Show established TCP connections

```bash
ss -ntp
```

### Show socket summary

```bash
ss -s
```

### Test IP reachability

```bash
ping -c 4 DESTINATION_IP
```

Do not conclude that a host is down only because ping fails; ICMP may be filtered.

### Trace the route

```bash
tracepath DESTINATION
```

Alternative if installed:

```bash
traceroute DESTINATION
```

### Test a TCP port

With netcat:

```bash
nc -vz HOST PORT
```

Example:

```bash
nc -vz server.example.com 443
```

### Test HTTP or HTTPS

Headers only:

```bash
curl -I https://example.com/
```

Verbose TLS and connection details:

```bash
curl -vk https://example.com/
```

Time individual phases:

```bash
curl -sS -o /dev/null \
  -w 'dns=%{time_namelookup} connect=%{time_connect} tls=%{time_appconnect} first_byte=%{time_starttransfer} total=%{time_total}\n' \
  https://example.com/
```

### Show NetworkManager state

```bash
nmcli general status
```

```bash
nmcli device status
```

Show one connection:

```bash
nmcli connection show CONNECTION_NAME
```

Show active connections:

```bash
nmcli connection show --active
```

### Show interface driver and link information

If `ethtool` is installed:

```bash
ethtool INTERFACE
```

Driver details:

```bash
ethtool -i INTERFACE
```

Counters:

```bash
ethtool -S INTERFACE
```

### Capture packets

Basic capture:

```bash
tcpdump -ni any
```

One host:

```bash
tcpdump -ni any host IP_ADDRESS
```

One TCP port:

```bash
tcpdump -ni any tcp port PORT
```

DNS traffic:

```bash
tcpdump -ni any port 53
```

Save for later analysis:

```bash
tcpdump -ni any -s 0 -w /tmp/capture.pcap
```

Read a saved capture:

```bash
tcpdump -nn -r /tmp/capture.pcap
```

Use `-nn` to avoid hostname and service-name resolution.

---

<a id="dns-troubleshooting"></a>
## DNS Troubleshooting

### Check the configured resolver

```bash
cat /etc/resolv.conf
```

On systems using `systemd-resolved`:

```bash
resolvectl status
```

### Test name resolution through the system libraries

```bash
getent hosts example.com
```

This follows the system's Name Service Switch configuration.

### Inspect Name Service Switch order

```bash
grep '^hosts:' /etc/nsswitch.conf
```

Example:

```text
hosts: files dns myhostname
```

### Query DNS directly

If `dig` is installed:

```bash
dig example.com
```

Use one specific DNS server:

```bash
dig @DNS_SERVER example.com
```

Query an A record:

```bash
dig example.com A
```

Query a reverse record:

```bash
dig -x IP_ADDRESS
```

Trace delegation:

```bash
dig +trace example.com
```

### Compare name and IP tests

```bash
ping -c 2 example.com
```

```bash
ping -c 2 IP_ADDRESS
```

If the IP works but the name fails, focus on DNS or NSS configuration.

### Check DNS timing with curl

```bash
curl -sS -o /dev/null \
  -w 'dns=%{time_namelookup} total=%{time_total}\n' \
  https://example.com/
```

---

<a id="firewall-and-packet-filtering"></a>
## Firewall and Packet Filtering

### `firewalld` Status

```bash
systemctl status firewalld
```

### Show active zones

```bash
firewall-cmd --get-active-zones
```

### Show current zone configuration

```bash
firewall-cmd --list-all
```

Specific zone:

```bash
firewall-cmd --zone=public --list-all
```

### Check whether a service is allowed

```bash
firewall-cmd --query-service=http
```

### Check whether a port is allowed

```bash
firewall-cmd --query-port=8080/tcp
```

### Compare runtime and permanent configuration

Runtime:

```bash
firewall-cmd --list-all
```

Permanent:

```bash
firewall-cmd --permanent --list-all
```

### Show nftables rules

```bash
nft list ruleset
```

### Show legacy iptables rules if used

```bash
iptables -S
```

```bash
iptables -L -n -v
```

Do not flush firewall rules as a first troubleshooting step. Inspect counters and test a narrow rule instead.

---

<a id="permissions-acls-ownership-and-selinux"></a>
## Permissions, ACLs, Ownership, and SELinux

### Inspect every path component

```bash
namei -l /path/to/file
```

This is excellent for finding a parent directory that blocks traversal.

### Show normal permissions

```bash
ls -ld /path /path/to /path/to/file
```

### Show numeric permissions

```bash
stat -c '%A %a %U:%G %n' /path/to/file
```

### Show ACLs

```bash
getfacl /path/to/file
```

Set a test ACL:

```bash
setfacl -m u:username:r /path/to/file
```

Remove one ACL entry:

```bash
setfacl -x u:username /path/to/file
```

### Understanding the ACL mask

An extended POSIX ACL can contain:

- File owner entry: `user::`
- Named user entries: `user:NAME:`
- Owning group entry: `group::`
- Named group entries: `group:NAME:`
- Mask entry: `mask::`
- Other entry: `other::`

Example:

```text
user::rw-
user:alice:rwx
group::r--
group:developers:r-x
mask::r-x
other::---
```

The ACL mask is the maximum effective permission allowed for the **group class**.

It limits:

- The owning group entry
- Every named user entry
- Every named group entry

It does not limit:

- The file owner entry
- The `other::` entry

Therefore, a named user can have requested permissions that are greater than their effective permissions.

Example:

```text
user:alice:rwx                 #effective:r-x
mask::r-x
```

Alice's ACL entry requests `rwx`, but the mask removes effective write access.

Show both requested and effective permissions:

```bash
getfacl /path/to/file
```

When the requested permissions are restricted, `getfacl` displays a comment such as:

```text
user:alice:rwx                 #effective:r-x
```

---

### Why the mask changes when adding users or groups

By default, `setfacl` normally recalculates the mask after ACL entries are modified, unless a mask is explicitly supplied or mask recalculation is disabled.

The recalculated mask is based on the permissions needed by:

- The owning group entry
- Named user entries
- Named group entries

Example:

```bash
setfacl -m u:alice:rwx file
```

The command may expand the mask so Alice's requested permissions can become effective.

Inspect the result:

```bash
getfacl file
```

This behavior is intentional. It prevents a newly added ACL entry from being silently ineffective merely because an older mask was narrower.

---

### Keep a specific mask during one modification

Use `--no-mask`, or its short option `-n`, to prevent automatic mask recalculation:

```bash
setfacl -n -m u:alice:rwx file
```

Equivalent:

```bash
setfacl --no-mask -m u:alice:rwx file
```

The existing mask remains unchanged.

Example:

```bash
setfacl -m m::r-x file
setfacl -n -m u:alice:rwx file
getfacl file
```

Possible result:

```text
user:alice:rwx                 #effective:r-x
mask::r-x
```

Alice requests write access, but the fixed mask blocks it.

This is not an error in `setfacl`; it is the purpose of the mask.

---

### Set the ACL entry and mask explicitly together

A clear method is to specify both in one command:

```bash
setfacl -m u:alice:rwx,m::r-x file
```

For multiple entries:

```bash
setfacl -m u:alice:rwx,u:bob:r--,g:developers:r-x,m::r-x file
```

Then verify:

```bash
getfacl file
```

When the mask entry is explicitly supplied, it defines the intended effective ceiling for the group-class entries in that update.

---

### Recalculate the mask intentionally

Recalculate the mask from the current ACL entries:

```bash
setfacl --mask file
```

Short option:

```bash
setfacl -m m::rwx file
```

These are not exactly the same operation:

- `setfacl --mask file` asks `setfacl` to calculate the mask from the ACL.
- `setfacl -m m::rwx file` explicitly sets the mask to `rwx`.

Use automatic calculation when you want the mask to represent the union required by current group-class entries.

---

### Modify the mask directly

Read and execute only:

```bash
setfacl -m m::r-x file
```

Read and write only:

```bash
setfacl -m m::rw- file
```

Full group-class ceiling:

```bash
setfacl -m m::rwx file
```

No effective permissions for named users and groups:

```bash
setfacl -m m::--- file
```

The ACL entries remain present, but the mask can make them ineffective.

---

### The ACL mask and `chmod`

The traditional group permission bits shown by `ls -l` represent the ACL mask when an extended ACL exists.

Example:

```bash
ls -l file
getfacl file
```

With an extended ACL, this:

```bash
chmod g-w file
```

can change the ACL mask rather than merely changing `group::`.

Always inspect the complete ACL after using `chmod` on a file with extended ACLs:

```bash
getfacl file
```

A `+` after the normal mode indicates additional ACL information:

```text
-rw-r-x---+ 1 root root ...
```

---

### Default ACL masks on directories

A directory can have:

- An access ACL controlling the directory itself
- A default ACL inherited by newly created children

Show both:

```bash
getfacl /shared
```

Create a default ACL:

```bash
setfacl -m d:u:alice:rwx,d:g:developers:r-x,d:m::rwx /shared
```

A complete practical example:

```bash
setfacl -m u:alice:rwx,g:developers:r-x,m::rwx /shared
setfacl -m d:u:alice:rwx,d:g:developers:r-x,d:m::rwx /shared
```

The first command changes access to **`/shared`** itself.

The second command controls ACL entries inherited by new files and directories created inside it.

Inspect default entries only:

```bash
getfacl /shared | sed -n '/^default:/p'
```

---

### Important inheritance detail

Default ACL inheritance does not guarantee that every new regular file becomes executable.

The application passes a creation mode to the kernel. A normal file is often requested as `0666`, while a new directory is often requested as `0777`.

The inherited ACL is adjusted so that permissions not requested by the creating application are not added unexpectedly.

Therefore:

- New directories may inherit execute permission where allowed.
- New regular files usually do not become executable merely because a default ACL contains `x`.

Test:

```bash
touch /shared/newfile
mkdir /shared/newdir
getfacl /shared/newfile
getfacl /shared/newdir
```

---

### Remove ACL entries safely

Remove one named user:

```bash
setfacl -x u:alice file
```

Remove one named group:

```bash
setfacl -x g:developers file
```

Remove all extended access ACL entries:

```bash
setfacl -b file
```

Remove only default ACLs from a directory:

```bash
setfacl -k /shared
```

Back up ACLs before a broad change:

```bash
getfacl -R /shared > /root/shared.acl.backup
```

Restore:

```bash
setfacl --restore=/root/shared.acl.backup
```

---

### ACL mask troubleshooting workflow

#### Symptom

A named user appears to have `rwx` in `getfacl`, but receives `Permission denied`.

#### Inspect the complete path

```bash
namei -l /path/to/file
```

The user needs execute permission on every parent directory.

#### Inspect requested and effective ACL permissions

```bash
getfacl /path/to/file
```

Look for:

```text
#effective:
```

#### Inspect the mask specifically

```bash
getfacl /path/to/file | grep '^mask::'
```

#### Test as the affected user

```bash
sudo -u username test -r /path/to/file && echo readable
sudo -u username test -w /path/to/file && echo writable
sudo -u username test -x /path/to/file && echo executable
```

For a directory:

```bash
sudo -u username ls /path/to/directory
```

#### Decide the intended policy

To allow the permissions, widen the mask:

```bash
setfacl -m m::rwx /path/to/file
```

To retain a restrictive ceiling, keep the mask and reduce the named entry so the ACL is easier to understand:

```bash
setfacl -n -m u:username:r-x /path/to/file
```

#### Recheck SELinux separately

DAC and ACL success do not override SELinux:

```bash
ls -lZ /path/to/file
ausearch -m AVC,USER_AVC -ts recent
```

#### Verify

```bash
getfacl /path/to/file
sudo -u username test -r /path/to/file && echo readable
```

---

### Recommended mask-management rule

Do not try to make the mask permanently unchangeable in every situation.

Instead:

1. Define the intended effective group-class ceiling.
2. Supply the mask explicitly when modifying ACLs.
3. Use `-n` when you deliberately want to preserve the existing mask.
4. Verify `#effective` output after every change.
5. Configure both access and default ACLs for shared directories.
6. Remember that `chmod g...` can alter the mask.

A controlled example:

```bash
setfacl -m u:alice:rwx,g:developers:r-x,m::r-x /shared
setfacl -n -m u:bob:rwx /shared
getfacl /shared
```

Bob's requested `rwx` is retained in the ACL entry, but his effective access is limited by `mask::r-x`.

### Test access as another user

```bash
sudo -u username test -r /path/to/file && echo readable
```

```bash
sudo -u username test -x /path/to/directory && echo traversable
```

### Show SELinux mode

```bash
getenforce
```

Detailed status:

```bash
sestatus
```

### Show SELinux contexts

```bash
ls -lZ /path/to/file
```

Process contexts:

```bash
ps -eZ
```

### Search recent AVC denials

```bash
ausearch -m AVC,USER_AVC -ts recent
```

For one service process name:

```bash
ausearch -m AVC,USER_AVC -ts recent -c process_name
```

### Produce a human-readable SELinux explanation

If `setroubleshoot-server` is installed:

```bash
sealert -a /var/log/audit/audit.log
```

### Show expected file context rules

```bash
semanage fcontext -l | grep '/path'
```

### Restore the expected context

```bash
restorecon -Rv /path
```

### Add a persistent custom mapping

```bash
semanage fcontext -a -t TYPE '/custom/path(/.*)?'
```

Then apply it:

```bash
restorecon -Rv /custom/path
```

Avoid using `chcon` as the permanent fix because relabeling can overwrite it.

### List SELinux booleans

```bash
getsebool -a
```

Search relevant booleans:

```bash
getsebool -a | grep httpd
```

Set a persistent boolean only when its meaning matches the intended policy:

```bash
setsebool -P BOOLEAN_NAME on
```

> **Warning:** Do not disable SELinux as the first troubleshooting step.

---

<a id="boot-kernel-and-emergency-mode-troubleshooting"></a>
## Boot, Kernel, and Emergency-Mode Troubleshooting

### Show failed units

```bash
systemctl --failed
```

### Show current boot errors

```bash
journalctl -b -p err..alert
```

### Show previous boot errors

```bash
journalctl -b -1 -p err..alert
```

### Show kernel messages with readable timestamps

```bash
dmesg -T
```

Search important patterns:

```bash
dmesg -T | grep -iE 'error|fail|panic|oom|I/O|timeout|segfault'
```

### Show boot performance

```bash
systemd-analyze
```

Show slow units:

```bash
systemd-analyze blame
```

Show critical dependency path:

```bash
systemd-analyze critical-chain
```

### Show kernel command line

```bash
cat /proc/cmdline
```

### Show installed kernels

```bash
rpm -q kernel
```

### Show GRUB kernel entries

On RHEL-family systems:

```bash
grubby --info=ALL
```

Show the default kernel:

```bash
grubby --default-kernel
```

### Inspect the initramfs

```bash
lsinitrd
```

Specific image:

```bash
lsinitrd /boot/initramfs-$(uname -r).img
```

### Regenerate the initramfs

```bash
dracut -f
```

Use this only after identifying why regeneration is needed.

### Check **`/etc/fstab`**

```bash
cat /etc/fstab
```

Validate mounts without rebooting:

```bash
mount -av
```

Check systemd-generated mount units:

```bash
systemctl --failed --type=mount
```

### Switch to rescue target

```bash
systemctl isolate rescue.target
```

### Switch to emergency target

```bash
systemctl isolate emergency.target
```

These commands disrupt normal services and should not be used casually on a production host.

---

<a id="lvm-troubleshooting"></a>
## LVM Troubleshooting

### Show physical volumes

```bash
pvs
```

Detailed:

```bash
pvdisplay
```

### Show volume groups

```bash
vgs
```

Detailed:

```bash
vgdisplay
```

### Show logical volumes

```bash
lvs -a -o +devices
```

Detailed:

```bash
lvdisplay
```

### Show free space in volume groups

```bash
vgs -o vg_name,vg_size,vg_free
```

### Show device-mapper tree

```bash
dmsetup ls --tree
```

### Extend a logical volume

Example:

```bash
lvextend -L +10G /dev/VG_NAME/LV_NAME
```

Use all remaining free extents:

```bash
lvextend -l +100%FREE /dev/VG_NAME/LV_NAME
```

### Extend the filesystem with the LV

For supported filesystems:

```bash
lvextend -r -L +10G /dev/VG_NAME/LV_NAME
```

`-r` runs the appropriate filesystem resize helper.

### Grow XFS after extending the LV

```bash
xfs_growfs /mountpoint
```

### Grow ext4 after extending the LV

```bash
resize2fs /dev/VG_NAME/LV_NAME
```

### Scan for LVM objects

```bash
pvscan
vgscan
lvscan
```

### Activate logical volumes

```bash
vgchange -ay
```

### Back up LVM metadata

```bash
vgcfgbackup
```

LVM metadata backups do not back up filesystem data.

---

<a id="package-and-repository-troubleshooting"></a>
## Package and Repository Troubleshooting

### Show enabled repositories

```bash
dnf repolist
```

### Test with fresh metadata

```bash
dnf clean all
dnf makecache
```

### Show verbose repository processing

```bash
dnf -v repolist
```

### Identify which package owns a file

```bash
rpm -qf /path/to/file
```

### Verify an installed package

```bash
rpm -V package_name
```

### Reinstall damaged package content

```bash
dnf reinstall package_name
```

### Show dependency requirements

```bash
rpm -qR package_name
```

### Search for a provider

```bash
dnf provides '*/filename'
```

### Inspect a failed transaction

```bash
dnf history
```

```bash
dnf history info TRANSACTION_ID
```

### Check repository definitions

```bash
grep -RniE '^\[|^name=|^baseurl=|^mirrorlist=|^metalink=|^enabled=|^gpgcheck=' \
  /etc/yum.repos.d/
```

### Verify system time before blaming TLS

```bash
timedatectl
```

### Test DNS and HTTPS to a repository

```bash
getent hosts repository.example.com
```

```bash
curl -Iv https://repository.example.com/
```

---

<a id="time-synchronization-troubleshooting"></a>
## Time Synchronization Troubleshooting

Incorrect time can break:

- TLS certificate validation
- Kerberos
- Distributed databases
- Log correlation
- Scheduled jobs

### Show time state

```bash
timedatectl
```

### Chrony sources

```bash
chronyc sources -v
```

### Chrony tracking

```bash
chronyc tracking
```

### Chrony activity

```bash
chronyc activity
```

### Service status

```bash
systemctl status chronyd
```

### Logs

```bash
journalctl -u chronyd -b
```

<a id="selinux-and-linux-security-deep-dive"></a>
## SELinux and Linux Security Deep Dive

Linux security is layered. A request may be permitted by one control and denied by another.

Common layers:

1. User and group identity
2. Traditional Unix permissions
3. POSIX ACLs
4. Linux capabilities
5. SELinux mandatory access control
6. Firewall and network policy
7. PAM and authentication rules
8. `sudo` authorization
9. systemd sandboxing
10. Application-specific authorization

A secure troubleshooting process checks every relevant layer instead of disabling security controls until the error disappears.

---

### DAC Compared with MAC

Traditional permissions and ACLs are **Discretionary Access Control**, or DAC.

SELinux is **Mandatory Access Control**, or MAC.

An operation can fail under SELinux even when:

- The user is `root`
- The file mode is `777`
- An ACL grants `rwx`
- The service account can access the path using normal permissions

A useful first check:

```bash
namei -l /path/to/file
getfacl /path/to/file
ls -lZ /path/to/file
ausearch -m AVC,USER_AVC -ts recent -i
```

Do not use `chmod 777` as an SELinux fix. It weakens DAC without changing the SELinux decision.

---

### SELinux Modes

Show the current mode:

```bash
getenforce
```

Detailed status:

```bash
sestatus
```

| Mode | Behavior |
|---|---|
| `Enforcing` | Policy denials are blocked and logged. |
| `Permissive` | Denials are logged but not blocked. |
| `Disabled` | SELinux is inactive. Labels may become stale while it is disabled. |

Show persistent configuration:

```bash
grep -vE '^[[:space:]]*(#|$)' /etc/selinux/config
```

Temporarily switch to permissive mode:

```bash
setenforce 0
```

Return to enforcing:

```bash
setenforce 1
```

`setenforce` cannot activate SELinux if it was disabled at boot.

Permissive mode is a diagnostic tool, not a root-cause fix. Collect the AVC denial and correct the label, boolean, port type, application path, or policy.

---

### SELinux Contexts

Show a file context:

```bash
ls -lZ /path/to/file
```

Show a directory context:

```bash
ls -Zd /path/to/directory
```

Show process contexts:

```bash
ps -eZ
```

One process:

```bash
ps -p PID -o pid,user,label,comm,args
```

Show the current shell context:

```bash
id -Z
```

A context normally appears as:

```text
selinux_user:role:type:level
```

Example:

```text
system_u:object_r:httpd_sys_content_t:s0
```

| Field | Meaning |
|---|---|
| SELinux user | SELinux identity mapped to a login or system object |
| Role | Role-based access-control field |
| Type | Main field used by targeted-policy type enforcement |
| Level | MLS or MCS sensitivity and category data |

For normal service troubleshooting, the **type** is usually the most important field.

Examples:

- Apache process domain: `httpd_t`
- Readable web content: `httpd_sys_content_t`
- Writable web content: `httpd_sys_rw_content_t`
- Generic temporary files: `tmp_t`
- Incorrectly labeled custom content: often `default_t`

SELinux policy commonly states which process domain can perform which operation on an object type.

---

### Current Labels and Expected Labels

Show the current context:

```bash
ls -lZ /srv/myapp/config.yml
```

Show the context expected by policy:

```bash
matchpathcon /srv/myapp/config.yml
```

Verify whether the current label matches:

```bash
matchpathcon -V /srv/myapp/config.yml
```

Show the context through `stat`:

```bash
stat -c '%C %n' /srv/myapp/config.yml
```

List file-context rules:

```bash
semanage fcontext -l
```

Show local customizations:

```bash
semanage fcontext -C -l
```

Search for related mappings:

```bash
semanage fcontext -l | grep -E '/srv/myapp|httpd'
```

If `semanage` is missing:

```bash
dnf provides '*/semanage'
```

On RHEL-family systems, it is commonly provided by `policycoreutils-python-utils`.

---

### `chcon`, `semanage fcontext`, and `restorecon`

Temporarily change a label:

```bash
chcon -t httpd_sys_content_t /srv/web/index.html
```

A `chcon` change does not create a persistent pathname rule. It can be overwritten by:

- `restorecon`
- A full filesystem relabel
- File replacement
- Some deployment or package operations

Create a persistent mapping:

```bash
semanage fcontext -a -t httpd_sys_content_t '/srv/web(/.*)?'
```

Apply the mapping:

```bash
restorecon -Rv /srv/web
```

Modify an existing mapping:

```bash
semanage fcontext -m -t httpd_sys_rw_content_t '/srv/web/uploads(/.*)?'
```

Delete a local mapping:

```bash
semanage fcontext -d '/srv/web(/.*)?'
```

Preview relabeling without changing files:

```bash
restorecon -nRv /srv/web
```

Recommended workflow:

```bash
semanage fcontext -a -t TYPE '/custom/path(/.*)?'
restorecon -Rv /custom/path
matchpathcon -V /custom/path
```

---

### Read-Only and Writable Web Content

Read-only application content:

```bash
semanage fcontext -a -t httpd_sys_content_t '/srv/site(/.*)?'
```

A narrow writable upload directory:

```bash
semanage fcontext -a -t httpd_sys_rw_content_t '/srv/site/uploads(/.*)?'
```

Apply:

```bash
restorecon -Rv /srv/site
```

Verify:

```bash
ls -lZR /srv/site
```

Do not label the entire site writable merely because one directory requires uploads.

---

### SELinux Booleans

List boolean states:

```bash
getsebool -a
```

Search:

```bash
getsebool -a | grep httpd
```

Show descriptions and persistent state:

```bash
semanage boolean -l | grep httpd
```

Change temporarily:

```bash
setsebool httpd_can_network_connect on
```

Change persistently:

```bash
setsebool -P httpd_can_network_connect on
```

Disable persistently:

```bash
setsebool -P httpd_can_network_connect off
```

Before enabling a boolean:

1. Read its description.
2. Confirm it matches intended behavior.
3. Understand the scope of access it broadens.
4. Test the original application request.
5. Recheck AVC logs.

Do not enable multiple booleans just because their names appear related.

---

### SELinux Port Types

A service may be denied permission to bind a port even if:

- The port is unused
- The firewall permits it
- The process runs as root

List SELinux port mappings:

```bash
semanage port -l
```

Search HTTP ports:

```bash
semanage port -l | grep '^http_port_t'
```

Allow an HTTP service to bind TCP port `8088`:

```bash
semanage port -a -t http_port_t -p tcp 8088
```

If the port already exists under another type, review the conflict before modifying it:

```bash
semanage port -m -t http_port_t -p tcp 8088
```

Delete a local mapping:

```bash
semanage port -d -t http_port_t -p tcp 8088
```

Show local port customizations:

```bash
semanage port -C -l
```

SELinux and the firewall are separate controls:

```bash
semanage port -a -t http_port_t -p tcp 8088
firewall-cmd --add-port=8088/tcp
```

After testing:

```bash
firewall-cmd --runtime-to-permanent
```

---

### SELinux Login Mappings

Show Linux-login to SELinux-user mappings:

```bash
semanage login -l
```

Show SELinux users:

```bash
semanage user -l
```

Show the current login context:

```bash
id -Z
```

Advanced systems may map administrators to confined SELinux users such as `staff_u`.

Example:

```bash
semanage login -a -s staff_u alice
```

Modify:

```bash
semanage login -m -s staff_u alice
```

Delete a local mapping:

```bash
semanage login -d alice
```

These changes can affect remote and administrative access. Test them in a controlled environment.

---

### Finding AVC Denials

Confirm audit logging:

```bash
systemctl status auditd
```

Search recent denials:

```bash
ausearch -m AVC,USER_AVC -ts recent
```

Readable output:

```bash
ausearch -m AVC,USER_AVC -ts recent -i
```

Search since boot:

```bash
ausearch -m AVC,USER_AVC -ts boot -i
```

Search by process name:

```bash
ausearch -m AVC,USER_AVC -ts recent -c httpd -i
```

Search by PID:

```bash
ausearch -m AVC,USER_AVC -p PID -i
```

Important fields:

| Field | Meaning |
|---|---|
| `scontext` | Source process context |
| `tcontext` | Target object context |
| `tclass` | Object class such as file, directory, or socket |
| `{ read }` | Requested operation that was denied |
| `comm` | Command name |
| `exe` | Executable path |
| `name` or `path` | Target object information |

Example:

```text
scontext=system_u:system_r:httpd_t:s0
tcontext=unconfined_u:object_r:default_t:s0
tclass=file
{ read }
```

This usually points to an incorrectly labeled file. The likely fix is a persistent context mapping and `restorecon`, not a broad allow rule.

---

### `audit2why` and `sealert`

Explain selected AVC records:

```bash
ausearch -m AVC,USER_AVC -ts recent --raw | audit2why
```

Analyze the audit log:

```bash
sealert -a /var/log/audit/audit.log
```

Show one alert:

```bash
sealert -l ALERT_ID
```

These tools provide suggestions, not guaranteed correct fixes.

Compare every suggestion with:

- Intended application behavior
- Existing booleans
- Current and expected labels
- Port mappings
- Least-privilege requirements

---

### Local SELinux Policy Modules

Create a local module only after checking:

1. File labels
2. Port labels
3. Existing booleans
4. Application configuration
5. Existing policy packages

Generate a candidate module for one process:

```bash
ausearch -m AVC,USER_AVC -ts recent -c myapp --raw \
  | audit2allow -M myapp_local
```

Review the generated source:

```bash
cat myapp_local.te
```

Install only after reviewing every permission:

```bash
semodule -i myapp_local.pp
```

List modules:

```bash
semodule -l
```

Remove the module:

```bash
semodule -r myapp_local
```

Do not automatically allow every denial in the complete audit log. It can contain unrelated failures or malicious attempts.

---

### Per-Domain Permissive Mode

Instead of making the entire system permissive, one domain can be made permissive temporarily.

List permissive domains:

```bash
semanage permissive -l
```

Add one domain:

```bash
semanage permissive -a httpd_t
```

Reproduce the problem and inspect denials:

```bash
ausearch -m AVC,USER_AVC -ts recent -i
```

Remove the exception:

```bash
semanage permissive -d httpd_t
```

This still weakens protection for that domain and must remain temporary.

---

### Relabeling and Recovery

Restore one file:

```bash
restorecon -v /path/to/file
```

Restore recursively:

```bash
restorecon -Rv /path/to/tree
```

Force a complete context reset for the tree:

```bash
restorecon -RFv /path/to/tree
```

Schedule a complete relabel at boot:

```bash
touch /.autorelabel
reboot
```

Alternative:

```bash
fixfiles -F onboot
```

A complete relabel can take significant time.

Use it when:

- SELinux was disabled and is being re-enabled
- Labels are broadly corrupted
- A filesystem was restored without extended attributes
- Many unrelated paths have incorrect labels

Do not perform a full relabel for one mislabeled file.

---

### SELinux Troubleshooting Workflow

#### Reproduce and timestamp the failure

Record:

- User
- Process
- Path or port
- Exact operation
- Exact time

#### Check DAC and ACLs

```bash
namei -l /path/to/object
getfacl /path/to/object
sudo -u service_user test -r /path/to/object
```

#### Inspect process and object contexts

```bash
ps -eZ | grep process_name
ls -lZ /path/to/object
```

#### Compare the expected label

```bash
matchpathcon -V /path/to/object
```

#### Read the AVC denial

```bash
ausearch -m AVC,USER_AVC -ts recent -i
```

#### Select the narrowest valid fix

- Wrong file type → `semanage fcontext` plus `restorecon`
- Custom port → `semanage port`
- Supported optional behavior → correct boolean
- Wrong path or application behavior → fix configuration
- Legitimate new policy requirement → reviewed local module

#### Verify in enforcing mode

```bash
setenforce 1
getenforce
```

Retest and check for new AVC records.

---

### `umask` and Default Permissions

Show the current mask:

```bash
umask
```

Symbolic form:

```bash
umask -S
```

Set a restrictive mask:

```bash
umask 027
```

Common results:

- Regular file requested as `0666` → `0640`
- Directory requested as `0777` → `0750`

Show a systemd service mask:

```bash
systemctl show service_name -p UMask
```

Example override:

```ini
[Service]
UMask=0027
```

A strict mask can break group collaboration, shared directories, or log readers. Test service behavior.

---

### Setuid, Setgid, and Sticky Bit

Find setuid files:

```bash
find / -xdev -type f -perm -4000 -ls 2>/dev/null
```

Find setgid files:

```bash
find / -xdev -type f -perm -2000 -ls 2>/dev/null
```

Find both:

```bash
find / -xdev -type f -perm /6000 -ls 2>/dev/null
```

Setgid on a shared directory commonly preserves group ownership:

```bash
chmod g+s /shared
```

Use the sticky bit for a shared writable directory:

```bash
chmod 1777 /shared/tmp
```

Find world-writable directories without the sticky bit:

```bash
find / -xdev -type d -perm -0002 ! -perm -1000 -ls 2>/dev/null
```

Review unexpected privileged files against package ownership and approved business need.

---

### Linux Capabilities

Show file capabilities:

```bash
getcap -r / 2>/dev/null
```

Show process capabilities:

```bash
getpcaps PID
```

Show the current shell capability state:

```bash
capsh --print
```

Allow one binary to bind a privileged port without setuid root:

```bash
setcap cap_net_bind_service=+ep /usr/local/bin/myserver
```

Verify:

```bash
getcap /usr/local/bin/myserver
```

Remove capabilities:

```bash
setcap -r /usr/local/bin/myserver
```

Capabilities can be lost when a binary is replaced. Recheck after upgrades or deployments.

Avoid granting broad capabilities such as `cap_sys_admin` unless absolutely required.

---

### Account and Password Review

Show identity:

```bash
id username
```

Resolve through NSS:

```bash
getent passwd username
getent group groupname
```

Find accounts with UID `0`:

```bash
awk -F: '$3 == 0 {print $1 ":" $7}' /etc/passwd
```

Show password state:

```bash
passwd -S username
```

Show aging:

```bash
chage -l username
```

Lock:

```bash
usermod -L username
```

Unlock:

```bash
usermod -U username
```

A password lock may not disable SSH keys, tokens, or existing sessions. Review every access method.

Disable interactive login for a service account:

```bash
usermod -s /sbin/nologin service_user
```

Review login history:

```bash
last -ai | head -30
lastb -ai | head -30
lastlog
```

---

### PAM, `authselect`, and `faillock`

Important paths:

```text
/etc/pam.d/
/etc/security/pwquality.conf
/etc/security/pwquality.conf.d/
/etc/security/faillock.conf
/etc/login.defs
```

Show the active RHEL authselect profile:

```bash
authselect current
```

Validate it:

```bash
authselect check
```

Avoid directly editing generated PAM files when `authselect` manages them. Use an appropriate profile or custom profile.

Show one user's failed-login state:

```bash
faillock --user username
```

Reset after confirming the user and cause:

```bash
faillock --user username --reset
```

Search authentication failures:

```bash
journalctl --since "1 hour ago" \
  | grep -iE 'authentication failure|failed password|pam_faillock'
```

An overly aggressive lockout policy can allow attackers to lock legitimate accounts.

---

### Sudo Security

Edit policy safely:

```bash
visudo
```

Edit a drop-in:

```bash
visudo -f /etc/sudoers.d/application-admins
```

Validate everything:

```bash
visudo -c
```

Validate one file:

```bash
visudo -cf /etc/sudoers.d/application-admins
```

Set secure ownership and mode:

```bash
chown root:root /etc/sudoers.d/application-admins
chmod 0440 /etc/sudoers.d/application-admins
```

Show a user's allowed commands:

```bash
sudo -l -U username
```

Narrow example:

```text
alice ALL=(root) /usr/bin/systemctl status httpd.service, /usr/bin/systemctl restart httpd.service
```

Avoid broad rules such as:

```text
alice ALL=(ALL) NOPASSWD: ALL
```

unless full unrestricted administration is intended.

Commands that allow shell escapes, arbitrary file writes, editor execution, package installation, or unit modification can become root-equivalent.

Search sudo activity:

```bash
journalctl _COMM=sudo --since "today"
ausearch -m USER_CMD -ts today -i
```

---

### SSH Server Hardening

Important paths:

```text
/etc/ssh/sshd_config
/etc/ssh/sshd_config.d/*.conf
~/.ssh/authorized_keys
/etc/ssh/ssh_host_*
```

Back up configuration:

```bash
cp -a /etc/ssh/sshd_config \
  /etc/ssh/sshd_config.$(date +%F-%H%M%S).bak
```

Validate syntax:

```bash
sshd -t
```

Show effective configuration:

```bash
sshd -T
```

Evaluate `Match` rules for a connection:

```bash
sshd -T -C user=alice,host=server.example.com,addr=192.0.2.10
```

Common settings to assess:

```text
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
MaxAuthTries 3
LoginGraceTime 30
AllowGroups sshusers
X11Forwarding no
PermitTunnel no
```

> **Warning:** Do not copy these blindly. Forwarding or tunneling may be a legitimate requirement.

Before disabling passwords:

1. Confirm key authentication.
2. Keep an existing session open.
3. Test a second session.
4. Confirm console or recovery access.

Reload after validation:

```bash
systemctl reload sshd
```

Verify:

```bash
systemctl status sshd
journalctl -u sshd --since "10 minutes ago"
```

Secure user key files:

```bash
chmod 700 /home/username/.ssh
chmod 600 /home/username/.ssh/authorized_keys
chown -R username:username /home/username/.ssh
restorecon -Rv /home/username/.ssh
```

---

### Firewall Hardening

Show active zones:

```bash
firewall-cmd --get-active-zones
```

Show a zone:

```bash
firewall-cmd --zone=public --list-all
```

List predefined services:

```bash
firewall-cmd --get-services
```

Add a service temporarily:

```bash
firewall-cmd --zone=public --add-service=https
```

Allow one source network:

```bash
firewall-cmd --zone=internal --add-source=192.0.2.0/24
```

Narrow rich rule:

```bash
firewall-cmd --zone=public \
  --add-rich-rule='rule family="ipv4" source address="192.0.2.10" service name="ssh" accept'
```

List rich rules:

```bash
firewall-cmd --zone=public --list-rich-rules
```

Validate permanent configuration:

```bash
firewall-cmd --check-config
```

Persist tested runtime changes:

```bash
firewall-cmd --runtime-to-permanent
```

Inspect nftables:

```bash
nft list ruleset -a
```

Expose only required services to the narrowest required sources.

---

### Auditd

Show service and subsystem status:

```bash
systemctl status auditd
auditctl -s
```

List active rules:

```bash
auditctl -l
```

Persistent rules:

```text
/etc/audit/rules.d/*.rules
```

Check and load generated rules:

```bash
augenrules --check
augenrules --load
```

Temporary watch:

```bash
auditctl -w /etc/ssh/sshd_config -p wa -k sshd_config
```

Search:

```bash
ausearch -k sshd_config -i
```

Remove the temporary watch:

```bash
auditctl -W /etc/ssh/sshd_config -k sshd_config
```

Persistent examples:

```text
-w /etc/ssh/sshd_config -p wa -k sshd_config
-w /etc/sudoers -p wa -k sudo_policy
-w /etc/sudoers.d/ -p wa -k sudo_policy
```

Permission-change syscall rule:

```text
-a always,exit -F arch=b64 -S chmod,fchmod,fchmodat -F auid>=1000 -F auid!=unset -k permission_change
```

On 64-bit hosts, some policies require matching `b32` and `b64` rules.

Reports:

```bash
aureport -au -i
aureport -x --summary -i
```

Audit rules can create high event volume. Monitor disk use and test filters.

---

### Package and File Integrity

Find package ownership:

```bash
rpm -qf /path/to/file
```

Verify one package:

```bash
rpm -V package_name
```

Verify all packages:

```bash
rpm -Va
```

Check an RPM signature:

```bash
rpmkeys --checksig package-file.rpm
```

List security advisories:

```bash
dnf updateinfo list --security
```

Show advisory details:

```bash
dnf updateinfo info --security
```

Apply approved security updates:

```bash
dnf upgrade --security
```

#### AIDE

Install:

```bash
dnf install aide
```

Initialize:

```bash
aide --init
```

Check integrity:

```bash
aide --check
```

Important paths:

```text
/etc/aide.conf
/var/lib/aide/
```

The initial database must be created from a trusted system. A baseline created after compromise may record malicious files as normal.

---

### systemd Service Sandboxing

Assess a unit:

```bash
systemd-analyze security service_name
```

This is a review aid, not proof of security.

Inspect configuration:

```bash
systemctl cat service_name
```

Create an override:

```bash
systemctl edit service_name
```

Common hardening directives:

```ini
[Service]
NoNewPrivileges=yes
PrivateTmp=yes
ProtectSystem=strict
ProtectHome=yes
ProtectKernelTunables=yes
ProtectKernelModules=yes
ProtectControlGroups=yes
RestrictSUIDSGID=yes
LockPersonality=yes
CapabilityBoundingSet=
RestrictAddressFamilies=AF_UNIX AF_INET AF_INET6
```

Allow narrow writable paths:

```ini
[Service]
ProtectSystem=strict
ReadWritePaths=/var/lib/myapp /var/log/myapp
```

Allow one capability:

```ini
[Service]
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_BIND_SERVICE
NoNewPrivileges=yes
```

Apply and test:

```bash
systemctl daemon-reload
systemctl restart service_name
systemctl status service_name --no-pager -l
journalctl -u service_name --since "5 minutes ago"
```

Add restrictions incrementally and document every required exception.

---

### Mount-Option Hardening

Show mount options:

```bash
findmnt -o TARGET,SOURCE,FSTYPE,OPTIONS
```

Inspect one path:

```bash
findmnt -T /path
```

| Option | Effect |
|---|---|
| `nodev` | Device nodes are not interpreted as devices |
| `nosuid` | Setuid, setgid, and file capabilities are not honored |
| `noexec` | Direct execution from the filesystem is blocked |
| `ro` | Filesystem is read-only |

Temporary remount:

```bash
mount -o remount,nodev,nosuid,noexec /mountpoint
```

Validate **`/etc/fstab`** changes:

```bash
mount -av
```

Caveats:

- `noexec` does not stop a readable script from being passed to an interpreter.
- `nosuid` can break programs requiring setuid or file capabilities.
- Containers and application runtimes may require specific options.
- **`/tmp`**, **`/home`**, **`/var`**, and application filesystems have different needs.

---

### Crypto Policies and FIPS

Show the current RHEL crypto policy:

```bash
update-crypto-policies --show
```

Common policies:

| Policy | Purpose |
|---|---|
| `DEFAULT` | Normal recommended policy |
| `FUTURE` | Stronger policy that may break old peers |
| `LEGACY` | Older compatibility with weaker security |
| `FIPS` | FIPS-oriented system policy |

Set:

```bash
update-crypto-policies --set DEFAULT
```

Changing policy can affect SSH, TLS, Kerberos, IPsec, and applications using system libraries.

Do not leave the system in `LEGACY` merely to support one obsolete client. Prefer upgrading or isolating that peer.

Check FIPS mode:

```bash
fips-mode-setup --check
```

A validated FIPS deployment is a planned system-lifecycle change and normally requires proper enablement and reboot.

---

### Security-Relevant sysctl Review

Inspect selected settings:

```bash
sysctl \
  kernel.randomize_va_space \
  fs.protected_hardlinks \
  fs.protected_symlinks \
  net.ipv4.conf.all.accept_redirects \
  net.ipv4.conf.all.send_redirects
```

Show merged sysctl configuration:

```bash
systemd-analyze cat-config sysctl.d
```

Persistent sources:

```text
/etc/sysctl.conf
/etc/sysctl.d/*.conf
/usr/lib/sysctl.d/*.conf
```

Apply reviewed settings:

```bash
sysctl --system
```

Do not paste generic hardening lists into production without reviewing routing, container, cluster, and application requirements.

---

### Suspected-Compromise Triage

Do not immediately reboot or kill a suspicious process unless containment urgency is greater than the value of evidence.

#### Record system identity and time

```bash
date --iso-8601=seconds
hostnamectl
uptime
```

#### Record users and logins

```bash
w
who -a
last -ai | head -50
lastb -ai | head -50
```

#### Record processes

```bash
ps -eo pid,ppid,user,lstart,stat,%cpu,%mem,exe,args --sort=-%cpu
pstree -ap
```

Inspect one process executable:

```bash
readlink -f /proc/PID/exe
ls -l /proc/PID/exe
```

#### Record network state

```bash
ss -lntup
ss -ntup
lsof -nP -i
```

#### Review persistence

```bash
systemctl list-unit-files --state=enabled
systemctl list-timers --all
ls -la /etc/cron.* /var/spool/cron 2>/dev/null
```

One user's crontab:

```bash
crontab -l -u username
```

#### Search recent temporary files

```bash
find /tmp /var/tmp /dev/shm -xdev -type f -mtime -2 -ls 2>/dev/null
```

#### Review recent configuration changes

```bash
find /etc -xdev -type f -mtime -2 \
  -printf '%TY-%Tm-%Td %TH:%TM:%TS %p\n' 2>/dev/null | sort
```

#### Review privilege mechanisms

```bash
find / -xdev -type f -perm /6000 -ls 2>/dev/null
getcap -r / 2>/dev/null
```

#### Hash and record suspicious files

```bash
sha256sum /path/to/file
stat /path/to/file
getfacl /path/to/file
ls -lZ /path/to/file
```

Store evidence on a trusted destination under the incident-response procedure. A potentially compromised host cannot be assumed to report every fact accurately.

---

### Security Baseline Checklist

#### Accounts

```bash
awk -F: '$3 == 0 {print $1}' /etc/passwd
getent group wheel
lastlog
```

#### Sudo

```bash
visudo -c
find /etc/sudoers.d -maxdepth 1 -type f -ls
```

#### SSH

```bash
sshd -t
sshd -T | grep -E \
  'permitrootlogin|passwordauthentication|pubkeyauthentication|maxauthtries|allowgroups'
```

#### SELinux

```bash
getenforce
sestatus
semanage fcontext -C -l
semanage port -C -l
semanage permissive -l
```

#### Firewall and sockets

```bash
firewall-cmd --get-active-zones
firewall-cmd --list-all
ss -lntup
```

#### Privileged files

```bash
find / -xdev -type f -perm /6000 -ls 2>/dev/null
getcap -r / 2>/dev/null
```

#### Audit

```bash
auditctl -s
auditctl -l
```

#### Updates and integrity

```bash
dnf updateinfo list --security
rpm -Va
```

#### Services and timers

```bash
systemctl --failed
systemctl list-unit-files --state=enabled
systemctl list-timers --all
```

Record approved exceptions. A baseline is useful only when changes can be compared with known expected state.

---

### Important Security Files

| Path | Purpose |
|---|---|
| **`/etc/selinux/config`** | Persistent SELinux mode and policy |
| **`/var/log/audit/audit.log`** | Audit and SELinux AVC records |
| **`/etc/audit/auditd.conf`** | Audit daemon configuration |
| **`/etc/audit/rules.d/*.rules`** | Persistent audit rules |
| **`/etc/passwd`** | Accounts and login shells |
| **`/etc/shadow`** | Password hashes and aging |
| **`/etc/group`** | Groups and membership |
| **`/etc/pam.d/`** | PAM service policies |
| **`/etc/security/pwquality.conf`** | Password-quality policy |
| **`/etc/security/faillock.conf`** | Failed-login lockout policy |
| **`/etc/sudoers`** | Main sudo policy |
| **`/etc/sudoers.d/`** | Sudo drop-ins |
| **`/etc/ssh/sshd_config`** | SSH server configuration |
| **`/etc/ssh/sshd_config.d/`** | SSH configuration drop-ins |
| **`/etc/firewalld/`** | Persistent firewalld state |
| **`/etc/sysctl.conf`** | Legacy persistent sysctl file |
| **`/etc/sysctl.d/`** | Persistent sysctl drop-ins |
| **`/etc/aide.conf`** | AIDE integrity policy |
| **`/var/lib/aide/`** | AIDE databases |
| **`/etc/crypto-policies/`** | System crypto-policy state |
| **`/etc/systemd/system/`** | Local units and hardening overrides |

---

### Security Command Index

```bash
getenforce
sestatus
setenforce 0
setenforce 1
ls -lZ /path
ls -Zd /directory
ps -eZ
id -Z
matchpathcon -V /path
restorecon -Rv /path
semanage fcontext -C -l
semanage port -C -l
semanage permissive -l
getsebool -a
setsebool -P BOOLEAN on
ausearch -m AVC,USER_AVC -ts recent -i
audit2why
sealert -a /var/log/audit/audit.log
semodule -l
auditctl -s
auditctl -l
augenrules --check
aureport -au -i
visudo -c
sudo -l -U username
sshd -t
sshd -T
faillock --user username
authselect current
firewall-cmd --get-active-zones
nft list ruleset -a
getcap -r /
getpcaps PID
systemd-analyze security service_name
update-crypto-policies --show
fips-mode-setup --check
rpm -V package_name
dnf updateinfo list --security
aide --check
```

<a id="linux-storage-deep-dive"></a>
## Linux Storage Deep Dive

Linux storage troubleshooting becomes much easier when the device stack is understood from top to bottom.

A common stack is:

```text
Physical or virtual disk
        ↓
Partition table
        ↓
Partition
        ↓
LVM Physical Volume (optional)
        ↓
Volume Group (optional)
        ↓
Logical Volume (optional)
        ↓
Filesystem
        ↓
Mount point
        ↓
Application data
```

Other stacks may include:

- Software RAID with `mdadm`
- Device Mapper
- LUKS encryption
- Multipath
- Thin provisioning
- VDO compression and deduplication
- Stratis
- Network filesystems such as NFS

The correct troubleshooting question is not only:

> Is the disk full?

It is:

> Which layer is full, missing, inactive, corrupted, or misconfigured?

---

### Storage Safety Rules

Before changing storage:

1. Identify the exact device.
2. Confirm whether the device contains data.
3. Confirm the filesystem type.
4. Confirm whether it is mounted.
5. Confirm whether LVM, RAID, encryption, or multipath is involved.
6. Save current configuration and metadata.
7. Take or verify a backup.
8. Use read-only inspection commands first.
9. Expand one layer at a time.
10. Verify after every change.

Useful identification commands:

```bash
lsblk -f
findmnt
blkid
pvs
vgs
lvs -a -o +devices
cat /proc/mdstat
```

Never copy destructive commands directly from notes without replacing placeholder device names and verifying them.

The following commands can permanently destroy data when used against the wrong target:

```bash
mkfs
wipefs
fdisk
parted
pvcreate
vgremove
lvremove
mdadm --create
dd
```

Use full device names and verify with `lsblk` immediately before execution.

---

### Discover the Storage Topology

Show block devices:

```bash
lsblk
```

Show filesystems, labels, and UUIDs:

```bash
lsblk -f
```

Detailed topology:

```bash
lsblk -o NAME,PATH,MAJ:MIN,SIZE,TYPE,FSTYPE,FSVER,LABEL,UUID,MOUNTPOINTS
```

Show parent-child relationships:

```bash
lsblk -s /dev/DEVICE
```

Show the complete path from a filesystem to the backing device:

```bash
lsblk -o NAME,TYPE,SIZE,FSTYPE,MOUNTPOINTS,PKNAME
```

Show device UUIDs and signatures:

```bash
blkid
```

Inspect one device:

```bash
blkid /dev/DEVICE
```

Show mounted filesystems:

```bash
findmnt
```

Find the filesystem containing one path:

```bash
findmnt -T /path/to/file
```

Show source, type, options, and target:

```bash
findmnt -o SOURCE,FSTYPE,OPTIONS,TARGET
```

Show kernel block devices:

```bash
cat /proc/partitions
```

Show device-mapper relationships:

```bash
dmsetup ls --tree
```

Show udev properties:

```bash
udevadm info --query=all --name=/dev/DEVICE
```

Show SCSI devices:

```bash
lsscsi
```

If `lsscsi` is missing:

```bash
dnf provides '*/lsscsi'
```

---

### Confirm Device Identity

Do not depend only on names such as **`/dev/sdb`**.

Device names can change after reboot, hardware changes, or discovery-order changes.

Show stable identifiers:

```bash
ls -l /dev/disk/by-id/
ls -l /dev/disk/by-uuid/
ls -l /dev/disk/by-path/
```

Resolve one symbolic link:

```bash
readlink -f /dev/disk/by-id/DEVICE_ID
```

Show device model and serial number:

```bash
lsblk -d -o NAME,SIZE,MODEL,SERIAL,WWN
```

For a SCSI disk:

```bash
udevadm info --query=property --name=/dev/sdb \
  | grep -E 'ID_MODEL=|ID_SERIAL=|ID_WWN='
```

For production storage, record:

- Device path
- WWN or serial
- Size
- Filesystem
- LVM membership
- Mount point
- Application owner

---

### MBR and GPT

#### MBR

MBR is an older partition-table format.

Important limitations:

- Commonly limited to approximately 2 TiB with 512-byte sectors
- Four primary partition entries
- More partitions require an extended partition
- Stores critical metadata near the beginning of the disk

#### GPT

GPT is the modern partition-table format.

Advantages:

- Supports large disks
- Supports many partitions
- Stores backup partition metadata
- Uses partition GUIDs
- Includes integrity checks for partition metadata
- Works well with UEFI systems

Inspect a partition table:

```bash
fdisk -l /dev/DEVICE
```

Using `parted`:

```bash
parted /dev/DEVICE print
```

Using `gdisk` where installed:

```bash
gdisk -l /dev/DEVICE
```

Show all disks:

```bash
fdisk -l
```

---

### Create a GPT Partition with `parted`

Start interactively:

```bash
parted /dev/sdb
```

Inside `parted`:

```text
print
mklabel gpt
mkpart primary 1MiB 100%
print
quit
```

Non-interactive example:

```bash
parted -s /dev/sdb mklabel gpt
parted -s /dev/sdb mkpart primary 1MiB 100%
```

For an LVM partition:

```bash
parted -s /dev/sdb set 1 lvm on
```

Display alignment:

```bash
parted /dev/sdb align-check optimal 1
```

Request the kernel to reread the partition table:

```bash
partprobe /dev/sdb
```

Wait for udev processing:

```bash
udevadm settle
```

Verify:

```bash
lsblk /dev/sdb
```

Creating a new partition table destroys the previous partition-table definition. Confirm the disk is empty before `mklabel`.

---

### Create a Partition with `fdisk`

Open the device:

```bash
fdisk /dev/sdb
```

Common interactive commands:

| Key | Meaning |
|---|---|
| `p` | Print partition table |
| `g` | Create GPT |
| `o` | Create DOS or MBR table |
| `n` | New partition |
| `d` | Delete partition |
| `t` | Change partition type |
| `w` | Write changes |
| `q` | Quit without writing |
| `m` | Help |

Always print the table before writing:

```text
p
```

After writing:

```bash
partprobe /dev/sdb
udevadm settle
lsblk -f /dev/sdb
```

---

### Back Up and Restore Partition Tables

Back up an MBR or GPT layout with `sfdisk`:

```bash
sfdisk --dump /dev/sdb > /root/sdb.partition-table
```

Inspect the backup:

```bash
cat /root/sdb.partition-table
```

Restore only to the correct target disk:

```bash
sfdisk /dev/sdb < /root/sdb.partition-table
```

GPT-specific backup with `sgdisk`:

```bash
sgdisk --backup=/root/sdb.gpt-backup /dev/sdb
```

Verify GPT metadata:

```bash
sgdisk --verify /dev/sdb
```

Restore:

```bash
sgdisk --load-backup=/root/sdb.gpt-backup /dev/sdb
```

Partition-table backups do not contain filesystem data.

---

### Inspect and Remove Old Signatures

Show signatures without changing them:

```bash
wipefs /dev/DEVICE
```

Show one partition:

```bash
wipefs /dev/sdb1
```

A device can retain signatures from:

- Filesystems
- LVM
- RAID
- Partition tables
- Swap

Remove signatures only from a confirmed disposable device:

```bash
wipefs -a /dev/DEVICE
```

Preview destructive signature removal:

```bash
wipefs --no-act -a /dev/DEVICE
```

Use the preview first.

An old signature can cause:

- Filesystem auto-detection confusion
- LVM warnings
- RAID assembly problems
- Installer refusal
- Wrong mount behavior

Do not remove signatures from a device merely because a warning appears. Identify the intended storage stack first.

---

### Create Filesystems

#### XFS

```bash
mkfs.xfs /dev/DEVICE
```

Force only after verifying the device:

```bash
mkfs.xfs -f /dev/DEVICE
```

Assign a label:

```bash
mkfs.xfs -L application_data /dev/DEVICE
```

#### ext4

```bash
mkfs.ext4 /dev/DEVICE
```

Assign a label:

```bash
mkfs.ext4 -L application_data /dev/DEVICE
```

#### Verify

```bash
lsblk -f /dev/DEVICE
blkid /dev/DEVICE
```

Creating a filesystem destroys previous filesystem metadata on the target.

---

### Filesystem Labels and UUIDs

Show UUID and label:

```bash
blkid /dev/DEVICE
```

#### XFS label

Show:

```bash
xfs_admin -l /dev/DEVICE
```

Set:

```bash
xfs_admin -L new_label /dev/DEVICE
```

The filesystem normally must be unmounted for `xfs_admin`.

#### ext4 label

Show:

```bash
e2label /dev/DEVICE
```

Set:

```bash
e2label /dev/DEVICE new_label
```

Alternative:

```bash
tune2fs -L new_label /dev/DEVICE
```

Mount by label:

```bash
mount LABEL=new_label /mountpoint
```

Mount by UUID:

```bash
mount UUID=FILESYSTEM_UUID /mountpoint
```

UUID-based **`/etc/fstab`** entries are usually safer than **`/dev/sdX`** names.

---

### Mount and Unmount

Create a mount point:

```bash
mkdir -p /data
```

Mount:

```bash
mount /dev/DEVICE /data
```

Specify type when required:

```bash
mount -t xfs /dev/DEVICE /data
```

Show the result:

```bash
findmnt /data
```

Show mount options:

```bash
findmnt -no SOURCE,FSTYPE,OPTIONS,TARGET /data
```

Unmount:

```bash
umount /data
```

Unmount by device:

```bash
umount /dev/DEVICE
```

Check whether a path is a mount point:

```bash
mountpoint /data
```

Return status only:

```bash
mountpoint -q /data
echo $?
```

A lazy unmount:

```bash
umount -l /data
```

A forced unmount:

```bash
umount -f /data
```

Lazy and forced unmounts are not normal first choices. They can hide active-use problems or create application inconsistency.

---

### **`/etc/fstab`**

Show configured mounts:

```bash
cat /etc/fstab
```

Typical entry:

```text
UUID=FILESYSTEM_UUID  /data  xfs  defaults  0  0
```

Fields:

| Field | Meaning |
|---|---|
| Source | UUID, label, device, or network source |
| Target | Mount point |
| Type | Filesystem type |
| Options | Mount behavior |
| Dump | Legacy dump flag |
| Pass | Boot-time filesystem check order |

Common local-filesystem options:

| Option | Meaning |
|---|---|
| `defaults` | Standard default options |
| `ro` | Read-only |
| `rw` | Read-write |
| `noexec` | Prevent direct execution |
| `nosuid` | Ignore setuid, setgid, and capabilities |
| `nodev` | Ignore device nodes |
| `nofail` | Boot continues when the mount fails |
| `noatime` | Do not update access time |
| `discard` | Online discard; assess storage impact first |
| `x-systemd.automount` | Create a systemd automount |
| `x-systemd.device-timeout=10s` | Limit device wait time |

Back up before editing:

```bash
cp -a /etc/fstab /etc/fstab.$(date +%F-%H%M%S).bak
```

Validate syntax and references:

```bash
findmnt --verify --verbose
```

Test all unmounted entries:

```bash
mount -av
```

Reload systemd after changing **`/etc/fstab`**:

```bash
systemctl daemon-reload
```

List generated mount units:

```bash
systemctl list-units --type=mount
```

Failed mounts:

```bash
systemctl --failed --type=mount
```

Do not reboot to test **`/etc/fstab`**. Use `findmnt --verify` and `mount -av` first.

---

### Systemd Mount Unit Names

Convert a path to a unit name:

```bash
systemd-escape -p --suffix=mount /data
```

Result:

```text
data.mount
```

Show the generated unit:

```bash
systemctl cat data.mount
```

Status:

```bash
systemctl status data.mount
```

Journal:

```bash
journalctl -u data.mount -b
```

A mount point such as **`/var/lib/myapp`** becomes:

```text
var-lib-myapp.mount
```

---

### Capacity and Space Analysis

Show filesystem use:

```bash
df -hT
```

One path:

```bash
df -hT /var
```

Use POSIX output for scripting:

```bash
df -P /var
```

Show inode use:

```bash
df -i
```

Show directory totals:

```bash
du -xsh /var/*
```

Top-level sorted use:

```bash
du -xhd1 /var 2>/dev/null | sort -h
```

Find large files:

```bash
find /var -xdev -type f -size +1G \
  -printf '%s %p\n' 2>/dev/null | sort -n
```

Human-readable:

```bash
find /var -xdev -type f -size +1G -print0 2>/dev/null \
  | xargs -0 du -h | sort -h
```

Find recently changed large files:

```bash
find /var -xdev -type f -mtime -1 -size +100M -ls 2>/dev/null
```

Find deleted open files:

```bash
lsof +L1
```

On one mount:

```bash
lsof +L1 /var
```

`df` reports allocated filesystem blocks.

`du` walks visible directory entries.

A large difference commonly means:

- Deleted files still held open
- Hidden files beneath a mount
- Permissions prevented `du` from reading directories
- Snapshots or filesystem-specific metadata
- Different mount namespaces

---

### Inode Exhaustion

Show inode use:

```bash
df -i
```

Count files:

```bash
find /path -xdev -type f | wc -l
```

Find directories containing many files:

```bash
find /var -xdev -type f -printf '%h\n' 2>/dev/null \
  | sort | uniq -c | sort -n | tail -30
```

Find small-file concentrations:

```bash
find /var -xdev -type f -size -4k -printf '%h\n' 2>/dev/null \
  | sort | uniq -c | sort -n | tail -30
```

Common causes:

- Session directories
- Mail queues
- Application cache
- Temporary files
- One-file-per-event logging
- Package-manager caches
- Failed cleanup jobs

Freeing block space does not fix inode exhaustion unless directory entries are removed.

---

### XFS Inspection and Growth

Show XFS geometry:

```bash
xfs_info /mountpoint
```

Show filesystem usage:

```bash
df -hT /mountpoint
```

Grow XFS to the full size of its block device:

```bash
xfs_growfs /mountpoint
```

Grow by a specified number of data blocks:

```bash
xfs_growfs -D BLOCK_COUNT /mountpoint
```

XFS growth is performed while mounted.

Verify:

```bash
xfs_info /mountpoint
df -hT /mountpoint
```

XFS is normally grown using the mount point, not the block-device path.

Normal XFS administration supports growth but not shrinking.

---

### XFS Repair

Read-only metadata check:

```bash
xfs_repair -n /dev/DEVICE
```

Actual repair:

```bash
xfs_repair /dev/DEVICE
```

The filesystem normally must be unmounted.

If the filesystem contains the root filesystem, use rescue mode or alternate boot media.

> **Warning:** Do not use `xfs_repair -L` casually.

`-L` clears the log and can lose recent metadata changes. Use it only when the filesystem cannot be repaired normally and recovery impact is accepted.

Check kernel logs first:

```bash
journalctl -k -g 'XFS|I/O error|metadata'
```

Storage hardware or path failures must be corrected before trusting a filesystem repair.

---

### ext4 Inspection, Growth, and Shrink

Show ext filesystem details:

```bash
tune2fs -l /dev/DEVICE
```

Show superblock information:

```bash
dumpe2fs -h /dev/DEVICE
```

Grow ext4 to the full block-device size:

```bash
resize2fs /dev/DEVICE
```

ext4 can usually grow while mounted.

Read-only check:

```bash
e2fsck -n /dev/DEVICE
```

Offline forced check:

```bash
e2fsck -f /dev/DEVICE
```

Shrink ext4 only while unmounted:

```bash
e2fsck -f /dev/DEVICE
resize2fs /dev/DEVICE NEW_SIZE
```

After shrinking the filesystem, reduce the containing LV or partition carefully.

Shrinking is a high-risk maintenance operation because the layers must be reduced in the correct order:

1. Back up data.
2. Unmount.
3. Check filesystem.
4. Shrink filesystem.
5. Reduce LV or partition.
6. Remount.
7. Verify.

> **Warning:** Never reduce an LV before shrinking an ext filesystem inside it.

---

### Swap

Show active swap:

```bash
swapon --show
```

Alternative:

```bash
cat /proc/swaps
```

Show memory and swap:

```bash
free -h
```

Create a swap logical volume or partition:

```bash
mkswap /dev/DEVICE
```

Enable:

```bash
swapon /dev/DEVICE
```

Disable:

```bash
swapoff /dev/DEVICE
```

Enable all configured swap:

```bash
swapon -a
```

Example **`/etc/fstab`** entry:

```text
UUID=SWAP_UUID  none  swap  defaults  0  0
```

Show swap UUID:

```bash
blkid /dev/DEVICE
```

Set swap priority:

```text
UUID=SWAP_UUID  none  swap  defaults,pri=100  0  0
```

Show priorities:

```bash
swapon --show --output=NAME,TYPE,SIZE,USED,PRIO
```

> **Warning:** Do not run `swapoff` without checking that enough RAM is available to absorb used swap.

---

### Create a Swap File

Create a 4 GiB file:

```bash
fallocate -l 4G /swapfile
```

If the filesystem or platform does not support a suitable file through `fallocate`:

```bash
dd if=/dev/zero of=/swapfile bs=1M count=4096 status=progress
```

Secure it:

```bash
chmod 600 /swapfile
```

Initialize:

```bash
mkswap /swapfile
```

Enable:

```bash
swapon /swapfile
```

Persist:

```text
/swapfile  none  swap  defaults  0  0
```

Verify:

```bash
swapon --show
```

Swap-file support and restrictions depend on the filesystem and platform. Verify the target filesystem's documentation.

---

### LVM Concepts

LVM layers:

```text
Disk or partition
      ↓
PV — Physical Volume
      ↓
VG — Volume Group
      ↓
LV — Logical Volume
      ↓
Filesystem
```

Advantages:

- Flexible allocation
- Online expansion
- Multiple disks in one pool
- Snapshots
- Thin provisioning
- Device migration with `pvmove`

LVM does not replace backups.

---

### Inspect LVM

Compact reports:

```bash
pvs
vgs
lvs
```

More columns:

```bash
pvs -o pv_name,pv_size,pv_free,vg_name,pv_uuid
```

```bash
vgs -o vg_name,vg_size,vg_free,pv_count,lv_count
```

```bash
lvs -a -o lv_name,vg_name,lv_size,lv_attr,segtype,data_percent,metadata_percent,devices
```

Detailed views:

```bash
pvdisplay
vgdisplay
lvdisplay
```

Show one VG:

```bash
vgs vg_name
```

Show one LV:

```bash
lvs /dev/vg_name/lv_name
```

Show device-mapper tree:

```bash
dmsetup ls --tree
```

Show LVM devices:

```bash
lvs -a -o +devices
```

---

### Create LVM Storage

Initialize a PV:

```bash
pvcreate /dev/sdb1
```

Create a VG:

```bash
vgcreate vg_data /dev/sdb1
```

Create a 100 GiB LV:

```bash
lvcreate -L 100G -n lv_app vg_data
```

Use all free extents:

```bash
lvcreate -l 100%FREE -n lv_app vg_data
```

Create XFS:

```bash
mkfs.xfs /dev/vg_data/lv_app
```

Mount:

```bash
mkdir -p /app
mount /dev/vg_data/lv_app /app
```

Show UUID:

```bash
blkid /dev/vg_data/lv_app
```

Persist in **`/etc/fstab`**:

```text
UUID=FILESYSTEM_UUID  /app  xfs  defaults  0  0
```

Validate:

```bash
findmnt --verify --verbose
mount -av
findmnt /app
```

---

### Extend an LV and Filesystem Online

Check current layers:

```bash
findmnt -T /app
df -hT /app
lvs -o lv_name,vg_name,lv_size
vgs -o vg_name,vg_size,vg_free
```

Extend by 20 GiB and resize the filesystem automatically:

```bash
lvextend -r -L +20G /dev/vg_data/lv_app
```

Use all remaining VG free space:

```bash
lvextend -r -l +100%FREE /dev/vg_data/lv_app
```

Verify:

```bash
lvs /dev/vg_data/lv_app
df -hT /app
```

Without `-r`, extend the LV first:

```bash
lvextend -L +20G /dev/vg_data/lv_app
```

Then grow XFS:

```bash
xfs_growfs /app
```

Or grow ext4:

```bash
resize2fs /dev/vg_data/lv_app
```

Online growth is a common zero-downtime operation when all underlying layers are healthy.

---

### Extend After a Virtual Disk Was Enlarged

Assume the hypervisor enlarged **`/dev/sda`** and LVM uses partition **`/dev/sda3`**.

#### Confirm the operating system sees the new disk size

```bash
lsblk /dev/sda
blockdev --getsize64 /dev/sda
```

Rescan a SCSI disk if required:

```bash
echo 1 > /sys/class/block/sda/device/rescan
```

Verify again:

```bash
lsblk /dev/sda
```

#### Grow the partition

Using `growpart`:

```bash
growpart /dev/sda 3
```

If missing:

```bash
dnf provides '*/growpart'
```

Or use `parted` after backing up the partition table.

#### Ask the kernel to reread it

```bash
partprobe /dev/sda
udevadm settle
```

#### Grow the PV

```bash
pvresize /dev/sda3
```

#### Confirm VG free space

```bash
pvs
vgs
```

#### Extend LV and filesystem

```bash
lvextend -r -l +100%FREE /dev/vg_name/lv_name
```

#### Verify

```bash
lsblk
pvs
vgs
lvs
df -hT /mountpoint
```

The correct order is:

```text
Disk → Partition → PV → VG free extents → LV → Filesystem
```

---

### Add a New Disk to an Existing VG

Identify the new disk:

```bash
lsblk -d -o NAME,SIZE,MODEL,SERIAL
```

Create a partition if required, then:

```bash
pvcreate /dev/sdc1
```

Extend the VG:

```bash
vgextend vg_data /dev/sdc1
```

Verify:

```bash
pvs
vgs
```

Extend the LV:

```bash
lvextend -r -L +500G /dev/vg_data/lv_app
```

Verify:

```bash
lvs -a -o +devices
df -hT /app
```

---

### Move Data Between LVM PVs

Show allocation:

```bash
pvs -o pv_name,pv_size,pv_free,vg_name
lvs -a -o +devices
```

Move allocated extents away from one PV:

```bash
pvmove /dev/sdb1
```

Move to a specific destination PV:

```bash
pvmove /dev/sdb1 /dev/sdc1
```

Monitor:

```bash
pvmove --poll y
```

After all extents are moved:

```bash
vgreduce vg_data /dev/sdb1
```

Remove the PV label if the disk is being retired:

```bash
pvremove /dev/sdb1
```

Verify before `vgreduce`:

```bash
pvs
lvs -a -o +devices
```

`pvmove` can often migrate active LVs online, but performance and redundancy impact must be assessed.

---

### LVM Metadata Backups

Back up all VG metadata:

```bash
vgcfgbackup
```

Back up one VG:

```bash
vgcfgbackup vg_data
```

Common archive locations:

```text
/etc/lvm/backup/
/etc/lvm/archive/
```

List:

```bash
ls -l /etc/lvm/backup /etc/lvm/archive
```

Restore metadata only under a controlled recovery plan:

```bash
vgcfgrestore -l vg_data
```

Show available versions:

```bash
vgcfgrestore -l vg_data
```

Restore a selected version:

```bash
vgcfgrestore -f /etc/lvm/archive/FILE.vg vg_data
```

LVM metadata backups do not contain filesystem data.

---

### LVM Snapshots

Create a classic snapshot:

```bash
lvcreate -L 10G -s -n lv_app_snap /dev/vg_data/lv_app
```

Show snapshot use:

```bash
lvs -a -o lv_name,origin,lv_size,data_percent,devices
```

Mount read-only:

```bash
mkdir -p /mnt/lv_app_snap
mount -o ro /dev/vg_data/lv_app_snap /mnt/lv_app_snap
```

Remove after use:

```bash
umount /mnt/lv_app_snap
lvremove /dev/vg_data/lv_app_snap
```

A snapshot stores changed blocks, not a full independent copy.

If the snapshot reaches 100% usage, it becomes invalid.

Snapshots can reduce write performance.

Application-consistent backups may require:

- Database flush or snapshot command
- Filesystem freeze
- Service pause
- Transaction coordination

Filesystem freeze example:

```bash
fsfreeze -f /mountpoint
```

Unfreeze:

```bash
fsfreeze -u /mountpoint
```

> **Warning:** Never leave a production filesystem frozen.

---

### Thin Provisioning

Create a thin pool:

```bash
lvcreate -L 500G -T vg_data/thin_pool
```

Create a thin LV with 1 TiB virtual size:

```bash
lvcreate -V 1T -T vg_data/thin_pool -n thin_app
```

Inspect:

```bash
lvs -a -o lv_name,lv_size,segtype,data_percent,metadata_percent
```

Important fields:

- `Data%`
- `Meta%`

Thin virtual size can exceed physical pool size.

This is overprovisioning, not free storage.

Monitor continuously:

```bash
watch -n 5 "lvs -a -o lv_name,lv_size,data_percent,metadata_percent"
```

Extend the pool:

```bash
lvextend -L +100G vg_data/thin_pool
```

Extend pool metadata when required:

```bash
lvextend --poolmetadatasize +1G vg_data/thin_pool
```

A full thin pool can cause I/O failures, filesystem errors, and service outages.

Configure monitoring and automatic extension before production use.

---

### Software RAID with `mdadm`

Show RAID status:

```bash
cat /proc/mdstat
```

Detailed array information:

```bash
mdadm --detail /dev/md0
```

Examine a member:

```bash
mdadm --examine /dev/sdb1
```

Create a RAID1 array from two confirmed empty members:

```bash
mdadm --create /dev/md0 \
  --level=1 \
  --raid-devices=2 \
  /dev/sdb1 /dev/sdc1
```

Monitor synchronization:

```bash
watch -n 2 cat /proc/mdstat
```

Create a filesystem:

```bash
mkfs.xfs /dev/md0
```

Save array assembly configuration:

```bash
mdadm --detail --scan
```

On RHEL-family systems, review the appropriate `mdadm.conf` location before writing persistent configuration.

Update initramfs when the root or boot process depends on the array:

```bash
dracut -f
```

---

### Replace a Failed RAID1 Member

Confirm the failure:

```bash
cat /proc/mdstat
mdadm --detail /dev/md0
```

Mark a device failed when required:

```bash
mdadm /dev/md0 --fail /dev/sdb1
```

Remove it:

```bash
mdadm /dev/md0 --remove /dev/sdb1
```

Partition the replacement to match the healthy member.

Compare:

```bash
sfdisk --dump /dev/sdc
```

Apply a reviewed layout to the replacement:

```bash
sfdisk /dev/sdb < /root/replacement.partition-table
```

Add the new member:

```bash
mdadm /dev/md0 --add /dev/sdb1
```

Monitor rebuild:

```bash
watch -n 2 cat /proc/mdstat
```

Verify:

```bash
mdadm --detail /dev/md0
```

> **Warning:** Do not remove the wrong healthy member.

RAID protects availability against specific disk failures. It is not a backup.

---

### Stratis

Show Stratis pools:

```bash
stratis pool list
```

Show block devices:

```bash
stratis blockdev list
```

Show Stratis filesystems:

```bash
stratis filesystem list
```

Create a pool:

```bash
stratis pool create pool_data /dev/sdb
```

Create a filesystem:

```bash
stratis filesystem create pool_data fs_app
```

Show its device path:

```bash
stratis filesystem list
```

Mount using its UUID or stable path according to the installed Stratis version.

Add a block device:

```bash
stratis pool add-data pool_data /dev/sdc
```

Create a snapshot:

```bash
stratis filesystem snapshot pool_data fs_app fs_app_snapshot
```

Monitor pool use:

```bash
stratis pool list
stratis blockdev list
```

Stratis behavior and CLI details depend on the installed version. Confirm with:

```bash
stratis --help
stratis pool --help
stratis filesystem --help
```

---

### LVM VDO

VDO provides thin provisioning, compression, and deduplication.

On modern RHEL-family systems, VDO is commonly managed through LVM.

Create a VDO LV using confirmed empty VG space:

```bash
lvcreate \
  --type vdo \
  --name vdo_lv \
  --size 100G \
  --virtualsize 1T \
  vg_data
```

Create a filesystem:

```bash
mkfs.xfs /dev/vg_data/vdo_lv
```

Inspect:

```bash
lvs -a -o lv_name,lv_size,data_percent,metadata_percent,segtype
```

Show detailed VDO statistics where available:

```bash
lvs -a -o +vdo_compression,vdo_deduplication
```

VDO virtual size is not physical capacity.

Monitor physical use and data characteristics.

Compression and deduplication ratios vary by workload.

Encrypted or already compressed data may receive little benefit.

VDO command details vary by distribution release. Confirm the installed LVM documentation before creation.

---

### Device Health and SMART

Show SMART summary:

```bash
smartctl -H /dev/sdX
```

Show all data:

```bash
smartctl -a /dev/sdX
```

Start a short self-test:

```bash
smartctl -t short /dev/sdX
```

View results later:

```bash
smartctl -l selftest /dev/sdX
```

NVMe:

```bash
nvme smart-log /dev/nvme0
```

Show NVMe devices:

```bash
nvme list
```

Kernel errors:

```bash
journalctl -k -g 'I/O error|medium error|reset|timeout|nvme|ata'
```

SMART passing does not prove a device or path is healthy.

Correlate:

- Error counters
- Kernel messages
- Storage-array alerts
- Latency
- Filesystem errors
- Application symptoms

---

### Storage Performance

Show device performance:

```bash
iostat -xz 1
```

Show process I/O:

```bash
pidstat -d 1
```

Interactive I/O use:

```bash
iotop -oPa
```

Show block-device statistics:

```bash
cat /proc/diskstats
```

Show scheduler:

```bash
cat /sys/block/DEVICE/queue/scheduler
```

Show read-ahead:

```bash
blockdev --getra /dev/DEVICE
```

Show sector size:

```bash
blockdev --getss /dev/DEVICE
blockdev --getpbsz /dev/DEVICE
```

Useful `iostat` fields commonly include:

| Field | Meaning |
|---|---|
| `r/s`, `w/s` | Operations per second |
| `rkB/s`, `wkB/s` | Throughput |
| `await` | Average completion latency |
| `aqu-sz` | Queue depth |
| `%util` | Time the device was busy |

Interpret values relative to:

- HDD, SSD, NVMe, SAN, or cloud disk
- RAID level
- Queue depth
- Workload type
- Service latency objective

---

### Busy Mount Troubleshooting

Attempt unmount:

```bash
umount /data
```

If busy:

```bash
fuser -vm /data
```

Open files:

```bash
lsof +f -- /data
```

Processes with current working directories under it:

```bash
lsof +D /data
```

`lsof +D` can be expensive on large trees.

Check nested mounts:

```bash
findmnt -R /data
```

Check shell working directory:

```bash
pwd
```

Move out:

```bash
cd /
```

Stop or redirect the identified process safely, then retry:

```bash
umount /data
```

Do not use lazy unmount merely to avoid identifying the active user.

---

### Read-Only Filesystem Investigation

Confirm options:

```bash
findmnt -T /affected/path
```

Search kernel errors:

```bash
journalctl -k -g 'read-only|I/O error|XFS|EXT4|Buffer I/O'
```

Identify backing devices:

```bash
lsblk -f
findmnt -no SOURCE,FSTYPE,TARGET /affected/path
```

Check LVM and RAID:

```bash
lvs -a -o +devices
cat /proc/mdstat
```

Check latency and errors:

```bash
iostat -xz 1
smartctl -a /dev/DEVICE
```

Do not immediately remount read-write.

The kernel may have changed the filesystem to read-only to limit further corruption.

Protect data, fix the underlying storage issue, then perform an offline filesystem check when required.

---

### Remote Storage and NFS Triage

Show NFS mounts:

```bash
findmnt -t nfs,nfs4
```

Show mount details:

```bash
nfsstat -m
```

Check server exports:

```bash
showmount -e NFS_SERVER
```

Test RPC services where appropriate:

```bash
rpcinfo -p NFS_SERVER
```

Check port reachability:

```bash
nc -vz NFS_SERVER 2049
```

Route:

```bash
ip route get NFS_SERVER_IP
```

Capture:

```bash
tcpdump -ni any host NFS_SERVER_IP and port 2049
```

Find blocked tasks:

```bash
ps -eo state,pid,ppid,wchan:32,comm,args | awk '$1 ~ /^D/'
```

A hung NFS mount can cause:

- High load average
- Low CPU usage
- Processes in `D` state
- Commands such as `df`, `du`, or `ls` hanging
- Service shutdown delays

Do not use unsafe mount options merely to hide server outages. Design timeouts and availability according to application requirements.

---

### Zero-Downtime Expansion Checklist

Before:

```bash
findmnt -T /mountpoint
df -hT /mountpoint
lsblk -f
pvs
vgs
lvs -a -o +devices
```

Confirm:

- Filesystem supports online growth
- Underlying storage is healthy
- Backup exists
- Correct LV and mount point are identified
- VG has free extents or the disk can be enlarged
- Monitoring is active

Typical LVM growth:

```bash
lvextend -r -L +20G /dev/vg_name/lv_name
```

After:

```bash
lvs /dev/vg_name/lv_name
df -hT /mountpoint
journalctl -k --since "10 minutes ago"
```

Application verification:

```bash
systemctl status application.service
```

Test a normal read and write through the application.

Do not treat successful `lvextend` output as complete verification. Confirm the filesystem size and application function.

---

### Storage Metadata and Configuration Backup

Recommended files and reports:

```bash
sfdisk --dump /dev/DEVICE > partition-table.txt
vgcfgbackup
pvs -a -o +pv_uuid > pvs.txt
vgs -a -o +vg_uuid > vgs.txt
lvs -a -o +devices > lvs.txt
blkid > blkid.txt
lsblk -f > lsblk.txt
findmnt --real > findmnt.txt
cat /etc/fstab > fstab.txt
cat /proc/mdstat > mdstat.txt
mdadm --detail --scan > mdadm-scan.txt
```

Store copies outside the affected host.

Metadata reports help reconstruct the stack, but they are not backups of application data.

---

### Storage Command Index

```bash
lsblk -f
blkid
findmnt
findmnt -T /path
mountpoint /path
fdisk -l
parted /dev/DEVICE print
partprobe /dev/DEVICE
udevadm settle
sfdisk --dump /dev/DEVICE
wipefs /dev/DEVICE
mkfs.xfs /dev/DEVICE
mkfs.ext4 /dev/DEVICE
mount /dev/DEVICE /mountpoint
umount /mountpoint
findmnt --verify --verbose
mount -av
df -hT
df -i
du -xhd1 /path
lsof +L1
xfs_info /mountpoint
xfs_growfs /mountpoint
xfs_repair -n /dev/DEVICE
tune2fs -l /dev/DEVICE
e2fsck -n /dev/DEVICE
resize2fs /dev/DEVICE
swapon --show
mkswap /dev/DEVICE
swapon /dev/DEVICE
swapoff /dev/DEVICE
pvs
vgs
lvs -a -o +devices
pvcreate /dev/DEVICE
vgcreate vg_name /dev/DEVICE
lvcreate -L SIZE -n lv_name vg_name
lvextend -r -L +SIZE /dev/vg_name/lv_name
pvresize /dev/DEVICE
vgextend vg_name /dev/DEVICE
pvmove /dev/SOURCE_PV
vgcfgbackup
cat /proc/mdstat
mdadm --detail /dev/md0
stratis pool list
stratis filesystem list
smartctl -a /dev/DEVICE
nvme smart-log /dev/nvme0
iostat -xz 1
pidstat -d 1
iotop -oPa
```
---

<a id="chapter-5-realistic-troubleshooting-scenarios"></a>
# Chapter 5: Realistic Troubleshooting Scenarios

The scenarios below use a consistent operational pattern: **Symptom or Problem**, **Diagnosis**, **Likely Causes**, **Resolution**, and **Verification**, where applicable.

> **Tip:** Reproduce the problem once, record the exact time, and correlate the failure with logs before changing the system.

<a id="scenario-1-a-systemd-service-will-not-start"></a>
## Scenario 1: A systemd Service Will Not Start

### Symptom

```bash
systemctl start myapp
```

returns a failure.

### Diagnosis

#### Read the detailed status

```bash
systemctl status myapp --no-pager -l
```

Look for:

- Exit code
- Missing file
- Permission denied
- Invalid option
- Dependency failure
- Repeated restart limit

#### Read the service journal

```bash
journalctl -u myapp -b -n 200 --no-pager
```

#### Inspect the exact unit and overrides

```bash
systemctl cat myapp
```

#### Inspect execution properties

```bash
systemctl show myapp \
  -p User \
  -p Group \
  -p ExecStart \
  -p WorkingDirectory \
  -p Environment \
  -p EnvironmentFiles \
  -p Result \
  -p ExecMainStatus
```

#### Verify referenced files

```bash
namei -l /path/from/ExecStart
```

```bash
ls -lZ /path/from/ExecStart
```

#### Test the application's configuration

Examples:

```bash
nginx -t
```

```bash
sshd -t
```

```bash
httpd -t
```

Use the validation command appropriate to the application.

#### Run the command manually as the service user

```bash
sudo -u service_user /path/to/program --arguments
```

This can reveal environment, permission, and working-directory problems.

#### Check port conflicts

```bash
ss -lntup | grep ':PORT'
```

#### Check SELinux denials

```bash
ausearch -m AVC,USER_AVC -ts recent
```

### Likely Causes

- Invalid configuration
- Missing environment file
- Wrong ownership or permissions
- Port already in use
- SELinux denial
- Missing package or library
- Wrong executable path
- Dependency unit failed

### Verification

```bash
systemctl restart myapp
systemctl is-active myapp
systemctl status myapp --no-pager
journalctl -u myapp --since "5 minutes ago"
```

Then test the actual application, not just the unit state.

---

<a id="scenario-2-the-service-is-running-but-the-port-is-unreachable"></a>
## Scenario 2: The Service Is Running but the Port Is Unreachable

### Symptom

```bash
systemctl status myapp
```

shows `active (running)`, but remote clients cannot connect.

### Diagnosis

#### Confirm the process is listening

```bash
ss -lntp | grep ':PORT'
```

Interpret the bind address:

- `127.0.0.1:PORT`: Localhost only
- `0.0.0.0:PORT`: All IPv4 interfaces
- `[::]:PORT`: All IPv6 interfaces and sometimes IPv4, depending on configuration

#### Test locally

```bash
nc -vz 127.0.0.1 PORT
```

Or:

```bash
curl -v http://127.0.0.1:PORT/
```

#### Test the server's real IP locally

```bash
nc -vz SERVER_IP PORT
```

#### Check interface addresses

```bash
ip -br address
```

#### Check firewall rules

```bash
firewall-cmd --get-active-zones
firewall-cmd --list-all
nft list ruleset
```

#### Capture packets while a remote client connects

```bash
tcpdump -ni any tcp port PORT
```

Interpretation:

- No SYN packet arrives: upstream routing, firewall, security group, or client problem.
- SYN arrives but no SYN-ACK leaves: local firewall or no listener on that address.
- SYN and SYN-ACK occur but connection still fails: return-path or client-side problem.
- Full handshake succeeds: inspect application protocol and logs.

#### Check application logs

```bash
journalctl -u myapp -f
```

### Likely Causes

- Service bound only to localhost
- Local firewall blocks the port
- Wrong server IP
- Upstream firewall or cloud security rule
- Asymmetric routing
- Application accepts TCP but rejects requests

---

<a id="scenario-3-high-load-average-but-cpu-is-not-busy"></a>
## Scenario 3: High Load Average but CPU Is Not Busy

### Symptom

`uptime` shows high load, but `top` shows a large idle percentage.

### Key Concept

Load average includes runnable tasks and tasks in uninterruptible sleep. High load with idle CPU often points to blocked I/O.

### Diagnosis

#### Confirm load and CPU

```bash
uptime
mpstat -P ALL 1
```

#### Inspect blocked tasks

```bash
vmstat 1
```

Watch:

- High `b`
- High `wa`
- Low CPU usage

#### Find processes in `D` state

```bash
ps -eo state,pid,ppid,wchan:32,comm,args | awk '$1 ~ /^D/'
```

#### Inspect storage latency

```bash
iostat -xz 1
```

#### Inspect per-process I/O

```bash
pidstat -d 1
```

#### Search kernel logs

```bash
journalctl -k -g 'I/O error|timeout|reset|blocked for more than'
```

#### Check network filesystems

```bash
findmnt -t nfs,nfs4,cifs
```

```bash
nfsstat -m
```

if NFS tools are installed.

### Likely Causes

- Slow or failing disk
- Storage-array latency
- Hung NFS mount
- Filesystem congestion
- Device reset or path failure

### Warning

A process in `D` state often cannot be killed until the kernel operation completes. Rebooting may clear the symptom but destroys evidence and does not fix the storage or network cause.

---

<a id="scenario-4-one-process-uses-100-cpu"></a>
## Scenario 4: One Process Uses 100% CPU

### Symptom

One process dominates a CPU core.

### Diagnosis

#### Identify the process

```bash
top
```

or:

```bash
ps -eo pid,ppid,user,%cpu,%mem,etime,comm,args \
  --sort=-%cpu | head
```

#### Determine whether one thread is responsible

```bash
top -H -p PID
```

or:

```bash
pidstat -t -p PID 1
```

#### Inspect the process tree

```bash
pstree -ap PID
```

#### Trace system calls briefly

```bash
timeout 10 strace -f -tt -T -p PID
```

Patterns:

- Repeated failed file opens: missing path or permission problem
- Repeated network retries: unreachable dependency
- Futex loops: thread contention
- No system calls while CPU remains high: user-space computation loop

#### Profile hot functions

```bash
perf top -p PID
```

or:

```bash
perf record -F 99 -p PID -g -- sleep 30
perf report
```

#### Check recent application changes

```bash
dnf history
```

```bash
systemctl cat service_name
```

### Temporary Containment

Lower scheduling priority:

```bash
renice +10 -p PID
```

Limit a systemd service where supported:

```bash
systemctl set-property --runtime service_name CPUQuota=50%
```

Containment is not the root-cause fix.

---

<a id="scenario-5-the-server-is-running-out-of-memory"></a>
## Scenario 5: The Server Is Running Out of Memory

### Symptom

Applications become slow, processes are killed, or the kernel reports OOM events.

### Diagnosis

#### Check memory and swap

```bash
free -h
swapon --show
```

#### Check active paging

```bash
vmstat 1
```

Watch sustained `si` and `so`.

#### Find large processes

```bash
ps -eo pid,ppid,user,%mem,rss,vsz,etime,comm,args \
  --sort=-rss | head -30
```

#### Examine one process

```bash
pmap -x PID | tail -20
```

```bash
grep -E 'VmPeak|VmSize|VmRSS|VmData|VmSwap|Threads' /proc/PID/status
```

#### Search for OOM-killer evidence

```bash
journalctl -k -g 'oom|Out of memory|Killed process'
```

#### Check service memory limits

```bash
systemctl show service_name \
  -p MemoryCurrent \
  -p MemoryPeak \
  -p MemoryMax \
  -p MemoryHigh
```

#### Distinguish cache from real pressure

```bash
grep -E 'MemAvailable|Cached|Buffers|SReclaimable|SwapFree' /proc/meminfo
```

### Likely Causes

- Memory leak
- Workload spike
- Too many worker processes
- Oversized cache
- Container or cgroup limit
- Insufficient swap for workload behavior
- Kernel slab growth

### Verification

```bash
free -h
vmstat 1 10
journalctl -k --since "10 minutes ago"
```

---

<a id="scenario-6-df-says-the-filesystem-is-full-but-du-does-not"></a>
## Scenario 6: `df` Says the Filesystem Is Full but `du` Does Not

### Symptom

```bash
df -h /var
```

shows nearly 100%, but:

```bash
du -xsh /var
```

shows much less usage.

### Diagnosis

#### Confirm both refer to the same filesystem

```bash
findmnt -T /var
```

#### Find deleted files still held open

```bash
lsof +L1 /var
```

Example interpretation:

```text
process  PID user  FD  ...  NAME
java     2241 app   7w ...  /var/log/app.log (deleted)
```

The pathname was removed, but the process still owns the inode through FD `7`.

#### Confirm the process

```bash
ps -fp 2241
```

#### Safest resolution

Ask the application to reopen logs, or restart only the affected service:

```bash
systemctl reload service_name
```

or:

```bash
systemctl restart service_name
```

#### Verify space is released

```bash
df -h /var
```

### Other Possible Causes

- Data hidden beneath a mounted filesystem
- Reserved filesystem blocks
- Snapshot usage
- Different mount namespace
- `du` lacks permission to read directories

Check for hidden data by inspecting the underlying mount only during a controlled maintenance procedure.

---

<a id="scenario-7-no-space-left-on-device-but-disk-space-is-available"></a>
## Scenario 7: “No Space Left on Device” but Disk Space Is Available

### Symptom

An application receives:

```text
No space left on device
```

but `df -h` shows free space.

### Diagnosis

#### Check inodes

```bash
df -i
```

#### Find directories containing huge numbers of files

A quick directory count:

```bash
find /var -xdev -type f -printf '%h\n' 2>/dev/null \
  | sort | uniq -c | sort -n | tail -30
```

Count files under one directory:

```bash
find /path -xdev -type f | wc -l
```

#### Find likely small-file producers

```bash
find /var -xdev -type f -size -4k \
  -printf '%h\n' 2>/dev/null | sort | uniq -c | sort -n | tail
```

### Likely Causes

- Mail queue explosion
- Session files
- Application cache
- Temporary files
- Millions of tiny log files
- Misconfigured job generating one file per event

### Resolution

Remove or archive files according to application policy, then fix the producer. Do not delete unknown files only to free inodes.

---

<a id="scenario-8-disk-i-o-is-slow"></a>
## Scenario 8: Disk I/O Is Slow

### Symptom

Applications respond slowly and processes spend time waiting for storage.

### Diagnosis

#### Check system-level I/O wait

```bash
vmstat 1
```

```bash
mpstat 1
```

#### Inspect device latency and queue depth

```bash
iostat -xz 1
```

#### Find processes performing I/O

```bash
pidstat -d 1
```

or, if installed:

```bash
iotop -oPa
```

#### Search for hardware or path errors

```bash
journalctl -k -g 'I/O error|timeout|reset|medium error|blk_update_request'
```

#### Check filesystem fullness

```bash
df -hT
df -i
```

#### Check whether swapping contributes

```bash
vmstat 1
```

High `si` and `so` means memory pressure is causing storage activity.

### Interpretation Examples

- High latency on one device: device or workload bottleneck
- High queue depth with high latency: overloaded path
- High I/O wait with NFS-mounted workload: network storage issue
- High write rate from one PID: application logging or batch job
- Disk errors in journal: hardware, cable, controller, or storage path issue

---

<a id="scenario-9-a-filesystem-became-read-only"></a>
## Scenario 9: A Filesystem Became Read-Only

### Symptom

Writes fail with:

```text
Read-only file system
```

### Diagnosis

#### Confirm mount options

```bash
findmnt -T /affected/path
```

#### Search kernel messages

```bash
journalctl -k -g 'read-only|I/O error|filesystem error|XFS|EXT4'
```

#### Identify the backing device

```bash
findmnt -no SOURCE,FSTYPE,TARGET /affected/path
```

#### Check device and path health

```bash
lsblk -f
```

```bash
iostat -xz 1
```

#### Stop writes and protect data

> **Warning:** Do not blindly remount read-write before understanding why the kernel remounted it read-only.

#### Plan offline repair

For XFS:

```bash
xfs_repair -n /dev/DEVICE
```

For ext filesystems:

```bash
e2fsck -n /dev/DEVICE
```

Actual repairs generally require unmounting, rescue mode, or booting from alternate media.

### Likely Causes

- Filesystem corruption
- Storage I/O error
- Device path loss
- Administrative read-only mount
- Snapshot or recovery workflow

---

<a id="scenario-10-dns-resolution-fails"></a>
## Scenario 10: DNS Resolution Fails

### Symptom

Connections by IP work, but names fail.

### Diagnosis

#### Compare IP and name tests

```bash
ping -c 2 IP_ADDRESS
```

```bash
getent hosts example.com
```

#### Inspect resolver configuration

```bash
cat /etc/resolv.conf
```

```bash
grep '^hosts:' /etc/nsswitch.conf
```

#### Query the configured server directly

```bash
dig example.com
```

#### Query a specific DNS server

```bash
dig @DNS_SERVER example.com
```

#### Capture DNS traffic

```bash
tcpdump -ni any port 53
```

Interpretation:

- Query leaves, no reply: server or network path problem
- Reply is `SERVFAIL`: upstream DNS or DNSSEC problem
- Reply is `NXDOMAIN`: name does not exist from that resolver's perspective
- No query leaves: NSS, application, or resolver-library issue

#### Check NetworkManager DNS data

```bash
nmcli device show | grep -i DNS
```

#### Check local resolved state if used

```bash
resolvectl status
```

### Likely Causes

- Wrong DNS server
- Unreachable resolver
- Bad search domain
- Incorrect **`/etc/nsswitch.conf`**
- Split-DNS or VPN configuration
- Firewall blocks UDP or TCP 53
- Stale local cache

---

<a id="scenario-11-ssh-troubleshooting-by-failure-type"></a>
## Scenario 11: SSH Troubleshooting by Failure Type

### Failure Type 1: Connection Refused

Usually means the host actively rejected the TCP connection.

Check:

```bash
systemctl status sshd
ss -lntp | grep ':22'
journalctl -u sshd -b
```

Potential causes:

- `sshd` is stopped
- Listening on another port
- Listening only on another address
- Local rejection rule

### Failure Type 2: Connection Timeout

Usually means packets are being dropped or the route is broken.

Check from the client:

```bash
ip route get SERVER_IP
nc -vz SERVER_IP 22
tracepath SERVER_IP
```

On the server:

```bash
tcpdump -ni any tcp port 22
firewall-cmd --list-all
nft list ruleset
```

### Failure Type 3: Authentication Failure

Use verbose client output:

```bash
ssh -vvv user@server
```

On the server:

```bash
journalctl -u sshd -f
```

Check account state:

```bash
id username
passwd -S username
chage -l username
```

Check home and key permissions:

```bash
namei -l /home/username/.ssh/authorized_keys
```

Typical secure values:

```bash
chmod 700 /home/username/.ssh
chmod 600 /home/username/.ssh/authorized_keys
chown -R username:username /home/username/.ssh
```

Check SELinux contexts:

```bash
ls -ldZ /home/username /home/username/.ssh
ls -lZ /home/username/.ssh/authorized_keys
restorecon -Rv /home/username/.ssh
```

Validate SSH configuration:

```bash
sshd -t
```

Show effective configuration:

```bash
sshd -T
```

---

<a id="scenario-12-selinux-blocks-an-application"></a>
## Scenario 12: SELinux Blocks an Application

### Symptom

Permissions look correct, but access is still denied.

### Diagnosis

#### Confirm enforcing mode

```bash
getenforce
```

#### Reproduce the failure once

This creates fresh audit evidence.

#### Search AVC records

```bash
ausearch -m AVC,USER_AVC -ts recent
```

#### Inspect process and file contexts

```bash
ps -eZ | grep process_name
```

```bash
ls -lZ /path/to/resource
```

#### Compare with expected context

```bash
semanage fcontext -l | grep '/path'
```

#### Restore expected labels

```bash
restorecon -Rv /path
```

#### Check relevant booleans

```bash
getsebool -a | grep keyword
```

### Recommended Fix Order

1. Fix incorrect file labels.
2. Use an existing SELinux boolean if it represents the intended behavior.
3. Move content to a standard labeled location if appropriate.
4. Write a narrow local policy only when the access is legitimate and no existing policy mechanism fits.

Do not permanently disable SELinux to hide the denial.

---

<a id="scenario-13-dnf-cannot-reach-a-repository"></a>
## Scenario 13: DNF Cannot Reach a Repository

### Symptom

DNF reports metadata download, DNS, TLS, or mirror errors.

### Diagnosis

#### Confirm time

```bash
timedatectl
chronyc tracking
```

#### Confirm DNS

```bash
getent hosts repository.example.com
```

#### Confirm routing

```bash
ip route get REPOSITORY_IP
```

#### Test HTTPS

```bash
curl -Iv https://repository.example.com/
```

#### Inspect proxy settings

```bash
env | grep -i proxy
```

```bash
grep -Rni proxy /etc/dnf /etc/yum.conf /etc/yum.repos.d/
```

#### Inspect repository definitions

```bash
dnf repolist -v
```

#### Rebuild metadata

```bash
dnf clean all
dnf makecache
```

#### Test one repository only

```bash
dnf --disablerepo='*' --enablerepo='REPO_ID' makecache
```

### Likely Causes

- DNS failure
- Incorrect date/time
- Proxy problem
- Expired or wrong TLS certificate
- Disabled or invalid repository
- Wrong GPG key
- Firewall blocks HTTPS
- Subscription or entitlement issue

---

<a id="scenario-14-the-host-boots-into-emergency-mode"></a>
## Scenario 14: The Host Boots into Emergency Mode

### Symptom

The server enters emergency mode instead of the normal target.

### Diagnosis

#### Read the on-screen failure and journal

```bash
journalctl -xb
```

#### Show failed units

```bash
systemctl --failed
```

#### Focus on mount failures

```bash
systemctl --failed --type=mount
```

#### Inspect **`/etc/fstab`**

```bash
cat /etc/fstab
```

#### Compare identifiers

```bash
lsblk -f
blkid
```

#### Test mounts

```bash
mount -av
```

#### Inspect the failed mount unit

```bash
systemctl status path-to-mount.mount
```

#### Search current boot logs

```bash
journalctl -b -g 'mount|dependency|timed out|failed'
```

### Likely Causes

- Wrong UUID in **`/etc/fstab`**
- Missing disk
- Network mount unavailable
- Filesystem corruption
- Invalid mount option
- Encrypted volume not unlocked
- LVM volume inactive

### Resolution

Back up the affected configuration before editing:

```bash
cp -a /etc/fstab /etc/fstab.before-fix
```

After correction:

```bash
mount -av
systemctl daemon-reload
systemctl default
```

---

<a id="scenario-15-an-lvm-filesystem-is-full"></a>
## Scenario 15: An LVM Filesystem Is Full

### Symptom

A filesystem on an LVM logical volume reaches capacity.

### Diagnosis

#### Identify the filesystem and LV

```bash
df -hT /mountpoint
findmnt -T /mountpoint
lsblk -f
```

#### Check volume-group free space

```bash
vgs -o vg_name,vg_size,vg_free
```

#### Inspect logical volumes

```bash
lvs -a -o lv_name,vg_name,lv_size,segtype,data_percent,metadata_percent,devices
```

#### Determine whether files can be safely removed first

```bash
du -xhd1 /mountpoint | sort -h
lsof +L1 /mountpoint
```

#### Extend when free extents exist

```bash
lvextend -r -L +10G /dev/VG_NAME/LV_NAME
```

or:

```bash
lvextend -r -l +100%FREE /dev/VG_NAME/LV_NAME
```

#### Verify

```bash
lvs
df -hT /mountpoint
```

### When the Volume Group Has No Free Space

Options may include:

- Add a new physical volume
- Extend the underlying virtual disk
- Move or archive data
- Reduce another volume only when the filesystem supports safe shrinking and a maintenance procedure exists

Do not assume XFS can be shrunk; normal XFS administration supports growing but not shrinking.

---

<a id="scenario-16-the-server-has-an-ip-address-but-cannot-reach-the-network"></a>
## Scenario 16: The Server Has an IP Address but Cannot Reach the Network

### Symptom

The interface is up and addressed, but external connectivity fails.

### Diagnosis

#### Inspect interface state

```bash
ip -br address
ip -s link
```

#### Inspect routes

```bash
ip route
```

#### Ask for the route to the destination

```bash
ip route get DESTINATION_IP
```

#### Test the local gateway

```bash
ping -c 3 GATEWAY_IP
```

#### Inspect neighbor resolution

```bash
ip neigh
```

Problem states may include:

- `FAILED`
- `INCOMPLETE`

#### Capture ARP and ICMP

```bash
tcpdump -ni INTERFACE 'arp or icmp'
```

#### Inspect policy routing

```bash
ip rule
ip route show table all
```

#### Inspect NetworkManager

```bash
nmcli device status
nmcli connection show --active
nmcli device show INTERFACE
```

### Likely Causes

- Missing default route
- Wrong subnet mask
- Wrong gateway
- Duplicate IP
- VLAN mismatch
- Link errors
- Policy-routing rule
- Upstream switch or router issue

---

<a id="scenario-17-a-process-is-a-zombie"></a>
## Scenario 17: A Process Is a Zombie

### Symptom

`ps` shows process state `Z`, sometimes displayed as `<defunct>`.

### Cause

A zombie process has already finished executing. The kernel keeps a small process-table entry containing information such as:

- PID
- Parent PID
- Exit status
- Basic accounting information

The executable code is no longer running, so the zombie does not consume normal CPU time and no longer owns its former user-space memory. Its process-table entry remains because the parent has not yet collected the child's termination status.

The parent must call one of the wait-family system calls, such as:

```c
wait()
waitpid()
waitid()
```

After the parent successfully reaps the child, the kernel removes the zombie entry.

### Diagnosis

#### Find zombie processes

```bash
ps -eo stat,pid,ppid,user,etime,comm,args | awk '$1 ~ /^Z/'
```

Alternative:

```bash
ps aux | awk '$8 ~ /^Z/'
```

#### Inspect one zombie and identify its parent

```bash
ps -o pid,ppid,stat,etime,comm,args -p ZOMBIE_PID
```

Then inspect the parent:

```bash
ps -fp PARENT_PID
```

Show the process hierarchy:

```bash
pstree -aps ZOMBIE_PID
```

#### Count zombies

```bash
ps -eo stat= | awk '$1 ~ /^Z/ {count++} END {print count+0}'
```

A single short-lived zombie can appear briefly during normal process handling. A growing or persistent population indicates that a parent process is failing to reap children.

#### Check whether the parent is a managed service

```bash
systemctl status parent_service
```

```bash
journalctl -u parent_service -b
```

For an application bug, inspect how it creates and handles child processes. The durable fix is for the parent to call `wait()`, `waitpid()`, or an equivalent library function and correctly handle `SIGCHLD`.

### Why `SIGKILL` Does Not Remove a Zombie

This does not help:

```bash
kill -9 ZOMBIE_PID
```

`SIGKILL` cannot make a difference because the child has already exited. There is no running process code left to kill. Only reaping the stored exit status removes the zombie entry.

### Resolution

#### Preferred fix: make the parent reap its children

Correct the parent application's child-handling logic so that it calls a wait-family function. This is the real fix when source code or application configuration can be changed.

#### Operational fix: gracefully restart the faulty parent

When the parent is a service and restart impact is understood:

```bash
systemctl restart parent_service
```

A graceful restart is preferable to killing it abruptly because the service can close files, release locks, and stop child processes cleanly.

#### Last-resort parent termination

If the parent is genuinely stuck or defective and cannot be restarted normally, terminating the parent causes its remaining children to be reparented. On modern Linux, they may be adopted by PID 1 or by a configured child subreaper. The adopter should call a wait-family function and reap exited children.

Try normal termination first:

```bash
kill -TERM PARENT_PID
```

Verify:

```bash
ps -p PARENT_PID
```

Use `SIGKILL` on the **parent**, not the zombie, only as a last resort when the consequences are understood:

```bash
kill -KILL PARENT_PID
```

Killing the parent may interrupt service, lose unflushed application data, or affect non-zombie children. Do not use it blindly.

### Verification

```bash
ps -p ZOMBIE_PID -o pid,ppid,stat,comm
```

No output normally means the process-table entry is gone.

Recount zombies:

```bash
ps -eo stat= | awk '$1 ~ /^Z/ {count++} END {print count+0}'
```

### Root-Cause Summary

| Observation | Meaning |
|---|---|
| Zombie has a PID | Its minimal process-table record still exists. |
| Zombie shows state `Z` | The child exited but has not been reaped. |
| `kill -9 ZOMBIE_PID` has no effect | The child is already dead. |
| Parent calls `wait()` or `waitpid()` | The zombie is reaped correctly. |
| Parent exits | The child is reparented to a subreaper or PID 1, which should reap it. |
| Zombies keep accumulating | The parent application likely has defective child-process handling. |

---

<a id="scenario-18-a-process-cannot-open-a-file"></a>
## Scenario 18: A Process Cannot Open a File

### Symptom

The application reports `Permission denied` or `No such file or directory`.

### Diagnosis

#### Trace file operations

```bash
strace -f -e trace=file -o /tmp/file-trace.txt command arguments
```

For a running process:

```bash
strace -f -e trace=file -p PID
```

#### Inspect every directory component

```bash
namei -l /path/to/file
```

#### Inspect permissions and ACLs

```bash
stat /path/to/file
getfacl /path/to/file
```

#### Test as the application user

```bash
sudo -u appuser test -r /path/to/file && echo readable
```

#### Inspect SELinux

```bash
ls -lZ /path/to/file
ausearch -m AVC,USER_AVC -ts recent
```

#### Check mount state

```bash
findmnt -T /path/to/file
```

Potential causes:

- Missing execute permission on a parent directory
- ACL denial
- Wrong user or group
- SELinux label
- Read-only filesystem
- Broken symbolic link
- Different mount namespace or container path

---

<a id="scenario-19-log-rotation-runs-but-disk-space-does-not-drop"></a>
## Scenario 19: Log Rotation Runs but Disk Space Does Not Drop

### Symptom

Old logs were rotated or deleted, but the filesystem remains full.

### Diagnosis

#### Confirm logrotate activity

```bash
journalctl -u logrotate.service
```

```bash
cat /var/lib/logrotate/logrotate.status
```

#### Find open deleted logs

```bash
lsof +L1
```

#### Identify the service holding them

```bash
ps -fp PID
```

#### Confirm how the application reopens logs

Check the logrotate stanza:

```bash
cat /etc/logrotate.d/application
```

Look for:

- `postrotate`
- `copytruncate`
- Missing reload signal

#### Reload or restart appropriately

```bash
systemctl reload service_name
```

or:

```bash
systemctl restart service_name
```

#### Verify

```bash
lsof +L1
df -h
```

### Prevention

Ensure the application receives its documented reopen signal after rotation.

---

<a id="scenario-20-an-application-is-slow-but-not-obviously-broken"></a>
## Scenario 20: An Application Is Slow but Not Obviously Broken

### Symptom

Requests complete, but latency has increased.

### Layered Diagnosis

#### Measure the full request

```bash
curl -sS -o /dev/null \
  -w 'dns=%{time_namelookup} connect=%{time_connect} tls=%{time_appconnect} first_byte=%{time_starttransfer} total=%{time_total}\n' \
  https://application.example.com/
```

Interpretation:

- High DNS time: resolver problem
- High connect time: route, packet loss, firewall, or listener backlog
- High TLS time: CPU, certificate, or network issue
- High first-byte time: server or backend processing
- High total after first byte: slow transfer or client path

#### Check system resources

```bash
uptime
vmstat 1
mpstat -P ALL 1
iostat -xz 1
free -h
```

#### Check socket pressure

```bash
ss -s
ss -nt state syn-recv
```

#### Check the service

```bash
systemctl status service_name
journalctl -u service_name --since "15 minutes ago"
```

#### Check downstream dependencies

Test:

- Database port
- DNS
- Remote API
- NFS storage
- Authentication service

#### Trace one slow worker if safe

```bash
strace -f -tt -T -p PID
```

### Operational Principle

“Slow” is not a root cause. Break request time into DNS, connection, TLS, application, backend, storage, and response-transfer phases.

<a id="scenario-21-a-named-acl-user-still-gets-permission-denied"></a>
## Scenario 21: A Named ACL User Still Gets `Permission denied`

### Symptom

The ACL appears to grant access:

```text
user:alice:rwx
```

but Alice cannot write.

### Diagnosis

#### Check effective permissions

```bash
getfacl /path/to/file
```

Example:

```text
user:alice:rwx                 #effective:r-x
mask::r-x
```

The mask removes write permission.

#### Check every directory component

```bash
namei -l /path/to/file
```

Alice needs execute permission on every parent directory.

#### Test directly as Alice

```bash
sudo -u alice test -w /path/to/file && echo writable
```

#### Check SELinux after DAC and ACL checks

```bash
ls -lZ /path/to/file
ausearch -m AVC,USER_AVC -ts recent
```

### Resolution Options

Allow write access through the mask:

```bash
setfacl -m m::rwx /path/to/file
```

Or retain the restrictive mask and make the requested entry match reality:

```bash
setfacl -n -m u:alice:r-x /path/to/file
```

### Verification

```bash
getfacl /path/to/file
sudo -u alice test -w /path/to/file && echo writable
```

---

<a id="scenario-22-a-file-works-before-mv-but-fails-in-its-new-selinux-location"></a>
## Scenario 22: A File Works Before `mv` but Fails in Its New SELinux Location

### Symptom

A file is moved into a service directory. Unix permissions look correct, but the service receives an SELinux denial.

### Diagnosis

#### Inspect the moved file

```bash
ls -liZ /destination/path/file
```

#### Compare expected labels in that directory

```bash
ls -ldZ /destination/path
semanage fcontext -l | grep '/destination/path'
```

#### Search the denial

```bash
ausearch -m AVC,USER_AVC -ts recent
```

### Cause

A same-filesystem `mv` preserves the inode and its SELinux label. The file may still carry the context from its old directory.

### Resolution

Restore the expected context:

```bash
restorecon -v /destination/path/file
```

For the complete tree:

```bash
restorecon -Rv /destination/path
```

### Verification

```bash
ls -lZ /destination/path/file
systemctl restart service_name
journalctl -u service_name --since "5 minutes ago"
```

<a id="scenario-23-a-web-service-cannot-read-content-under-srv"></a>
## Scenario 23: A Web Service Cannot Read Content Under **`/srv`**

### Symptom

The web service reads its default content but receives `Permission denied` for **`/srv/site`**.

### Diagnosis

```bash
namei -l /srv/site/index.html
sudo -u apache test -r /srv/site/index.html && echo readable
ls -ldZ /srv/site
ls -lZ /srv/site/index.html
matchpathcon -V /srv/site/index.html
ausearch -m AVC,USER_AVC -ts recent -c httpd -i
```

The service account may differ by distribution.

### Resolution

Read-only content:

```bash
semanage fcontext -a -t httpd_sys_content_t '/srv/site(/.*)?'
```

Writable upload directory only:

```bash
semanage fcontext -a -t httpd_sys_rw_content_t '/srv/site/uploads(/.*)?'
```

Apply:

```bash
restorecon -Rv /srv/site
```

Verify:

```bash
curl -I http://127.0.0.1/
ausearch -m AVC,USER_AVC -ts recent
```

---

<a id="scenario-24-a-service-cannot-bind-to-a-custom-port"></a>
## Scenario 24: A Service Cannot Bind to a Custom Port

### Symptom

A service configured for TCP port `8088` fails with `Permission denied`.

### Diagnosis

```bash
ss -lntp | grep ':8088'
ausearch -m AVC,USER_AVC -ts recent -i
semanage port -l | grep -E 'http_port_t|8088'
```

Look for:

```text
tclass=tcp_socket
{ name_bind }
```

### Resolution for an HTTP Service

```bash
semanage port -a -t http_port_t -p tcp 8088
firewall-cmd --add-port=8088/tcp
systemctl restart httpd
ss -lntp | grep ':8088'
curl -I http://127.0.0.1:8088/
firewall-cmd --runtime-to-permanent
```

The listener, SELinux port type, and firewall are separate layers.

---

<a id="scenario-25-a-user-is-in-wheel-but-sudo-fails"></a>
## Scenario 25: A User Is in `wheel` but `sudo` Fails

### Diagnosis

```bash
id username
getent group wheel
sudo -l -U username
visudo -c
find /etc/sudoers.d -maxdepth 1 -type f \
  -printf '%m %u:%g %p\n'
journalctl _COMM=sudo --since "30 minutes ago"
```

Common causes:

- Session does not contain recently added group membership
- `%wheel` rule is disabled
- Drop-in syntax error
- Drop-in file permissions are wrong
- Command path or arguments do not match
- The user has only command-specific authorization

Edit safely:

```bash
visudo -f /etc/sudoers.d/application-admins
visudo -c
```

Do not grant unrestricted `NOPASSWD: ALL` to solve one narrow problem.

---

<a id="scenario-26-repeated-ssh-authentication-failures"></a>
## Scenario 26: Repeated SSH Authentication Failures

### Diagnosis

```bash
journalctl -u sshd --since "1 hour ago" \
  | grep -i 'failed password'
lastb -ai | head -50
faillock --user username
ss -lntp | grep ':22'
firewall-cmd --zone=public --list-all
sshd -T | grep -E \
  'permitrootlogin|passwordauthentication|pubkeyauthentication|maxauthtries|allowgroups'
```

Defensive actions may include:

- Disable direct root login
- Prefer key authentication
- Restrict logins with `AllowGroups`
- Restrict firewall sources
- Review PAM lockout policy
- Alert on failures and successful logins from unexpected sources

Before disabling passwords, confirm key login and recovery access.

---

<a id="scenario-27-determine-who-changed-a-security-file"></a>
## Scenario 27: Determine Who Changed a Security File

### Symptom

**`/etc/ssh/sshd_config`** changed unexpectedly.

### Existing Evidence

```bash
stat /etc/ssh/sshd_config
rpm -qf /etc/ssh/sshd_config
rpm -V openssh-server
ausearch -f /etc/ssh/sshd_config -ts today -i
ausearch -k sshd_config -ts today -i
```

### Monitor Future Changes

Temporary rule:

```bash
auditctl -w /etc/ssh/sshd_config -p wa -k sshd_config
```

Persistent rule:

```text
-w /etc/ssh/sshd_config -p wa -k sshd_config
```

Load and verify:

```bash
augenrules --load
auditctl -l | grep sshd_config
```

If no audit rule or event existed when the file changed, timestamps alone may not identify the exact actor.

---

<a id="scenario-28-systemd-hardening-breaks-a-service"></a>
## Scenario 28: systemd Hardening Breaks a Service

### Diagnosis

```bash
systemctl cat service_name
systemctl status service_name --no-pager -l
journalctl -u service_name -b -n 200 --no-pager
ausearch -m AVC,USER_AVC -ts recent -i
systemd-analyze security service_name
```

Common causes:

- `ProtectSystem=strict` blocks a write
- `ProtectHome=yes` hides required files
- `PrivateTmp=yes` changes temporary-path visibility
- `RestrictAddressFamilies=` blocks a socket family
- `CapabilityBoundingSet=` removes a required capability

Add the narrowest exception:

```ini
[Service]
ProtectSystem=strict
ReadWritePaths=/var/lib/myapp /var/log/myapp
```

Then:

```bash
systemctl daemon-reload
systemctl restart service_name
systemctl status service_name --no-pager -l
```

Do not remove every hardening directive to fix one required path.

---

<a id="scenario-29-an-unexpected-setuid-or-capability-binary-appears"></a>
## Scenario 29: An Unexpected Setuid or Capability Binary Appears

### Diagnosis

```bash
stat /path/to/binary
ls -lZ /path/to/binary
getcap /path/to/binary
sha256sum /path/to/binary
rpm -qf /path/to/binary
```

If package-owned:

```bash
rpm -V package_name
rpm -qi package_name
```

Review activity:

```bash
ausearch -f /path/to/binary -i
lsof /path/to/binary
ps -eo pid,user,lstart,exe,args | grep -F '/path/to/binary'
```

Follow incident-response policy. Immediately deleting the file may destroy evidence or break a legitimate service.

---

<a id="scenario-30-return-selinux-from-permissive-to-enforcing"></a>
## Scenario 30: Return SELinux from Permissive to Enforcing

### Diagnosis

```bash
getenforce
sestatus
ausearch -m AVC,USER_AVC -ts boot -i
ausearch -m AVC,USER_AVC -ts boot --raw | audit2why
```

Review:

```bash
semanage fcontext -C -l
semanage port -C -l
semanage permissive -l
getsebool -a
```

Correct labels, ports, booleans, and application behavior.

Test enforcing mode:

```bash
setenforce 1
systemctl --failed
journalctl -p err..alert --since "10 minutes ago"
ausearch -m AVC,USER_AVC -ts recent -i
```

Verify persistent configuration:

```bash
grep '^SELINUX=' /etc/selinux/config
```

Expected:

```text
SELINUX=enforcing
```

<a id="scenario-31-a-newly-attached-disk-does-not-appear"></a>
## Scenario 31: A Newly Attached Disk Does Not Appear

### Symptom

The virtualization or storage team added a disk, but `lsblk` does not show it.

### Diagnosis

#### Record current inventory

```bash
lsblk -d -o NAME,SIZE,MODEL,SERIAL
lsscsi
```

#### Rescan SCSI hosts

```bash
for host in /sys/class/scsi_host/host*; do
    echo "- - -" > "$host/scan"
done
```

Wait for udev:

```bash
udevadm settle
```

#### Recheck

```bash
lsblk -d -o NAME,SIZE,MODEL,SERIAL
lsscsi
```

#### Search kernel messages

```bash
journalctl -k --since "10 minutes ago" \
  | grep -iE 'scsi|sd[a-z]|capacity|I/O error|reject'
```

#### Verify device identity

```bash
ls -l /dev/disk/by-id/
```

### Likely Causes

- Hypervisor change not applied to the correct VM
- SAN LUN not mapped
- SCSI scan not performed
- Multipath configuration issue
- Kernel or controller error
- Device present under a different name

> **Warning:** Do not initialize a newly discovered disk until its serial or WWN is verified.

---

<a id="scenario-32-a-new-partition-exists-in-fdisk-but-not-in-dev"></a>
## Scenario 32: A New Partition Exists in `fdisk` but Not in **`/dev`**

### Symptom

The partition table shows **`/dev/sdb1`**, but the device node is missing.

### Diagnosis

```bash
fdisk -l /dev/sdb
lsblk /dev/sdb
partprobe /dev/sdb
udevadm settle
ls -l /dev/sdb*
journalctl -k --since "10 minutes ago"
```

Check whether the disk is actively used:

```bash
findmnt
pvs
cat /proc/mdstat
```

### Likely Causes

- Kernel has not reread the partition table
- Existing partitions are busy
- Device mapper or multipath owns the disk
- Invalid or overlapping partition layout
- Udev processing delay

If rereading is unsafe because the device is busy, schedule maintenance rather than forcing the change.

---

<a id="scenario-33-a-server-enters-emergency-mode-because-of-etc-fstab"></a>
## Scenario 33: A Server Enters Emergency Mode Because of **`/etc/fstab`**

### Diagnosis

```bash
journalctl -xb
systemctl --failed --type=mount
cat /etc/fstab
lsblk -f
blkid
findmnt --verify --verbose
mount -av
```

Common causes:

- Wrong UUID
- Missing mount point
- Wrong filesystem type
- Invalid option
- Removed device
- Network mount unavailable
- Typographical error

Back up before editing:

```bash
cp -a /etc/fstab /etc/fstab.before-storage-fix
```

Correct and test:

```bash
findmnt --verify --verbose
mount -av
systemctl daemon-reload
```

Return to the normal target:

```bash
systemctl default
```

Use `nofail` or automount options only when boot should genuinely continue without that storage.

---

<a id="scenario-34-df-is-full-but-du-shows-much-less-data"></a>
## Scenario 34: `df` Is Full but `du` Shows Much Less Data

### Diagnosis

```bash
findmnt -T /affected/path
df -hT /affected/path
du -xsh /affected/path
lsof +L1 /affected/path
```

If an open deleted file appears:

```bash
ps -fp PID
systemctl status service_name
```

Preferred fix:

```bash
systemctl reload service_name
```

If reload does not reopen the file:

```bash
systemctl restart service_name
```

Verify:

```bash
lsof +L1 /affected/path
df -hT /affected/path
```

Other causes:

- Hidden data beneath another mount
- Different namespace
- Permission-denied directories excluded from `du`
- Filesystem metadata or snapshots

Do not truncate arbitrary file descriptors unless the application impact is understood.

---

<a id="scenario-35-no-space-left-on-device-with-free-blocks"></a>
## Scenario 35: “No Space Left on Device” with Free Blocks

### Diagnosis

```bash
df -hT /affected/path
df -i /affected/path
```

If inode use is 100%:

```bash
find /affected/path -xdev -type f -printf '%h\n' 2>/dev/null \
  | sort | uniq -c | sort -n | tail -30
```

Inspect likely producers:

```bash
find /affected/path -xdev -type f -size -4k \
  -printf '%h\n' 2>/dev/null \
  | sort | uniq -c | sort -n | tail -30
```

Common causes:

- Session-file leak
- Queue explosion
- Cache cleanup failure
- One-file-per-request application behavior
- Temporary-file leak

Delete only files that are safe according to the application.

Fix the producer and cleanup policy, not only the symptom.

---

<a id="scenario-36-extend-an-xfs-lvm-filesystem-without-downtime"></a>
## Scenario 36: Extend an XFS LVM Filesystem Without Downtime

### Symptom

**`/app`** is nearly full, and the VG has free space.

### Diagnosis

```bash
findmnt -T /app
df -hT /app
vgs -o vg_name,vg_size,vg_free
lvs -a -o lv_name,vg_name,lv_size,devices
```

Confirm the filesystem is XFS:

```bash
findmnt -no FSTYPE /app
```

Extend by 20 GiB:

```bash
lvextend -r -L +20G /dev/vg_data/lv_app
```

Verify:

```bash
lvs /dev/vg_data/lv_app
df -hT /app
xfs_info /app
journalctl -k --since "10 minutes ago"
```

The application remains online because both the LV and XFS support online growth.

---

<a id="scenario-37-the-virtual-disk-grew-but-the-filesystem-did-not"></a>
## Scenario 37: The Virtual Disk Grew but the Filesystem Did Not

### Symptom

The hypervisor enlarged the disk, but `df` is unchanged.

### Layer Identification

```bash
findmnt -T /mountpoint
lsblk -f
pvs
vgs
lvs
```

Assume the stack is:

```text
/dev/sda → /dev/sda3 → PV → VG → LV → XFS
```

#### Rescan disk

```bash
echo 1 > /sys/class/block/sda/device/rescan
lsblk /dev/sda
```

#### Grow partition

```bash
growpart /dev/sda 3
partprobe /dev/sda
udevadm settle
```

#### Grow PV

```bash
pvresize /dev/sda3
```

#### Confirm free extents

```bash
pvs
vgs
```

#### Grow LV and filesystem

```bash
lvextend -r -l +100%FREE /dev/vg_name/lv_name
```

#### Verify

```bash
lsblk
pvs
vgs
lvs
df -hT /mountpoint
```

A larger disk does not automatically enlarge partitions, PVs, LVs, or filesystems.

---

<a id="scenario-38-the-filesystem-suddenly-became-read-only"></a>
## Scenario 38: The Filesystem Suddenly Became Read-Only

### Diagnosis

```bash
findmnt -T /affected/path
journalctl -k -g 'read-only|I/O error|XFS|EXT4|Buffer I/O'
lsblk -f
lvs -a -o +devices
cat /proc/mdstat
iostat -xz 1
```

Check device health:

```bash
smartctl -a /dev/DEVICE
```

### Resolution

1. Stop unnecessary writes.
2. Protect application data.
3. Identify the underlying device or path error.
4. Repair hardware or connectivity.
5. Schedule an offline filesystem check.
6. Restore service only after verification.

> **Warning:** Do not blindly use:

```bash
mount -o remount,rw /mountpoint
```

The read-only state may be protecting the filesystem from additional corruption.

---

<a id="scenario-39-an-lvm-logical-volume-is-missing-after-reboot"></a>
## Scenario 39: An LVM Logical Volume Is Missing After Reboot

### Diagnosis

```bash
pvs
vgs
lvs -a -o +devices
pvscan
vgscan
lvscan
```

Activate VGs:

```bash
vgchange -ay
```

Inspect devices:

```bash
lsblk -f
blkid
```

Check LVM logs and boot journal:

```bash
journalctl -b | grep -iE 'lvm|device-mapper|physical volume|volume group'
```

Check metadata archives:

```bash
ls -l /etc/lvm/backup /etc/lvm/archive
vgcfgrestore -l vg_name
```

Common causes:

- Missing disk or SAN path
- PV UUID not visible
- Device filtering
- Inactive VG
- Damaged LVM metadata
- Multipath inconsistency
- Wrong initramfs for root storage

Do not run `pvcreate` on the missing PV. That can overwrite its LVM metadata.

---

<a id="scenario-40-a-thin-pool-is-almost-full"></a>
## Scenario 40: A Thin Pool Is Almost Full

### Diagnosis

```bash
lvs -a -o lv_name,lv_size,segtype,data_percent,metadata_percent
```

Monitor:

```bash
watch -n 2 "lvs -a -o lv_name,lv_size,data_percent,metadata_percent"
```

Check VG space:

```bash
vgs -o vg_name,vg_size,vg_free
```

Extend data space:

```bash
lvextend -L +100G vg_name/thin_pool
```

Extend metadata when required:

```bash
lvextend --poolmetadatasize +1G vg_name/thin_pool
```

Verify:

```bash
lvs -a -o lv_name,lv_size,data_percent,metadata_percent
```

### Prevention

- Alert before critical thresholds
- Reserve VG free space
- Configure tested automatic extension
- Track virtual allocation separately from physical use
- Remove unused thin snapshots carefully

A thin-pool outage can affect every thin LV in the pool.

---

<a id="scenario-41-raid1-is-degraded"></a>
## Scenario 41: RAID1 Is Degraded

### Diagnosis

```bash
cat /proc/mdstat
mdadm --detail /dev/md0
journalctl -k -g 'md0|raid|I/O error|failed'
```

Identify healthy and failed members by serial or WWN:

```bash
lsblk -d -o NAME,SIZE,MODEL,SERIAL,WWN
mdadm --examine /dev/sdX1
```

Remove failed member:

```bash
mdadm /dev/md0 --fail /dev/FAILED_MEMBER
mdadm /dev/md0 --remove /dev/FAILED_MEMBER
```

Prepare the correct replacement, then add it:

```bash
mdadm /dev/md0 --add /dev/NEW_MEMBER
```

Monitor:

```bash
watch -n 2 cat /proc/mdstat
```

Verify:

```bash
mdadm --detail /dev/md0
```

Do not assume **`/dev/sdb`** is still the failed disk after a reboot. Verify serial numbers.

---

<a id="scenario-42-umount-reports-target-is-busy"></a>
## Scenario 42: `umount` Reports “Target Is Busy”

### Diagnosis

```bash
findmnt -R /data
fuser -vm /data
lsof +f -- /data
```

Check current shell:

```bash
pwd
```

Move away if necessary:

```bash
cd /
```

Check service use:

```bash
systemctl list-units --type=service --state=running
```

Stop only the identified service:

```bash
systemctl stop service_name
```

Retry:

```bash
umount /data
```

Avoid `umount -l` until active users and nested mounts are understood.

---

<a id="scenario-43-disk-i-o-latency-causes-high-load-average"></a>
## Scenario 43: Disk I/O Latency Causes High Load Average

### Diagnosis

```bash
uptime
vmstat 1
iostat -xz 1
pidstat -d 1
ps -eo state,pid,ppid,wchan:32,comm,args | awk '$1 ~ /^D/'
journalctl -k -g 'I/O error|timeout|reset|blocked for more than'
```

Interpretation:

- High `b` in `vmstat` means blocked tasks
- High `await` means slow completion
- Growing queue means requests are waiting
- `D` state often indicates uninterruptible storage wait
- Kernel resets suggest path or device instability

Investigate the device, SAN, RAID, NFS server, or workload creating the latency.

A reboot may clear the queue temporarily but usually removes valuable evidence.

---

<a id="scenario-44-a-hung-nfs-mount-freezes-commands"></a>
## Scenario 44: A Hung NFS Mount Freezes Commands

### Symptom

`df`, `du`, `ls`, or application shutdown hangs.

### Diagnosis

```bash
findmnt -t nfs,nfs4
nfsstat -m
ps -eo state,pid,ppid,wchan:32,comm,args | awk '$1 ~ /^D/'
ip route get NFS_SERVER_IP
nc -vz NFS_SERVER 2049
tcpdump -ni any host NFS_SERVER_IP and port 2049
```

Check server-side export and service state if accessible:

```bash
showmount -e NFS_SERVER
```

Common causes:

- NFS server outage
- Routing or firewall change
- DNS issue
- Storage failure behind the NFS server
- Incorrect mount-time resilience settings
- Stale server state

Coordinate recovery according to application consistency and mount semantics.

---

<a id="scenario-45-an-lv-was-extended-but-df-did-not-change"></a>
## Scenario 45: An LV Was Extended but `df` Did Not Change

### Diagnosis

```bash
lvs /dev/vg_name/lv_name
findmnt -T /mountpoint
df -hT /mountpoint
```

The LV may be larger while the filesystem still has its old size.

For XFS:

```bash
xfs_growfs /mountpoint
```

For ext4:

```bash
resize2fs /dev/vg_name/lv_name
```

Verify:

```bash
df -hT /mountpoint
```

Common cause:

```bash
lvextend
```

was used without:

```bash
-r
```

The LV and filesystem are separate layers.

---

<a id="scenario-46-a-snapshot-became-invalid"></a>
## Scenario 46: A Snapshot Became Invalid

### Diagnosis

```bash
lvs -a -o lv_name,origin,lv_size,lv_attr,data_percent
journalctl -k -g 'snapshot|device-mapper'
```

A classic snapshot that reaches its allocated capacity can become invalid.

### Resolution

- Stop relying on the invalid snapshot
- Verify the origin LV
- Remove the invalid snapshot under a controlled plan
- Recreate it with appropriate capacity
- Reduce snapshot lifetime
- Monitor `Data%`
- Consider application-native backup methods

A snapshot is not a permanent backup.

---

<a id="scenario-47-the-wrong-disk-was-almost-selected-for-formatting"></a>
## Scenario 47: The Wrong Disk Was Almost Selected for Formatting

### Safe Verification Procedure

Before any destructive command:

```bash
lsblk -d -o NAME,PATH,SIZE,MODEL,SERIAL,WWN
lsblk -f
findmnt
pvs
cat /proc/mdstat
wipefs /dev/CANDIDATE
```

Resolve a stable identifier:

```bash
readlink -f /dev/disk/by-id/EXPECTED_ID
```

Confirm it matches the intended device.

Only after verification should a destructive action be considered.

Use this principle:

> Device names are hints; serial numbers, WWNs, topology, and ownership are evidence.
---

<a id="chapter-6-quick-reference"></a>
# Chapter 6: Quick Reference

Use these compact workflows and indexes during initial triage or when you already understand the underlying concepts.

<a id="compact-troubleshooting-workflows"></a>
## Compact Troubleshooting Workflows

### Identify the Process Listening on a Port

**Problem:** A TCP or UDP port is in use, but the owning process is unknown.

**Diagnosis:**

```bash
ss -lntp | grep ':PORT'
lsof -i :PORT
fuser -v PORT/tcp
ps -fp PID
ls -l /proc/PID/fd/
```

**Solution:** Confirm that the process belongs to the expected service. Review the service configuration before stopping or restarting it.

> **Warning:** Do not terminate a listener solely because it is unfamiliar. First identify the service owner and assess production impact.

### Recover Space Held by Deleted Open Files

**Symptom:** `df` reports a full filesystem, but `du` cannot account for the used space.

**Likely cause:** A running process still has a deleted file open through a file descriptor.

**Diagnosis:**

```bash
df -hT
du -xsh /var/* 2>/dev/null | sort -h
lsof +L1
```

**Solution:** After identifying the owning service, reload or restart it using the least disruptive supported action:

```bash
systemctl reload service_name
```

If reload is unsupported or does not release the descriptor:

```bash
systemctl restart service_name
```

### Diagnose a Log That Is Not Rotating

**Symptom:** A log file continues to grow or expected rotated files are absent.

**Diagnosis:**

```bash
grep -R --line-number '/path/to/log' /etc/logrotate.conf /etc/logrotate.d/
logrotate -d /etc/logrotate.conf
cat /var/lib/logrotate/logrotate.status
systemctl status logrotate.timer
journalctl -u logrotate.service
ls -lZ /path/to/log
lsof /path/to/log
```

**Solution:** Correct the matching configuration, permissions, SELinux context, timer state, or application log-reopen behavior. Re-test with debug mode before forcing a rotation.

### Locate a Missing Package or Command

**Problem:** A required command is unavailable or the package name is unknown.

**Diagnosis and solution:**

```bash
command -v command_name
dnf provides '*/command_name'
dnf info package_name
dnf install package_name
rpm -q package_name
rpm -ql package_name
```

### Restore a Modified Packaged File

**Symptom:** A file installed by an RPM package has been changed, corrupted, or removed.

**Diagnosis:**

```bash
rpm -qf /path/to/file
rpm -V package_name
rpm -qc package_name
```

**Solution:** Preserve any required local configuration, then reinstall the package when appropriate:

```bash
dnf reinstall package_name
```

<a id="command-index"></a>
## Command Index

### Processes and FDs

```bash
ps aux
ps -ef
ps -fp PID
pgrep sshd
pgrep -a sshd
pidof sshd
lsof -p PID
lsof -i :22
lsof /path/to/file
lsof +L1
ls -l /proc/PID/fd/
readlink /proc/PID/fd/FD
cat /proc/PID/fdinfo/FD
```

### Sockets

```bash
ss -lnt
ss -lntp
ss -antp
ss -lnup
ss -lx
ss -lxnp
fuser -v 22/tcp
```

### Inodes and Links

```bash
ls -li
stat filename
ln source_file hardlink_name
ln -s target link_name
readlink link_name
readlink -f link_name
find /path -inum INODE_NUMBER
find /path -xdev -type f -links +1
mkdir directory_name
ls -la directory_name
```

### Logrotate

```bash
cat /etc/logrotate.conf
ls -l /etc/logrotate.d/
logrotate -d /etc/logrotate.conf
logrotate -v /etc/logrotate.conf
logrotate -f /etc/logrotate.conf
logrotate -vf /etc/logrotate.conf
systemctl status logrotate.timer
systemctl list-timers logrotate.timer
systemctl status logrotate.service
journalctl -u logrotate.service
cat /var/lib/logrotate/logrotate.status
```

### DNF

```bash
dnf repolist
dnf repolist all
dnf repoinfo
dnf search keyword
dnf info package_name
dnf list installed
dnf list available
dnf install package_name
dnf remove package_name
dnf check-update
dnf upgrade
dnf upgrade --security
dnf reinstall package_name
dnf downgrade package_name
dnf --showduplicates list package_name
dnf provides '*/command'
dnf history
dnf clean all
dnf makecache
dnf group list
dnf module list
```

### RPM

```bash
rpm -q package_name
rpm -qa
rpm -qi package_name
rpm -ql package_name
rpm -qc package_name
rpm -qd package_name
rpm -qR package_name
rpm -qf /path/to/file
rpm -qpi package-file.rpm
rpm -qpl package-file.rpm
rpm -qpR package-file.rpm
rpm -K package-file.rpm
rpm -ivh package-file.rpm
rpm -Uvh package-file.rpm
rpm -e package_name
rpm -V package_name
rpm -Va
rpm --import /path/to/key
```

---

<a id="important-files-index"></a>
## Important Files Index

```text
/proc/PID/fd/
/proc/PID/fdinfo/
/proc/PID/status
/proc/PID/cmdline
/proc/PID/environ
/proc/PID/maps
/etc/logrotate.conf
/etc/logrotate.d/
/var/lib/logrotate/logrotate.status
/var/lib/logrotate/status
/usr/sbin/logrotate
/usr/lib/systemd/system/logrotate.service
/usr/lib/systemd/system/logrotate.timer
/etc/dnf/dnf.conf
/etc/yum.conf
/etc/yum.repos.d/
/var/cache/dnf/
/var/lib/rpm/
/etc/pki/rpm-gpg/
/var/log/dnf.log
/var/log/dnf.rpm.log
/var/log/yum.log
```

---

<a id="useful-one-liners-for-fast-triage"></a>
## Useful One-Liners for Fast Triage

### Top CPU processes

```bash
ps -eo pid,ppid,user,%cpu,%mem,etime,comm,args \
  --sort=-%cpu | head -20
```

### Top memory processes

```bash
ps -eo pid,ppid,user,%mem,rss,vsz,etime,comm,args \
  --sort=-rss | head -20
```

### Processes in uninterruptible sleep

```bash
ps -eo state,pid,ppid,wchan:32,comm,args | awk '$1 ~ /^D/'
```

### Zombie processes

```bash
ps -eo stat,pid,ppid,user,comm,args | awk '$1 ~ /^Z/'
```

### Failed units

```bash
systemctl --failed --no-pager
```

### Important current-boot errors

```bash
journalctl -b -p err..alert --no-pager
```

### Listening sockets

```bash
ss -lntup
```

### Established connections by destination

```bash
ss -nt | awk 'NR>1 {print $5}' | sort | uniq -c | sort -n
```

### Large files over 1 GiB

```bash
find / -xdev -type f -size +1G \
  -printf '%s %p\n' 2>/dev/null | sort -n
```

### Deleted open files

```bash
lsof +L1
```

### Filesystems over 90%

```bash
df -P | awk 'NR>1 {gsub("%","",$5); if ($5 >= 90) print}'
```

### Inode usage over 90%

```bash
df -Pi | awk 'NR>1 {gsub("%","",$5); if ($5 >= 90) print}'
```

### Recent kernel errors

```bash
journalctl -k --since "1 hour ago" -p warning..alert
```

### Recent configuration changes

```bash
find /etc -xdev -type f -mmin -120 \
  -printf '%TY-%Tm-%Td %TH:%TM %p\n' 2>/dev/null | sort
```

### Network interface errors

```bash
ip -s link
```

### Route decision

```bash
ip route get DESTINATION_IP
```

### Test one TCP endpoint

```bash
nc -vz -w 3 HOST PORT
```

### Show command exit status

```bash
command
echo $?
```

A nonzero exit status usually means failure, but command-specific documentation defines exact meanings.

---

<a id="chapter-7-troubleshooting-safety-rules"></a>
# Chapter 7: Troubleshooting Safety Rules

> **Warning:** Safety rules are part of the troubleshooting procedure, not optional advice. Preserve evidence, protect data, and minimize service disruption.

1. Collect logs and state before restarting or rebooting.
2. Prefer read-only inspection commands first.
3. Change one item at a time.
4. Keep a backup before editing configuration:

```bash
cp -a /etc/example.conf /etc/example.conf.$(date +%F-%H%M%S).bak
```

5. Validate configuration before reload or restart.
6. Use `reload` instead of `restart` when supported and appropriate.
7. Do not disable SELinux or flush the firewall as a diagnostic shortcut.
8. Do not use `kill -9` before trying a normal termination signal.
9. Do not run `fsck`, `e2fsck`, or `xfs_repair` blindly on mounted read-write filesystems.
10. Do not delete files until ownership and application purpose are understood.
11. Do not force RPM transactions with `--nodeps` or `--force` during ordinary troubleshooting.
12. Record the exact fix and the evidence proving it worked.

<a id="signal-escalation-for-a-process"></a>
## Signal escalation for a process

Request normal termination:

```bash
kill -TERM PID
```

Wait and verify:

```bash
ps -p PID
```

Only if the process cannot terminate normally and the impact is understood:

```bash
kill -KILL PID
```

`SIGKILL` gives the process no chance to clean up files, release application locks cleanly, or flush buffered data.

---

<a id="chapter-8-document-maintenance-and-change-log"></a>
# Chapter 8: Document Maintenance and Change Log

This chapter records how the reference is maintained and summarizes significant additions.

<a id="maintenance-process"></a>
## Maintenance Process

This is the initial project checkpoint.

For future updates:

1. New commands and notes will be added to `README.md`.
2. The saved checkpoint will remain unchanged.
3. A comparison will be made between the checkpoint and the updated file.
4. The update summary will identify exactly what was added or changed.

Checkpoint files:

- `README.checkpoint-2026-07-27.md`
- `README.checkpoint.json`

---

<a id="future-update-log"></a>
## Future Update Log

### Checkpoint 1 — 2026-07-27

Initial topics recorded:

- Processes and process inspection
- File descriptors
- Sockets and port ownership
- **`/proc/PID/fd`**
- Inodes
- Hard links
- Directory link count
- Symbolic links
- `logrotate`
- DNF package management
- RPM package inspection and verification
- Important files and troubleshooting workflows

Future entries will be added below this section while preserving the checkpoint copy.

---

<a id="troubleshooting-update-log"></a>
## Troubleshooting Update Log

### Update 6 — 2026-07-28

Added and refined:

- Storage topology and layer-by-layer troubleshooting
- Stable disk identification using serial numbers, WWNs, and **`/dev/disk`**
- MBR and GPT comparison
- `fdisk`, `parted`, `gdisk`, `sfdisk`, `partprobe`, and `udevadm`
- Partition-table backup and recovery
- Signature discovery and safe `wipefs` preview
- XFS and ext4 creation, labels, growth, checks, and repair warnings
- Mounting, unmounting, **`/etc/fstab`**, and systemd mount units
- Capacity, inode, deleted-open-file, and busy-mount analysis
- Swap partitions, swap files, and priorities
- Complete LVM lifecycle: PV, VG, LV, online growth, `pvresize`, `pvmove`, and metadata backups
- LVM snapshots and thin provisioning
- Software RAID inspection, creation, degraded-array recovery, and rebuild monitoring
- Stratis and LVM VDO command references
- SMART, NVMe, and storage-performance commands
- NFS and remote-storage troubleshooting
- Zero-downtime storage-expansion checklist
- Storage metadata backup checklist
- Seventeen additional storage troubleshooting scenarios

### Update 5 — 2026-07-27

Added and refined:

- Linux security layers and DAC versus MAC
- SELinux modes, context fields, domains, and object types
- Current and expected labels with `matchpathcon`
- Persistent labeling using `semanage fcontext` and `restorecon`
- `chcon` limitations
- SELinux booleans, port types, and login mappings
- AVC analysis using `ausearch`, `audit2why`, and `sealert`
- Local policy modules and per-domain permissive mode
- SELinux relabeling and recovery
- `umask`, setuid, setgid, sticky-bit, and world-writable audits
- Linux capabilities
- Account, PAM, authselect, and failed-login checks
- Least-privilege sudo configuration
- SSH validation and hardening
- Firewall source, zone, service, and rich-rule controls
- auditd rules and reports
- Package verification, security advisories, and AIDE
- systemd service sandboxing
- Mount-option hardening
- Crypto policies, FIPS checks, and sysctl review
- Suspected-compromise triage and evidence collection
- Security baseline checklist and important security files
- Eight additional SELinux and security scenarios

### Update 4 — 2026-07-27

Added and refined:

- Deep comparison of `cp` and `mv`
- Same-filesystem rename versus cross-filesystem copy-and-delete behavior
- Inode, hard-link, symbolic-link, metadata, open-FD, and performance effects
- Safe directory copying, hidden-file handling, and verification
- SELinux context differences between copying and moving
- Detailed POSIX ACL mask behavior
- Why `setfacl` recalculates the mask
- How `--no-mask` and an explicit `mask::` entry affect updates
- Requested versus `#effective` ACL permissions
- Interaction between `chmod` group bits and the ACL mask
- Default ACL masks and inheritance
- ACL backup and restore commands
- Scenario for a named ACL user receiving `Permission denied`
- Scenario for a moved file retaining the wrong SELinux label

### Update 3 — 2026-07-27

Added and refined:

- Zombie-process lifecycle, process-table state, and exit-status reaping
- Correct use of `wait()`, `waitpid()`, and `waitid()`
- Explanation of why `kill -9` cannot remove a zombie
- Safe parent restart and last-resort parent termination workflow
- PID 1 and child-subreaper adoption behavior
- Commands to find, count, inspect, and verify removal of zombies
- `ulimit -v` and the inherited `RLIMIT_AS` virtual-memory limit
- Soft and hard virtual-memory limits
- `prlimit --as` notes for running processes
- Repeated process-memory monitoring with `watch`
- Accurate definitions of `VmSize`, `VmRSS`, `VmData`, and `VmSwap`
- `smaps_rollup` and `Pss` for more useful proportional memory accounting

### Update 2 — 2026-07-27

Added:

- Repeatable troubleshooting methodology
- Baseline capture commands
- systemd service diagnostics
- Advanced journal filtering
- CPU and load analysis
- `vmstat`, `mpstat`, `pidstat`, `iostat`, `strace`, and `perf`
- Memory, swap, OOM, and cgroup checks
- Disk space, inode, filesystem, and storage-latency checks
- Network, routing, DNS, firewall, and packet-capture commands
- Permissions, ACLs, and SELinux diagnostics
- Boot, kernel, initramfs, and emergency-mode checks
- LVM troubleshooting and safe extension workflows
- Time synchronization checks
- Twenty realistic troubleshooting scenarios
- Fast-triage one-liners
- Safety rules for production troubleshooting
