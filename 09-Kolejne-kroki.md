Docker Banch Sec:
```
git clone https://github.com/docker/docker-bench-security.git
cd docker-bench-security
sh docker-bench-security.sh
```
Przydatne komendy:
```
docker ps --quiet | xargs docker inspect --format '{{ .Id }}: Ports={{ .NetworkSettings.Ports }}'
docker ps --quiet --all | xargs docker inspect --format '{{ .Id }}: Propagation={{range $mnt := .Mounts}} {{json $mnt.Propagation}} {{end}}'
```
Apparmor:
```
mkdir -p /etc/apparmor.d/containers/
nano /etc/apparmor.d/containers/docker-nginx
 
-> wkład z https://docs.docker.com/engine/security/apparmor/#nginx-example-profile

apparmor_parser -r -W /etc/apparmor.d/containers/docker-nginx
```
