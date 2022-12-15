With this repository you can easily install your own node as an alternative to using opag's node as a service.

# Prepare node installation
## install ufw as firewall and fail2ban for ssh bruteforce protection
sudo apt install ufw
sudo apt install curl
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 9050
sudo ufw enable
sudo apt install fail2ban

## install docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker
newgrp docker
### test docker installation
docker run hello-world
## install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
