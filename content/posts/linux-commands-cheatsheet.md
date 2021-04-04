+++
categories = ["linux", "shell", "bash"]
date = "2021-04-04"
description = "Linux CLI Cheatsheet"
title = "Linux CLI Cheatsheet"
+++


### Base64 encode
```bash
echo -ne "Text to encode" | base64
```

### Base64 decode
```bash
echo VGV4dCB0byBlbmNvZGU= | base64 -d
```

or

```bash
echo VGV4dCB0byBlbmNvZGU= | base64 --decode
```

### Bruteforce Form without Login

```bash
hydra -l '' -P /media/ravindra/Files/Computer_Science/GitHub/SecLists/Passwords/Leaked-Databases/rockyou-75.txt docker.hackthebox.eu http-post-form "/:username=^USER^&password=^PASS^:Invalid password" -s 35805
```

### Remove Empty Lines
```bash
sed '/^:space:*$/d'
```

### Find and replace in one file.
```bash
sed -i -e 's/foo/bar/g'
```

### Find and replace in many file.
```bash
cd /path/to/your/folder
sed -i 's/foo/bar/g' *
```

### Find Commands Examples.

### Optimize all jpeg files in current folder and subfolers

```bash
find . -type f -name "*.jp*g" -exec jpegoptim {} \;
```

```bash
find . -iname "*.jp*g"
```
- `.:` current directory
- `-iname:` name case-insensitive

```bash
find . -type d
```
- `-type:` d= direcotory, f=files

```bash
find . -type f -perm 777
```
- `-perm:` octal permission


### MySQL login without root
Access MySQL Shell: `sudo mysql -u root`

```sql
drop user 'root'@'localhost';
create user 'root'@'%' identified by 'password';
grant all privileges on *.* to 'root'@'%' with grant option;
flush privileges;
```


### Some Bash Stuff
#### Using \#
- As character counter
```bash
myname="Ravindra Sisodia"
echo "$myname is ${#myname} characters long"
```

- In base conversion
```bash
echo $(( 2#100 ))		# 4
echo $(( 8#100 ))		# 64		
echo $(( 10#100 ))		# 100
echo $(( 16#100 ))		# 256
```

# Using ,
- For case conversion
```bash
foo="ONEtwo"
echo ${foo,}	# oNEtwo
echo ${foo,,}	# onetwo
```

### Youtube-dl
```bash
youtubel-dl <youtube-link>			# Download max quality.
youtubel-dl -F <youtube-link>		# List all available qualities.
youtubel-dl -f 22 <youtube-link>	# Select one from the list.
```

# Swap related stuff
## Check Swappiness
```bash
cat /proc/sys/vm/swappiness
```

## Change Temporary
```bash
sudo sysctl vm.swappiness=10
```
## Change Permanent
```bash
sudo vim /etc/sysctl.conf
```
Add this line in the end
```
vm.swappiness=10
```

## Load changes from file
```bash
sudo sysctl --load=/etc/sysctl.conf
```

## Change file watcher limit
```bash
sudo vim /etc/sysctl.conf
# Add following line
fs.inotify.max_user_watches = 524288
```

## Turn of Swap
```bash
sudo swapoff -a
```

## Turn on swap
```bash
sudo swapon -a
```

## Enable Noise Cancallation
Open `/etc/pulse/default.pa`

```bash
sudo vim /etc/pulse/default.pa
```

Add the following lines

```
### Enable Echo/Noise-Cancelation
load-module module-echo-cancel aec_method=webrtc aec_args="analog_gain_control=0 digital_gain_control=1" source_name=echoCancel_source sink_name=echoCancel_sink
set-default-source echoCancel_source
set-default-sink echoCancel_sink
```

Restart PulseAudio
```bash
pulseaudio -k
pulseaudio --start
```

# Zip Current Folder
```bash
# This will create a foo.zip containing everything from current folder.
zip -r foo.zip .
```