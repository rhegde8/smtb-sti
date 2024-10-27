# Ubuntu vs RHEL 8 Developer Cheatsheet

### Package Management
```bash
# Ubuntu                    # RHEL 8
apt update                  dnf check-update
apt upgrade                 dnf upgrade
apt install <package>       dnf install <package>
apt remove <package>        dnf remove <package>
apt search <package>        dnf search <package>
apt list --installed       dnf list installed

# Adding Repositories
# Ubuntu
add-apt-repository ppa:<repo>

# RHEL 8
dnf config-manager --add-repo <repo_url>
```

### Service Management
```bash
# Both systems use systemctl
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl status <service>

# Enable on boot
systemctl enable <service>
```

### Firewall Management
```bash
# Ubuntu (ufw)             # RHEL 8 (firewalld)
ufw status                 firewall-cmd --state
ufw enable                 firewall-cmd --zone=public --add-port=80/tcp
ufw allow 80/tcp           firewall-cmd --reload
```

### Development Tools
```bash
# Ubuntu
apt install build-essential

# RHEL 8
dnf groupinstall "Development Tools"
```

### PostgreSQL Setup
```bash
# Ubuntu
apt install postgresql postgresql-contrib
systemctl start postgresql
sudo -u postgres psql

# RHEL 8
dnf install postgresql-server postgresql-contrib
postgresql-setup --initdb
systemctl start postgresql
sudo -u postgres psql
```

### Go Installation
```bash
# Ubuntu
apt install golang-go

# RHEL 8
dnf install golang
```

### Node.js Installation
```bash
# Ubuntu
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
apt install nodejs

# RHEL 8
dnf module enable nodejs:18
dnf install nodejs
```

### Common Directories
```bash
# Ubuntu                    # RHEL 8
/etc/apt/                  /etc/yum.repos.d/
/var/log/syslog           /var/log/messages
/etc/network/             /etc/sysconfig/network-scripts/
```

### SELinux (RHEL 8 Specific)
```bash
# Check SELinux status
getenforce

# Temporarily disable
setenforce 0

# Permanently disable (edit /etc/selinux/config)
SELINUX=disabled

# List SELinux contexts
ls -Z

# Change context
chcon -t httpd_sys_content_t /path/to/file
```

### Important Tips
1. RHEL 8 uses SELinux by default - learn basic SELinux commands
2. RHEL 8 uses podman instead of docker by default
3. RHEL 8 uses modules for managing multiple versions of packages
4. Always use official Red Hat repositories when possible
5. Keep documentation of all custom configurations
