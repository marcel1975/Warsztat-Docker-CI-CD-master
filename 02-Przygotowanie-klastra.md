Należy wykonać dla dwóch węzłów klastra (manager01, worker01) oraz serwerze jenkins:
```
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get -y install docker-ce
sudo docker info
```
Na węźle manager01:
```
ifconfig
sudo docker swarm init --advertise-addr [IP]
sudo docker info
sudo docker node ls
```
Na węźle worker01:
```
sudo docker swarm join --token [token] [IP]:2377
sudo docker info
```
Uruchomienie visualizera:
```
sudo docker service create \
  --name=viz \
  --publish=8090:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
sudo docker service ls
sudo docker container ls
```
Wejdz na vizulizera:
```
http://manager01:8090
```
