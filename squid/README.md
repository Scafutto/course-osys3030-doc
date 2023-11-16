# Squid
We will use Squid to set a transparent proxy server to our clients. <br />
[Source](https://ubuntu.com/server/docs/how-to-install-a-squid-server)

## Install
Simply install squid:
```bash
sudo apt install squid -y
```

## Configuration
First, let's copy the original config file:
```bash
sudo cp /etc/squid/squid.conf /etc/squid/squid.conf.original
```

For this example, the only changes made was the visible_hostname, the acl name and source network, and allowing that acl, all that on `squid.conf`, the rest was kept default. That was added right after the first commented block (introduction):
```
visible_hostname squido
acl linuxClass src 10.0.0.0/24
http_access allow linuxClass
```

Finally, restart squid and you shuld be good to go:
```bash
sudo systemctl restart squid.service
```

Remeber to add any ufw rule, if necessary, in our case, we will allow port 3128 (squid's default port):
```bash
sudo ufw allow 3128
```