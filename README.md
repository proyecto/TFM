# TFM

## Configuration

### Create the VM

Created a virtual machine with IP 192.168.1.107 and installed ubuntu server 18.04, then updated the repos:

```
sudo apt-get update
sudo apt-get upgrade
```

### Configure Docker

Configure docker repository:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

Update the the repository information, install and init docker:

```bash
sudo apt-get update
sudo apt-get install -y docker-ce
sudo apt-get install docker-compose
systemctl start docker
systemctl enable docker
sudo usermod -a -G docker $USER
```

### Configure Portainer

Create a folder to store portainer data:

```bash
mkdir /home/ubuntu/data
docker volume create portainer_data
```

Initialize portainer:

```bash
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

### Deploy ELK Stack

### Deploy Filebeat

### Deploy Packetbeat

### Deploy service containers

Deployed a nginx container just to generate logs and test