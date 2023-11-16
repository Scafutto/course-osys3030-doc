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
options {
        directory "/var/cache/bind";
        forwarders {
                8.8.8.8;
                8.8.4.4;
        };
};
```

Now, let's configure `/etc/bind/named.conf.local`.
```bash
zone "sysninja" {
    type master;
    file "/etc/bind/db.sysninja";
};
```

Create a new file for our records:
```bash
mkdir /etc/bind/db.sysninja
```
Finally, let's add the records to our DNS server at `/etc/bind/db.sysninja`:
```bash
$TTL 86400
@       IN      SOA     sysninja. root.sysninja. (
                2               ; Serial
                3600            ; Refresh
                1800            ; Retry
                604800          ; Expire
                86400 )         ; Minimum TTL

; NS Records
@       IN      NS      ns1.sysninja.
; A Records
@       IN      A       10.0.0.100
*       IN      A       10.0.0.100
; TXT Records
*       IN      TXT     ccLcw6J4v7SGdM2ZhzHBoyFdbVvKh6oGQLQQSEzC4vivBUz35Qz6KVUi6PGSAPJfVH7bNEMpACrKk
; SPF Records
*       IN      TXT     "v=spf1 include:_spf.google.com ~all"
```