# TFM

## Configuration

### Create the VM

Created a virtual machine with IP 192.168.1.107 and installed ubuntu server 18.04, then updated the repos:

`sudo apt-get update`
`sudo apt-get upgrade`

### Configure Docker

Configure docker repository:

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
`add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

Update the the repository information, install and init docker:

`sudo apt-get update`
`sudo apt-get install -y docker-ce`
`sudo apt-get install docker-compose`
`systemctl start docker`
`systemctl enable docker`

### Initialize Swarm

`sudo docker swarm init`

### Configure Portainer

Create a folder to store portainer data:

`mkdir /home/ubuntu/data`

Initialize portainer as a docker swarm service:

`sudo docker service create --name portainer --publish 9000:9000 --constraint 'node.role == manager' --mount type=bind,src=/home/ubuntu/data,dst=/data --mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock portainer/portainer -H unix:///var/run/docker.sock`

### Deploy ELK Stack + Filebeat





### Deploy service containers

Deployed a nginx container just to generate logs and test