# Homelab Documentation
A collection of write-ups following my journey into Linux and Windows security.

## Environment
I have ensured that my virtual machines are completely isolated from my LAN as well as setting up a firewall rule to drop packets to my host machine, making it air-tight.

I installed a manually-configured a minimalist installation of Gentoo Linux. I utilised the tools [QEMU](https://www.qemu.org/), [libvirt](https://libvirt.org/) and [virt-manager](https://virt-manager.org/) to create virtual machines for both a [Kali](https://www.kali.org/) Linux installation as the attacker, and a [Metasploitable 2](https://docs.rapid7.com/metasploit/metasploitable-2/) installation as the defender.  Unless otherwise specified, these are the two machines used in my experiments. 
