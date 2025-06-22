
# Linux & Internet Essentials — Complete README

This guide covers how the internet works, types of servers, differences between application and web servers, Linux basics, system management, and **clear, common commands for practical use**.

---

## How Does the Internet Work?

- The internet is a massive network of computers linked globally.
- Your device connects to an Internet Service Provider (ISP).
- Data travels as **packets** via routers to its target.
- **DNS** translates website names (like www.google.com) to IP addresses.
- The browser communicates with remote servers using protocols like **HTTP/HTTPS** and receives content.

---

## What is a Server?

- A **server** is a computer or software providing resources or services (web page, email, file) to other computers (clients) over a network.

---

## Web Server vs Application Server

| Web Server                   | Application Server                      |
|------------------------------|-----------------------------------------|
| Serves static content (HTML) | Runs code for dynamic content (e.g., Java, PHP) |
| Handles HTTP/HTTPS requests  | Handles business logic, connects to databases |
| Examples: Apache, NGINX      | Examples: Tomcat, JBoss, WebLogic       |

---

## Types of Applications

- **Standalone Apps:** Run on your computer with no need for the internet (e.g., VLC, MS Word).
- **Web Applications:** Accessible through your browser (e.g., Gmail).
- **Mobile Apps:** Designed for phones/tablets (e.g., WhatsApp).
- **Distributed Apps:** Work across a network of computers.

---

## What are Standalone Apps?

- Programs installed and run on a local device, independent of network connection.

---

## What are Web Applications?

- Apps that live on remote servers; accessed and used through your browser.

---

## Application Support & Maintenance

- **Support:** Help users, troubleshoot issues, apply quick fixes.
- **Maintenance:** Fix bugs, update features, maintain security.

---

## Linux Introduction

- **Linux** is a free, open-source operating system, popular for its security and flexibility.
- Used in servers, desktops, embedded systems.

---

## What is Linux? (OS Introduction)

- Linux is the core (kernel) + a set of tools (GNU utilities).
- Distributions: Ubuntu, CentOS, Fedora, Arch, etc.

---

## Installing Linux

### WSL + Ubuntu (on Windows)

1. Enable Windows Subsystem for Linux via Windows Features.
2. Download "Ubuntu" from Microsoft Store.
3. Launch and set up username and password.

### On AWS EC2

1. Go to EC2 dashboard. Click "Launch Instance."
2. Select Ubuntu as the OS.
3. Set instance type, storage, security group (open SSH/22).
4. Download key pair.
5. Connect:  
   ```sh
   ssh -i /path/to/key.pem ubuntu@<instance-ip>
   ```

---

## Linux vs. Windows

| Linux                | Windows                 |
|----------------------|------------------------|
| Open-source          | Closed-source          |
| Free                 | Paid                   |
| Highly customizable  | Less customizable      |
| Used for servers     | Used for desktops      |

---

## Remote Server Tools

- **SSH**: Secure command line (Linux)
- **RDP**: Remote desktop (Windows)
- **VNC**: Remote GUI (Linux/Windows)
- **PuTTY**, **MobaXterm**: Popular SSH clients on Windows
- **SCP/rsync**: Secure file copy

---

## Important Linux Concepts

- **Kernel:** The core program controlling the system.
- **Bootloader:** Loads Linux at startup (GRUB).
- **Shell:** CLI interface (bash, zsh).

---

## Desktop Environment

- Desktop GUI: GNOME, KDE, XFCE.

---

## Linux System Architecture

- Applications
- Shell
- System Utilities/Libraries
- Kernel
- Hardware

---

## Hardware Info Commands

- CPU info: `lscpu`
- Block devices: `lsblk`
- PCI devices: `lspci`
- USB info: `lsusb`
- Memory: `free`
- Disk: `df`, `du`

---

## Linux File System Structure

- `/home` - user files
- `/etc` - configs
- `/var` - variable data/logs
- `/bin`, `/sbin` - system binaries
- `/dev` - devices
- `/tmp` - temp files

---

## Linux vs. Unix

| Linux       | Unix                |
|-------------|---------------------|
| Open source | Proprietary         |
| Free        | Paid                |
| PCs/Servers | Servers/mainframes  |

---

## Linux Process States

- `R`: Running
- `S`: Sleeping
- `T`: Stopped
- `Z`: Zombie

---

## Basic Linux Commands

### Working with Files & Directories

