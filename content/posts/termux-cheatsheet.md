---
title: "Termux Cheatsheet"
date: 2019-07-11T00:00:01+05:30
description: "MySQL cheatsheet contains almost everything I know about MySQL, It is great resource to learn new things about MySQL"
tags: [mysql]
---

**Termux** was very first program I installed after buying my first Android phone, it is the best Terminal emulator on Android with it's own repository which contains programs like ssh, php, nodejs, perl, etc. Here is a list of common commands and programs I keep in **Termux**

## Update packages and package index
```bash
pkg up
# or
apt update && apt upgrade
```

## Enable tab completion
```bash
pkg i bash-completion
# Restart may be required
```

## Enable Two Line Keyboard
```bash
echo "extra-keys = [['ESC','/','-','HOME','UP','END','PGUP'],['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN']]" >> .termux/termux.properties
```

## Enable spell correction for bash
It works for cd command, Add `shopt -s cdspell` to `.bashrc`
```bash
echo 'shopt -s cdspell' >> .bashrc
```

## Change prompt
Add this line to `.bashrc`
```bash
echo 'PS1="\[\033[1;30m\][\@] \[\033[1;37m\]Ravindra@Termux:\w $ \[\033[0;37m\]"' >> .bashrc
```
**NOTE**: Change `Ravindra@Termux` with your own name

## Disable start up banner
```bash
touch ~/.hushlogin
```

## Add welcome banner
```bash
pkg i figlet pv
echo 'figlet "Welcome Ravindra" | pv -qL 500' >> .bashrc
```
**NOTE**: Change `Welcome Ravindra` with your own name

## Install Aria
`aria2` is a command based download manager, it is faster than `curl`, `wget`. It has resume support, it can download torrent files and etc.
```bash
pkg i aria2

# To download a file
aria2 <url>
```

## Install Megatools
`megatools` allows us to download files form `mega.nz`, I like command version because it fast and very small in size but it doesn't have resume support.

```bash
pkg i megatools

# Download a url
megadl <url>
```

## Install Oh My ZSH
```bash
pkg i curl git zsh

# Just follow official guide after this
```
**NOTE: We can't set zsh as default, you can add a line in .bashrc to automatically start zsh but it is not a good idea for small devices**

## Install WFuzz
```bash
# Install dependencies
apt install python openssl curl clang libcrypt libcurl
export PYCURL_SSL_LIBRARY=openssl
pip install -U wfuzz
```

## Install TOR & TORSOCKS
```bash
pkg i torsocks
```
Edit config files
```bash
vim $PREFIX/etc/tor/torrc
```
- Add a new line `Socks5Proxy 127.0.0.1:9050`
- Start Tor: `tor`
- Stop Tor: Just CTRL + C, if you've used `tor&` then `pkill tor`
- Torify shell: `source torsocks on` and everything will route through tor.
- Stop torifing shell: `source torsocks off` and everything will fallback to normal behaviour.
- Using NMap: Always use TCP scan `nmap -sT blah blah blah` and don't run nmap as root.


## Check all open ports on your phone (Root required)
- Install `tsu`: `pkg i tsu`
- Type `tsu`
- Type `netstat -puntl` and it will list all open ports and programs using them.
- If you see something unfamilliar then you may be a victom of open port vulnerability.


## SSH
- Installation: `pkg i openssh`
- SSH client is ready, you can keep keys in $HOME/.ssh
- Server only supports SSH Key so go to `$HOME/.ssh`
    - Generate a new SSH Key pair: `ssh-keygen`
    - Add content of public key to `~/.ssh/authorized_keys`
    - Type `sshd` to start SSH server on port 8022
    - Connect from another system.


## PHP

PHP has MySQL support by default and postgres support can be added using packages, postgres and mysql database are available.

- Installation: `pkg i php`

    
## Install common programs

- 7z: `pkg i p7zip`
- C/C++ Compiler: `pkg i clang` GCC is not available anymore.
- FFMpeg: `pkg i ffmpeg`
- Git: `pkg i git`
- Hydra: `pkg i hydra`
- Nano: `pkg i nano`
- Nmap: `pkg i nmap`
- Node: `pkg i nodejs`
- SQLMap: `pkg i python && pip install -U sqlmap` 
- Vim: `pkg i vim` 
- Youtube-DL: `pkg i ffmpeg python && pip install -U youtube_dl`