# TFM

## Configuration

### Create the VM

created a virtual machine with IP 192.168.1.107
Installed ubuntu server 18.04
sudo apt-get update
sudo apt-get upgrade

### Configure Docker

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
sudo apt-get install docker-compose
systemctl start docker
systemctl enable docker

### Initialize Swarm

sudo docker swarm init

### Configure Portainer

curl -L https://downloads.portainer.io/portainer-agent-stack.yml -o portainer-agent-stack.yml
mkdir /home/ubuntu/data
sudo docker service create     --name portainer     --publish 9000:9000     --constraint 'node.role == manager'     --mount type=bind,src=/home/ubuntu/data,dst=/data      --mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock     portainer/portainer     -H unix:///var/run/docker.sock

### Deploy ELK Stack

Deployed ELK at portainer with this repo https://github.com/deviantony/docker-elk using deplot-stack.yml with portioner.

### Deploy Filebeat



### Deploy service containers

Deployed a nginx container just to generate logs and test