```sh
ls            # List files
cd DIR        # Change directory
pwd           # Print current directory
mkdir FOLDER  # Create folder
rm FILE       # Remove file
rmdir FOLDER  # Remove empty folder
cp SRC DST    # Copy files/directories
mv SRC DST    # Move/Rename files/directories
touch FILE    # Create empty file/update timestamp
cat FILE      # Show file content
zcat FILE.gz  # Show content of .gz file
head FILE     # First 10 lines
tail FILE     # Last 10 lines
tail -f FILE  # Live updates (logs)
less FILE     # Page-by-page view
more FILE     # Like less
wc FILE       # Word/line/char count
diff A B      # Show differences between files
ln FILE LINK  # Hard link
ln -s FILE LINK  # Soft link (symbolic)
cut -d':' -f1 /etc/passwd  # Example of cut
tee FILE      # Output to terminal and file
sort FILE     # Sort lines
clear         # Clear terminal
```

### Editing

```sh
vi FILE       # Open file in vi editor
nano FILE     # Open file in nano editor
```

### Login & User:

```sh
ssh user@host     # SSH to server
whoami            # Show current username
who               # Show logged-in users
su USERNAME       # Switch user
sudo COMMAND      # Run as superuser
passwd            # Change password
useradd bob       # Add user bob
userdel bob       # Delete user bob
groupadd devs     # Create group
groupdel devs     # Delete group
gpasswd -a user group  # Add user to group
gpasswd -m users group # Add multiple users to group
id                # Show user & group ids
```

### Disk Usage

```sh
df -h        # Disk free/used space (human-readable)
du -sh DIR   # Show size of directory
```

### Processes

```sh
ps aux       # Show all processes
top          # Live process monitor
kill PID     # Kill process
fuser -n tcp 22  # Show process using port 22
nohup CMD    # Run command immune to hangups
free -h      # Show RAM usage
vmstat       # System activity, memory, CPU etc.
```

### System Info

```sh
uname -a     # System info
uptime       # How long running
date         # Date and time
which CMD    # Path of command
shutdown now # Shutdown system
reboot       # Reboot system
```

### Package Management

```sh
apt update     # Update package list (Debian/Ubuntu)
apt install PKG # Install package
yum install PKG # Install (RedHat/CentOS)
dnf install PKG # Install (Fedora)
pacman -S PKG   # Install (Arch)
```

### Permissions & Links

```sh
chmod 755 FILE        # Set permissions
chown user:group FILE # Change owner
chgrp group FILE      # Change group
```

### Compression

```sh
tar -czvf out.tar.gz DIR # Create compressed TAR.GZ
tar -xzvf out.tar.gz     # Extract TAR.GZ
gzip FILE                # Compress
gunzip FILE.gz           # Decompress
zip out.zip FILE         # ZIP file
unzip out.zip            # Unzip file
```

### File Transfer & Networking

```sh
scp FILE user@host:/path      # Copy file over SSH
rsync -avz SRC DST            # Sync files/directories
ftp HOST                      # FTP client
sftp user@host                # SFTP client

ping HOST         # Test connectivity
netstat -tuln     # Show open ports
ifconfig          # Network interfaces
ip addr           # Modern network config
traceroute HOST   # Route to host
tracepath HOST    # Alternative traceroute
mtr HOST          # Trace and monitor
nslookup HOST     # DNS info
dig HOST          # Detailed DNS info
telnet HOST PORT  # Connect to port
hostname          # Hostname info
arp -a            # Show ARP cache
iwconfig          # Wireless info
ss -tuln          # Socket statistics
route             # Routing table
nmap HOST         # Network scanner
wget URL          # Download file
curl URL          # Fetch URL
watch CMD         # Repeat CMD
iptables -L       # List firewall rules
```

### Advanced Text Processing

```sh
awk '{print $1}' FILE   # Extract first column
sed 's/foo/bar/g' FILE  # Replace text
grep "pattern" FILE     # Search text
```

---

## Volume Management & AWS

- **Volume:** A logical storage device.
- **Physical Volume (PV):** Actual disk or partition.
- **Volume Group (VG):** Pool of PVs.
- **Logical Volume (LV):** Resizable "virtual" partitions from VGs.

### Managing Volumes

```sh
# Show disks/partitions
lsblk

# Create a physical volume
pvcreate /dev/xvdf

# Create volume group
vgcreate myvg /dev/xvdf

# Create logical volume
lvcreate -L 10G -n myvol myvg

# Format
mkfs.ext4 /dev/myvg/myvol

# Mount
mount /dev/myvg/myvol /mnt/myvol
```

### AWS EBS Steps

- Attach new EBS volume to EC2 in AWS Console.
- SSH to instance, use `lsblk` to confirm attachment.
- Use `fdisk`, `mkfs`, and `mount` as above.

---
