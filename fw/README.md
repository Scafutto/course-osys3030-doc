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
In this part, we will enabled packet forwarding. First, edit the ufw forward policy to `DEFAULT_FORWARD_POLICY="ACCEPT"`:
```bash
sudo nano /etc/default/ufw
```

After that, uncomment the ip_forward line from the sysctl.conf file `net/ipv4/ip_forward=1`. You may also want to change the ipv6 forward line.:
```bash
sudo nano /etc/ufw/sysctl.conf
```

## Nat tables
It is also necessary to edit the nat table rules, on the /`etc/ufw.before.rules` file.

```bash
NAT TABLE RULES HERE
```

Enable the new settings:
```bash
sudo ufw disable && sudo ufw enable && sudo sysctl -p
```

And issue this command:
```bash
sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o INTERFACEHEREEEEEEEEEEEEEEEEEEEEEEEEEE -j MASQUERADE
```
