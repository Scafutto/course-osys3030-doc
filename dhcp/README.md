# DHCP
Setting up a DHCP server for a 10.0.0.0/24 internal network. <br />
[Source](https://ubuntu.com/server/docs/how-to-install-and-configure-isc-dhcp-server)

## Requirements
A new network adaptor should be used for that. In this case, >>>> INTERFACE <<<<.  was added as an internal adaptor by edditing the VM settings.

## Install
To install isc-dhcp-server, simply run the command:
```bash
sudo apt install isc-dhcp-server -y
```

## Configuration
To start cofngiuring our DHCP service, let's first edit our config file.
```bash
sudo nano /etc/dhcp/dhcpd.conf
```
>>>> MISSING THE OTHER FILES <<<<

Restart the service to apply the new configuration
```bash
sudo systemctl restart isc-dhcp-server.service
```

## Test
On our Client machine, edit the netplan file. The file should be in /etc/netplan/ <br />

The file should look like this

```console
marco@ubuntusv:~$ cat /etc/netplan/ ?????????
REST OF IT HERE
```
