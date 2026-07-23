# Objective
Perform the classic backdoor on vsftpd, on open port 21 to give me an open shell on port 6200.

## Environment
Isolated labnet. See README.md.

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
