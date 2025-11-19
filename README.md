# Overview
BlackBox is a complete Ansible playbook that transforms a fresh Arch Linux installation into a complete security research workstation. Everything is optimized for security work.
## Key Feature
- 🎨 Minimal UI: Sway (Wayland) with true black Gruvbox theme, ultra-minimal Waybar
- 🔒 Hardened: Mac randomizer, UFW firewall, AppArmor, kernel hardening
- 🛠️ Tools: BlackArch repository (2800+ tools), essential security packages
- 🖥️ Virtualization: KVM/QEMU with 3 isolated networks for lab environments
- 🐳 Containers: Docker with pre-configured vulnerable applications
- ⚡ Automation: VPN management, HTB/THM workflows, lab scripts

---

# Quick Start
## Prerequisites
1. Fresh Arch Linux installation with:
- Full disk encryption (LUKS2)
- Base system + base-devel

2. Install Ansible
```bash
sudo pacman -S ansible git
```

3. Run the playbook
```bash
# Clone the repository
git clone https://github.com/yourusername/blackbox.git
cd blackbox
# Review configuration
nvim group_vars/all.yml
# Run complete setup
ansible-playbook -i inventory/localhost.ini playbooks/main.yml --ask-become-pass
```

4. First boot
```bash
# Reboot
sudo reboot
# Login and start Sway
sway
# Run security check
lab-check
# Connect to HTB/THM
htb start
```

---

# What Gets Installed
**Desktop Environment**
- Sway - Wayland compositor
- Waybar - Status bar (minimal, true black)
- Alacritty - Terminal (GPU-accelerated)
- Wofi - Application launcher
- Mako - Notification daemon
- Zsh - Shell with Oh My Zsh + Powerlevel10k

**Security & Hardening**
- UFW - Firewall (deny incoming, allow outgoing)
- AppArmor - Mandatory Access Control
- Audit - System auditing
- Kernel hardening - Sysctl parameters
- MAC randomization - Network privacy
- DNS - Cloudflare 1.1.1.1

**Tools & Repositories**
- BlackArch - 2800+ security tools
- Essential tools: nmap, burp, metasploit, wireshark, hashcat, john, hydra
- Virtualization: KVM, QEMU, libvirt, virt-manager
- Containers: Docker with DVWA, Juice Shop, WebGoat

**Lab Infrastructure**
3 VM Networks:
- isolated (192.168.100.0/24) - No internet, malware analysis
- pentest (10.10.10.0/24) - VPN-routed, offensive ops
- defensive (10.20.20.0/24) - NAT, blue team monitoring

**Automation & Scripts**
- VPN management (HTB/THM)
- HTB machine workspace creator
- Pre-operation security checks
- Docker lab management
- System health monitoring
- Session logging

---

# Key Commands
**Security & VPN**
```bash
lab-check           # Pre-operation security check
htb start           # Connect to HackTheBox
thm start           # Connect to TryHackMe
vpncheck            # Check VPN status
fwstatus            # Firewall status
```

**HTB/THM Workflow**
```bash
htb-machine Lame 10.10.10.3  # Setup HTB machine workspace
cd ~/HTB/Active/Lame          # Navigate to workspace
qscan $TARGET                 # Quick nmap scan
set-target 10.10.10.3         # Set target variable
```

**Virtualization**
```bash
vms                          # List all VMs
vm-start kali                # Start VM
vm-stop kali                 # Stop VM
create-vm name network ram   # Create new VM
virt-viewer kali             # Connect to VM console
```

**Docker Lab**
```bash
dlab start                   # Start vulnerable apps
dlab stop                    # Stop lab
dlab status                  # Show status

# Access apps at:
# DVWA:       http://localhost:8080
# Juice Shop: http://localhost:3000
# WebGoat:    http://localhost:8081
```

**System**
```bash
system-health               # Full system status
lab-manage start            # Start lab environment
lab-manage stop             # Stop all VMs/containers
```

---

# Customization
Edit `group_vars/all.yml` :

**Change Theme Colors**
```yml
gruvbox:
  bg_hard: "#000000"    # Pure black
  fg: "#ebdbb2"         # Beige text
  blue: "#458588"       # Accent color
```

**Add Custom Tools**
```yml
security_tools:
  - nmap
  - your-custom-tool
```

**Modify Networks**
```yml
vm_networks:
  - name: mynetwork
    ip: 10.50.50.1
    netmask: 255.255.255.0
```

---

# Post-Installation
1. Set Up VPNs
Download your VPN configs:
- HTB: https://www.hackthebox.com/home/htb/access
- THM: https://tryhackme.com/access

Save to:
```bash
~/cyber-lab/vpn/htb.ovpn
~/cyber-lab/vpn/thm.ovpn
```

2. Install AUR Helper
```bash
cd /tmp
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

3. Install Additional Tools
```bash
paru -S burpsuite obsidian librewolf-bin
```

4. Install VM ISOs
```bash
mkdir -p ~/Downloads/ISOs
# Download Kali, Metasploitable, Windows, etc.
```

---

# To-Dos:

**High Priority**
- [ ] **Dotfiles Management**
- [ ] Implement GNU Stow
- [ ] Create dotfiles repository
- [ ] Add sync script
- [ ] Version control all configs

- [ ] **Automated Backups**
- [ ] Borg backup integration
- [ ] Systemd timer for daily backups
- [ ] External drive mounting
- [ ] Backup verification script

- [ ] **Neovim Configuration**
- [ ] LSP support (Python, Bash, YAML)
- [ ] Syntax highlighting for all languages
- [ ] Gruvbox theme integration
- [ ] Security-focused plugins

**Medium Priority**
- [ ] **Tmux Configuration**
- [ ] Gruvbox theme
- [ ] Session management scripts
- [ ] Automatic session restoration
- [ ] Lab-specific layouts

- [ ] **VM Template Automation**
- [ ] Pre-configured VM images
- [ ] Automated VM creation
- [ ] Network auto-assignment
- [ ] Snapshot management

- [ ] **Password Manager**
- [ ] KeePassXC setup
- [ ] SSH key management

**Low Priority**
- [ ] **Browser Hardening**
- [ ] Firefox configuration
- [ ] Extension installation (FoxyProxy, Wappalyzer)
- [ ] Certificate management

**Multi-Host Support**
- [ ] Support for multiple machines
- [ ] Different profiles (laptop, desktop, VM)

