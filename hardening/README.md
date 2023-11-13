# Hardening
Setting up a DHCP server for a 10.0.0.0/24 internal network. <br />

## Requirements
Although any of the commands and techniques here should work in any given moment of a Ubuntu 22.04 server, it is highly recommended to harden you server right after a fresh install.

## Checking services
Check which services are running on the host.
```bash
service --status-all | grep "[ + ]"
```

## Logs
The /var/log/ directory contains logs for different services. For example, checking the logs for auth:
```bash
cat /var/log/auth.log
```
To keep checking logs in real time, add tail -f:
```bash
sudo tail -f /var/log/syslog
```

## Checking for Rootkits
First, install a rookkit scanner, and then run it:
```bash
sudo apt install rkhunter -y && sudo rkhunter -c
```

## Manageging system access
First, let's make sure UID 0 is assigned to root. <br />
The expected output should be something like "root:x:0:0:root:/root"/bin/bash".
```bash
awk -F: '($3=="0"){print}' /etc/passwd
```
Second, let's check if all users have a password set.
The expected output should be ">".
```bash
cat /etc/shadow | awk -F: '($2==""){print
$1}’
```
We can also check which users are sudoers with visudo. This should open a text file the lists which users and groups may gain root privileges.
```bash
sudo visudo
```
If not sure about which users are part of a group, change user to the actual user you want to investigate:
```bash
groups marco
```

## Updating packages
It is always a good idea to have your packages up to date.
```bash
sudo apt update -y && sudo apt dist-upgrade -y && sudo apt upgrade -y
```
You may also want to check which packages you already have installed.
```bash
apt list -installed
```

## Securing SSH
It is a good practice to restrict who can access the machine with ssh. Changing the port, limiting it to IPv4, blocking sshing to root, and only allowing authentication with keys can be done by simply changing the sshd_config file.
```bash
sudo nano /etc/ssh/ssh_config
```

## Blocking unused ports
First, let's install ufw if it's not already there.
```bash
sudo apt install ufw -y
```
Now, let's add rules to allow only the ports your services use. You may need to read the documentation for the services you installed to verify which port it is using. And if you followed the previous (ssh) steps, remember to also allow the new ssh port.
```bash
sudo ufw allow 53 && sudo ufw allow 67 && sudo ufw allow 68 && sudo ufw allow 323 && sudo ufw allow 953
``` 
Remember to enable ufw as well.
```bash
sudo ufw enable
```