# Objective
Perform the classic backdoor on vsftpd, on open port 21 to give me an open shell on port 6200.

## Environment
I have ensured that my virtual machines are completely isolated from my LAN as well as setting up a firewall rule to drop packets to my host machine, making it air-tight.

I installed a manually-configured a minimalist installation of Gentoo Linux. I utilised the tools [QEMU](https://www.qemu.org/), [libvirt](https://libvirt.org/) and [virt-manager](https://virt-manager.org/) to create virtual machines for both a [Kali](https://www.kali.org/) Linux installation as the attacker, and a [Metasploitable 2](https://docs.rapid7.com/metasploit/metasploitable-2/) installation as the defender.

To ensure my host machine could not be reached by the VMs, I used [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) to create a rule that drops all traffic to my host. With 8.8.8.8 being unreachable,
100% packet loss to my host, and the VMs able to ping each other, I was satisfied.

## Methodology
While initially I was very quickly able to use the metasploit framework to quickly run the necessary commands, I was not satisfied. I attempted this simple exploit by hand.
nmap -sV, netcat <ip>, put a ':)' at the end of a random username followed by a random password, created a new shell and entered 'id' to confirm root access.

## Commands Reference
### Firewall
- `doas nano /etc/conf.d/libvirtd` changed: rc_need="" so that libvirtd can run without internet
- `doas nft list ruleset`
- `doas nft list table ip libvirt_network`
- `doas nft add rule ip libvirt_network guest_input iifname "virbr1" drop`

### Exploit
- `nmap -sV`
- `netcat`
