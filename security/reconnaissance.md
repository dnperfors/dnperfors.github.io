Here I describe some techniques I use for reconnaissance work when I play a CTF. I don't think these are the best ways of doing things, but it does work for me.

## network enumeration

### arp-scan

For simply scanning all devices on a local network (i.e. a virtual network for a CTF), I use arp-scan:

```
root@kali:~# arp-scan -l
Interface: eth0, datalink type: EN10MB (Ethernet)
Starting arp-scan 1.9.5 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.56.1    0a:00:27:00:00:0f  (Unknown)
192.168.56.100  08:00:27:83:b6:24  Cadmus Computer Systems
192.168.56.101  08:00:27:45:3f:7e  Cadmus Computer Systems
```

Finding out the IP of the target machine is trivial:
- We can assume that 192.168.56.1 is used for the host system (this is an host-only network), running a nmap scan on this host would confirm that
- We know from the dhcp lease file that 192.168.56.100 is the DHCP server
- So 192.168.56.101 should be the target machine

### sparta

[Sparta](https://github.com/SECFORCE/sparta) is an easy to use Network Infrastructure Penetration Testing Tool, that basically automates running nmap, nikto and several other tools. The tool has a graphical user interface, so I can't show any commands here.

### nmap

For portscanning and OS detection I use Nmap. Since the scans I perform are on an internal virtual network, I can use the following command:

```
root@kali:~# nmap -v -A -T5 -p 1-65535 192.168.56.101
```
This takes some time, but will give some results in the end.

### nikto

For simple web application scanner, nikto is my first choice.

```
root@kali:~# nikto --host 192.168.56.101
```

## Local enumeration

A great source for local enumeration can be found on https://pinkysplanet.net/nix-enumeration/