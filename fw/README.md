# Firewall
We will setup a firewall and setup a mask to our client's IP address. <br />
[Source](https://ubuntu.com/server/docs/security-firewall)

## Requirements
For this, we will use 2 interfaces on our server. One connected to the 172 network (with access to the internet), and the other interface for our internal network (and the client's gateway).

## Install
Let's first make sure ufw is installed.
```bash
sudo apt install ufw -y && sudo systemctl status ufw
```

## Blocking unused ports
Just like the hardening section, we will ensure to allow used ports only. For example:
```bash
sudo ufw allow 53 && sudo ufw allow 67 && sudo ufw allow 68 && sudo ufw allow 323 && sudo ufw allow 953
``` 
Remember to enable ufw as well.
```bash
sudo ufw enable
```

## Packet Forwarding
In this part, we will enabled packet forwarding. First, edit the ufw forward policy on `/etc/default/ufw`:
```bash
DEFAULT_FORWARD_POLICY="ACCEPT"
```

After that, uncomment the ip_forward line from the `/etc/ufw/sysctl.conf` file. You may also want to change the ipv6 forward line.:
```bash
net/ipv4/ip_forward=1
net/ipv6/conf/default/forwarding=1
```

## Nat tables
It is also necessary to edit the nat table rules, on the `/etc/ufw/before.rules` file.

```bash
# nat Table rules
*nat
:POSTROUTING ACCEPT [0:0]

-A POSTROUTING -s 10.0.0.0/24 -o enp0s3 -j MASQUERADE

COMMIT
```

Enable the new settings:
```bash
sudo ufw disable && sudo ufw enable && sudo sysctl -p
```

And issue this command, you may need to change the subnet and the output interface to match your server:
```bash
sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o enp0s3 -j MASQUERADE
```
