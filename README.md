# osys3030-doc
Documentation for OSYS 3030

## The Server
This server was created for the sole purpose of this class. It only contains the packages described in this documentation, besides the ones that come with the fresh install. <br />

**Interfaces** <br />
enp0s3 - Has access to the internet <br />
enp0s8 - Internal network interface <br />

**Specifications** <br />
Operating System: Ubuntu 22.04 (Jammy) server <br />
Virtualization Platform: VirtualBox <br />
RAM: 2 GB <br />
Processor: 1 <br />
Cores: 1 <br />
Storage: 20 GB

## Hardening
Quick techniques to make a fresh install server a bit more secure, using a bit of services, logs, restricting system access, blocking unused ports/services and keeping packages updated.

## DNS - BIND9
Basic DNS configuration for a fictional tld (sysninja), using bind9.

## DHCP - ISC DHCP SERVER
Setting up a DHCP server for the internal network, using isc-dhcp-server.

## FW
Enabling packet forwarding and a few iptable rules to grant access to the internet to our Client host, and hiding its IP.

## SQUID
Transparent proxy for our clients with squid! This is an amazing and widely-used tool for caching proxy purposes.
