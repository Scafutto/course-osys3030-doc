# DHCP
Setting up a DHCP server for a 10.0.0.0/24 internal network. <br />
[Source](https://ubuntu.com/server/docs/how-to-install-and-configure-isc-dhcp-server)

## Requirements
A new network adaptor should be used for that. In this case, enp0s8.  was added as an internal adaptor by editting the VM settings.

## Install
To install isc-dhcp-server, simply run the command:
```bash
sudo apt install isc-dhcp-server -y
```

## Configuration
To start cofngiuring our DHCP service, let's first edit our config file `sudo nano /etc/dhcp/dhcpd.conf`:
```bash
default-lease-time 600;
max-lease-time 7200;

subnet 10.0.0.0 netmask 255.255.255.0 {
        range 10.0.0.1 10.0.0.100;
        range 10.0.0.201 10.0.0.215;
        option routers 10.0.0.250;
        option domain-name-servers 10.0.0.250;
}
```

We should also change the interface that DHCP should listen to, at `/etc/default/isc-dhcp-server`:
```bash
INTERFACESv4="enp0s8"
```

Restart the service to apply the new configuration
```bash
sudo systemctl restart isc-dhcp-server.service
```

## Test
On our Client machine, edit the netplan file. The file should be in `/etc/netplan/00-installer-config.yaml` <br />

The file should look like this

```bash
network:
  ethernets:
    enp0s3:
      dhcp4: true
  version: 2
```

Apply the changes and enjoy your new IP:
```bash
sudo netplan apply
```