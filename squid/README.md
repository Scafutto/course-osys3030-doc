# Squid
We will use Squid to . <br />
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



----------
Configure the ACL to work with our network
```bash
acl fortytwo_network src 10.0.0.0/24
```


---------
WHAT TO DO HERE???????






Finally, restart squid:
```bash
sudo systemctl restart squid.service
```