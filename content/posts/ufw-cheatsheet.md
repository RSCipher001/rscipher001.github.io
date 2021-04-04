+++
categories = ["firewall", "ufw"]
date = "2021-04-04"
description = "UFW cheatsheet to help you with setting up Ubuntu server"
title = "UFW Cheatsheet"
+++

UFW cheatsheet

### Installation

```bash
sudo apt install ufw
```

GUI version

```bash
sudo apt install gufw
```

## Enable firewall

```bash
sudo ufw enable
```

### Check rules & status

```bash
sudo ufw status
sudo ufw status verbose
```

### Allow applications

```bash
sudo ufw allow ssh            # Allow SSH port 22

sudo ufw allow http           # Allow web server port 80
sudo ufw allow https          # Allow web server port 443

sudo ufw allow 4444           # Allow port 4444
sudo ufw allow 4444/tcp       # Allow port 4444 TCP only
sudo ufw allow 4444/udp       # Allow port 4444 UDP only

sudo ufw allow 1714:1764/udp  # Allow Port From 1714 to 1764 UDP
sudo ufw allow 1714:1764/udp  # Allow Port From 1714 to 1764 TCP
```

**Note:** Refer to `/etc/services` for all services <br>
**Note:** Port range doesn't supprot both TCP and UDP at once.

### Remove allowed applications

```bash
sudo ufw delete allow ssh     # Remove Allow SSH Entry
```

**Note:** After removing an entry firewall will use default rules for that port,default rule is deny incoming.


### Reload firewall
```bash
sudo ufw reload
```


## Other Resources
- [UFW - Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/firewall.html) <br>
- [UFW - Ubuntu Community](https://help.ubuntu.com/community/UFW) <br>
- [UFW - Ubuntu Wiki](https://wiki.ubuntu.com/UncomplicatedFirewall) <br>
- [UFW Essentials - Digital Ocean](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands) <br>
- [UFW - Wikipedia](https://en.wikipedia.org/wiki/Uncomplicated_Firewall)
