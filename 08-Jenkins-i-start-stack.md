Tworzymy na serwerze gitlab w folderze z repozytorium plik docker-compose.yml:
```
version: '3.1'

services:
  app:
    image: [nazwa repo]/[obraz]:latest
    ports:
      - "8080:80"
    deploy:
      replicas: 2
    command: nginx -g 'daemon off;'
```
Nastepnie zakładamy plik index.html i wpisujemy co chcemy, na końcu edytujemy plik Dockerfile:
```
# Version: 0.2
FROM ubuntu:16.04
MAINTAINER Maciej Lelusz "maciej.lelusz@inleo.pl"
RUN apt-get update && apt-get install -y nginx
COPY index.html /var/www/html/index.html
EXPOSE 80
```
Zamin zrobimy git push wejdzmy na jenkins:
```
Cmentarna-Polka-Deploy -> Konfiguruj -> Kroki budowania -> Dodaj krok budowania
  -> Execute shell:
    export DOCKER_HOST="tcp://[manager01-wew-IP]:4243"
    docker stack rm cmentarna-polka
    docker stack deploy -c /var/lib/jenkins/workspace/Cmentarna-Polka-Deploy/docker-compose.yml cmentarna-polka
```
Powołaj vizualizer na manager01:
```
docker service rm viz
sudo docker service create --name=viz --publish=8090:8080/tcp --constraint=node.role==manager -e DOCKER_HOST="[manager01-wew-IP]:4243"   dockersamples/visualizer
```
Wykonaj git push na gitlab w katalogu repozytorium:
```
git add . && git commit -m "change" && git push -u origin master
```

