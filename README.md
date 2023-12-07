# Clean Install And Configure Debian Desktop

**add user**
```
sudo adduser anonymous
sudo usermod -aG sudo anonymous
su - anonymous
whoami
```

**add user as sudo**
```
su root
echo 'anonymous ALL=(ALL:ALL) ALL' >> /etc/sudoers
su - anonymous
```

**fix update sourcelist**
```
sudo vim /etc/apt/sources.list

deb http://deb.debian.org/debian/ bookworm main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main non-free-firmware

deb http://security.debian.org/debian-security/ bookworm-security main non-free-firmware
deb-src http://security.debian.org/debian-security/ bookworm-security main non-free-firmware

# bookworm-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debi ... _backports
deb http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main non-free-firmware 

:wq
```

**update and upgrade debian**
```
sudo apt update && sudo apt upgrade -y
```

**fix installation error because permission**
```
sudo chown -Rv _apt:root /var/cache/apt/archives/partial/
sudo chmod -Rv 700 /var/cache/apt/archives/partial/
```

**configure timezone**
```
sudo dpkg-reconfigure tzdata
```

**enable chrome remote desktop**
```
sudo apt install xfce4 xfce4-goodies -y

sudo wget https://dl.google.com/linux/direct/chrome-remote-desktop_current_amd64.deb
sudo apt install ./chrome-remote-desktop_current_amd64.deb -y

https://remotedesktop.google.com/access
```

**install guest addition virtual box**
```
sudo apt install build-essential dkms linux-headers-$(uname -r)
#mount vbox iso first
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run --nox11
sudo reboot
```

**install app**
```
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/dn.yarnpkg.com.gpg >/dev/null
sudo sh -c "echo deb https://dl.yarnpkg.com/debian stable main \
/etc/apt/sources.list.d/yarn.list"

sudo apt-get install yarn

wget -O chrome.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./chrome.deb

wget https://az764295.vo.msecnd.net/stable/6c3e3dba23e8fadc360aed75ce363ba185c49794/code_1.81.1-1691620686_amd64.deb
sudo apt install ./code_1.81.1-1691620686_amd64.deb

sudo apt install vim nodejs npm htop -y
```

**install nvidia driver**
```
su
echo 'deb http://deb.debian.org/debian/ sid main contrib non-free non-free-firmware' >> /etc/apt/sources.list
apt update
apt install nvidia-driver firmware-misc-nonfree
```
