# Docker and Docker Compose installation on Raspberry Pi

## Info

Installation instructions for installing docker and docker-compose on Raspberry Pi.

Command instructions are from the guides below:  
[docker](https://docs.docker.com/engine/install/debian/)  
[docker-compose](https://docs.docker.com/compose/install/)

## docker

Remove any possible old versions of docker:

    sudo apt-get remove docker docker-engine docker.io containerd runc

Install dependencies:

    sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

Get docker repository key:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

Add docker repo to apt-get:

    echo "deb [arch=arm64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Update apt-get from repository:

    sudo apt-get update

Install docker:

    sudo apt-get install docker-ce docker-ce-cli containerd.io

Create user group for docker incase it doesn't already exist:

    sudo groupadd docker

Add current user to docker group so no need to "sudo" docker:

    sudo usermod -aG docker $USER


## docker-compose

Download docker-compose executable:

    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

This might not work so you may need to install using apt:

    sudo apt install docker-compose

Apply executable persmissions to the binary:

    sudo chmod +x /usr/local/bin/docker-compose
