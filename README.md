With this repository you can easily install your own node as an alternative to using opago's node as a service. Tested with a minimal Debian 11 install. The intended use is for running this in clearnet hybrid mode, with a domain and apropriate subdomains available. This is a work in progresss, so use with care.

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
sudo usermod -aG docker $USER
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
# Adjust node configs
## Domains
change domains  in docker-compose to your own domain, make sure that the subdomains are created and pointed to your node's host ip
```
nano docker-compose.yml
```
## lnd.conf
change domains, tor password etc in lnd.conf
```
nano ./lnd/lnd.conf
```
## lnd password
```
nano ./lnd/password.txt
```
# First Startup
## Tor
Hash your tor password, replace "password" with your password from the lnd.conf
```
docker-compose up -d
docker exec -it tor tor --hash-password password
```
Copy the hash the above command returns and add it to your torrc.default
```
nano ./tor/torrc.default
docker restart tor
```
## LND
It's really important that you set the same password here as in the password.txt and that you store the 24 words returned by the command. Without these you cannot recover your wallet if anything goes wrong.
```
docker exec -it lnd lncli create
```
# Run Node
```
docker-compose up -d
```
# Check container status, replace btc with the container you want to check
```
docker logs -f btc
```
# Stop Node
```
docker-compose down
```
# Build
If you don't want to use our docker containers, you can build them yourself. To do so cd into each build directory and run the docker build command with your desired tag, example below
```
docker build -t opago/bitcoin:latest .
docker push opago/bitcoin:latest
```
Then change the images in docker-compose.yml to your image tag.
P.S. If you are not logged into the docker repo that you are trying to build for, the push command will give you an error. You can solve this by running.  
```
docker login
```
