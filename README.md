\# SSH Remote Server Setup

This project is part of the \[roadmap.sh](https://roadmap.sh/projects/ssh-remote-server-setup) Linux administration track. The goal was to set up a remote Linux server, configure secure SSH key-based authentication, and implement basic security hardening.

\## Project Overview

In this project, I configured an Ubuntu Server (running on a VirtualBox VM) to be managed remotely from a Windows host machine. I replaced traditional password authentication with secure SSH key pairs and optimized the connection process using an SSH configuration file.

\##  Features \& Steps

\### 1. SSH Key Generation

I generated two separate SSH key pairs using the modern and secure \*\*Ed25519\*\* algorithm to fulfill the requirement of having multiple access keys.

```bash

ssh-keygen -t ###### -f ~/.ssh/projet\_linux\_1

ssh-keygen -t ###### -f ~/.ssh/projet\_linux\_2

\## 2. IMPORTANT 

Since the ssh-copy-id command is not natively available on Windows PowerShell, I manually deployed the public key to the server using the following command: type $HOME\\.ssh\\projet\_linux\_1.pub | ssh user@server-ip "mkdir -p ~/.ssh \&\& cat >> ~/.ssh/authorized\_keys"

\## 3. SSH Configuration (Alias)

To simplify the connection process, I created an SSH config file located at ~/.ssh/config on the host machine. This allows me to connect using a simple alias instead of remembering the IP address and identity file path.

Host serveur-projet

    HostName 000.000.000.000

    User txt

    IdentityFile ~/.ssh/projet\_linux\_1

\## 4. Security Hardening (Fail2ban)

As a stretch goal, I installed and configured Fail2ban on the Ubuntu server to protect against brute-force attacks.
Installation: sudo apt install fail2ban

Status: Verified as active (running) to monitor failed login attempts.

\## 5. How to Connect

After the setup, connecting to the server is as simple as running: ssh serveur-projet
