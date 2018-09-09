In order to savely run vulnerable boxes, I use virtual machines on top of VirtualBox.

## Installing Kali Linux

Kali linux is my distribution of choice when it comes to penetration testing and setting it up in VirtualBox is as simple as downloading a [premade box](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/).

## Choosing the right virtual network 

VirtualBox supports several type of [virtual networks](https://www.virtualbox.org/manual/ch06.html) and each have their advantages and disadvantages. But to be secure, vulnerable boxes should not be directly accessible by your normal network, therefore you will have the following options:

* NAT
* Internal networking
* Host-only networking

I tried all three networks with Mr. Robot. With Internal networking, the VM of Mr. Robot didn't even start.
Using NAT, there where in total 5 hosts visible, although I used only two VM's, one was probably my host, another would have been the DHCP server, but the 5th I couldn't really find out.
With Host-only I could see in total 4 hosts, 1 of my host machine, 1 dhcp server and two vm's, this makes it easy to identify which host is my target host.

So for now I stick to Host-only when performing pentests on virtual machines.

Ultimately I want to be able to connect my Kali box to a NAT network and an internal or host-only network so that I can keep it up to date, but for reasons unkown to me, I can only activate a single network card.