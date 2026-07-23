# Objective
Perform the classic backdoor on vsftpd, on open port 21 to give me an open shell on port 6200.

# Set-Up Mistakes
After creating a snapshot of my fresh installs I wanted to change my VM IPs to something more memorable: 10.0.0.11 and 10.0.0.12. However, this did not work due to the fact my host supported the ranger 192.168.100.1 to 192.168.100.255.
This meant I was not correctly isolating my host from my VMs. While my LAN was isolated, I wanted it to be air-tight. After quickly realising my mistake I reverted back and proceeded with the experiment.

# My Firewall
To ensure my host machine could not be reached by the VMs, I used [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) to create a rule that drops all traffic to my host. With 8.8.8.8 being unreachable,
100% packet loss to my host, and the VMs able to ping each other, I was satisfied.

# Methodology
While initially I was very quickly able to use the metasploit framework to quickly run the necessary commands, I was not satisfied. I attempted this simple exploit by hand.
nmap -sV, netcat <ip>, put a ':)' at the end of a random username followed by a random password, created a new shell and entered 'id' to confirm root access.

# Commands Reference
### Firewall
- `doas nano /etc/conf.d/libvirtd` changed: rc_need="" so that libvirtd can run without internet
- `doas nft list ruleset`
- `doas nft list table ip libvirt_network`
- `doas nft add rule ip libvirt_network guest_input iifname "virbr1" drop`

### Exploit
-`nmap -sV`
-`netcat`
