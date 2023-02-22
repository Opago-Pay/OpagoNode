With this repository you can easily install your own node as an alternative to using opag's node as a service. Tested with a mininal Debian 11 install. This is a work in progresss, so use with care.

# Prepare node installation
## install ufw as firewall and fail2ban for ssh bruteforce protection and other packages
```
sudo apt update
sudo apt install -y ufw curl nano git fail2ban
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 9735
sudo ufw enable
```
## disable ipv6
change IPV6=yes to IPV6=no
```
sudo nano /etc/default/ufw
```
## install docker
```
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker
newgrp docker
```
### test docker installation
```
docker run hello-world
```
## install docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

# Installation
## clone this repository
```
git clone https://github.com/Opago-Pay/OpagoNode/
cd OpagoNode
```
# change rcp password from "password" to your password (same in both the btc and cln section) and node alias from "alias" to your alias
```
nano docker-compose.yml
```
# Run Node
```
docker-compose up -d
```
