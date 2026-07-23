# Homelab Documentation
A collection of write-ups following my journey into Linux and Windows security.

## Environment
___All lab activity happens on my isolated network with no path to any shared network OR access to the host machine.___

I installed a manually-configured a minimalist installation of Gentoo Linux. I utilised the tools [QEMU](https://www.qemu.org/), [libvirt](https://libvirt.org/) and [virt-manager](https://virt-manager.org/) to create virtual machines for both a [Kali](https://www.kali.org/) Linux installation as the attacker, and a [Metasploitable 2](https://docs.rapid7.com/metasploit/metasploitable-2/) installation as the defender.

I have ensured that my virtual machines are completely isolated from my LAN using a custom labnet profile with no forwarding/NAT.
To ensure my host machine could not be reached by the VMs, I used [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) to create a rule that drops all traffic to my host.
