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