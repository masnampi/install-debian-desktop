# Clean Install And Configure Debian Desktop

**update and upgrade debian**
```
sudo apt update && sudo apt upgrade -y
```

**fix installation error because permission**
```
sudo chown -Rv _apt:root /var/cache/apt/archives/partial/
sudo chmod -Rv 700 /var/cache/apt/archives/partial/
```

**install guest addition virtual box**
```
sudo apt install build-essential dkms linux-headers-$(uname -r)
mount lewat menu isonya
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run --nox11
sudo reboot
```

**add user**
```
adduser anonymous
usermod -aG sudo anonymous
su - anonymous
whoami
```

**add user as sudo**
```
su root
echo 'anonymous ALL=(ALL:ALL) ALL' >> /etc/sudoers
su - anonymous
```

**configure timezone**
```
sudo dpkg-reconfigure tzdata
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

sudo apt install vim nodejs npm htop
```
