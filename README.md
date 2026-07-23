# Homelab Documentation
A collection of write-ups following my journey into Linux and Windows security.

## Environment
___All lab activity happens on my isolated network with no path to any shared network or access to the host machine.___

I installed a manually-configured, minimalist installation of Gentoo Linux. I utilised the tools [QEMU](https://www.qemu.org/), [libvirt](https://libvirt.org/) and [virt-manager](https://virt-manager.org/) to create virtual machines for both a [Kali](https://www.kali.org/) Linux installation as the attacker, and a [Metasploitable 2](https://docs.rapid7.com/metasploit/metasploitable-2/) installation as the target.

My virtual machines are fully isolated from my LAN using a custom labnet profile with no forwarding/NAT configured.
To prevent the VMs from reaching my host machine, I used [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) to create a rule that drops all incoming traffic arriving from the labnet bridge interface at the host.

The above was verified via ping test: VM-to-VM communication succeeds, internet traffic is unreachable (ping 8.8.8.8 fails, no route), and host traffic is dropped (route exists, packets discarded).

### Command Reference
- `doas nano /etc/conf.d/libvirtd` changed: rc_need="" so that libvirtd no longer requires internet to run
- `doas nft list ruleset`
- `doas nft list table ip libvirt_network`
- `doas nft add rule ip libvirt_network guest_input iifname "virbr1" drop`
