# DNS - BIND9
Setting up a DNS server with Bind9, this DNS server should resolve requests to a fictional TLD named sysninja.

## Requirements
We will only need to our Client DNS IP to the server IP (for the same network). This could be done with DHCP (recommended), or manually.

## Install
Install bind9 and other useful packages.
```bash
sudo apt install bind9 bind9utils bind9-doc -y
```
Check if the installation was succesfully by checking the status, it should be `active`.
```bash
sudo systemctl status bind9
```

## Configuration
To start cofngiuring our DNS service, let's first copy the original files to its own directory.
```bash
sudo mkdir /etc/bind/original && sudo cp /etc/bind/named.conf.options /etc/bind/named.conf.options.original /etc/bind/original/
```

Now let's configure the files. Starting from `/etc/bind/named.conf.options`.
```bash
FILE HERE
```

Now, let's configure `/etc/bind/named.conf.local`.
```bash
FILE HERE
```



THE REST











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
The expected output should be something like `root:x:0:0:root:/root"/bin/bash`.
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