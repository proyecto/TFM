# TFM

## Configuration

### Create the VM

Created a virtual machine with IP 192.168.1.107 and installed ubuntu server 18.10, then updated the repos:

```
sudo apt-get update
sudo apt-get upgrade
```

### Configure Docker

Configure docker repository:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

Update the the repository information, install and init docker:

```bash
sudo apt-get update
sudo apt-get install -y docker-ce
systemctl start docker
systemctl enable docker
sudo usermod -a -G docker $USER
```

Now you have to reboot the system to apply the privileges change.

### Install Docker-Compose

We can install docker compose directly from ubuntu repository, but it is not the latest version. Though this command, you can install the latest version.

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Configure Portainer

Create a folder to store portainer data:

```bash
mkdir $HOME/data
sudo chmod -R 777 $HOME/data
docker volume create portainer_data
```

Deploy portainer:

```bash
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/home/ubuntu/data portainer/portainer
```

Create the user, and connect to the local docker instance.

### Deploy ELK Stack

Due to the version at the current portainer docker (1.22.2), and the docker-compose it has installed, we should launch the ELK Stack from console. SSH to the Docker host, clone this repo, and run:

```bash
cd /path.to.repo/TFM/elk
docker-compose up -d
```

We can monitor the status of the ELK containers at portainer.

### Deploy Filebeat

### Deploy Packetbeat

### Deploy service containers

Deployed a nginx container just to generate logs and test