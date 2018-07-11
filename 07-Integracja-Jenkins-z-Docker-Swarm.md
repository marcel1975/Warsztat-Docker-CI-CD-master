Przekonfiguruj węzeł manager01:
```
sudo vi /lib/systemd/system/docker.service
  -> Zmień linię "ExecStart=/usr/bin/dockerd -H..." na:
  -> ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243
sudo export DOCKER_HOST="tcp://0.0.0.0:4243"
sudo systemctl daemon-reload
sudo service docker restart
sudo docker ps
```
Przekonfiguruj Jenkinsa:
```
http://jenkins:8080

Cmentarna-Polka-Deploy -> Konfiguruj -> Kroki budowania
  -> Docker Build and Publish
    -> Docker Host URI: tcp://[manager-ip]:4243
```
Uruchom zadanie, podczas wejdz na manager01:
```
sudo watch docker ps
```
