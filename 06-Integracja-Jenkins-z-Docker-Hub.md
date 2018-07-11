Na serwerze GitLab, w miejscu gdzie jest nasz kod tworzymy plik .dockerignore i umieszczamy w nim:
```
.git
```
Następnie towrzymy Dockerfile:
```
# Version: 0.1
FROM ubuntu:16.04
MAINTAINER Imie Nazwisko "imie.nazwisko@adres.pl"
RUN apt-get update && apt-get install -y nginx
RUN echo 'Wujek Vernon, wujek Vernon.' > /var/www/html/index.html
EXPOSE 80
```
Zainstaluj plugin CloudBees Docker Build and Publish w Jenkins:
```
http://jenkins:8080

Zarządzaj Jenkinsem -> Zarządzaj wtyczkami -> Dostępne:
  -> CloudBees Docker Build and Publish
    -> Zainstaluj bez restartu
    -> Uruchom ponownie kiedy wtyczka zostanie zainstalowana
```
Następnie trzeba dodać uprawnienia dla użytkownika jenkins:
```
sudo usermod -a -G docker jenkins
sudo usermod -a -G root jenkins
```
I zrestartować serwer:
```
sudo reboot
```
Po restarcie zaloguj się do Jenkinsa:
```
http://jenkins:8080

Cmentarna-Polka-Deploy -> Konfiguruj -> Dodaj krok budowania
  -> Docker Build and Publish
    -> Repository name: [użytkownik-z-dodcker-hub]/[nazwa-repo]
    -> Tag: ${BUILD_NUMBER}
    -> Registry credentials:
      -> Add: Jenkins
        -> Kind: Username with Password
        -> Username: [użytkownik-docker-hub]
        -> Password: [hasło-docker-hub]
        -> ID: [użytkownik]
```
Na serwerze GitLab, w miejscu gdzie jest nasz kod wywołujemy:
```
git add . && git commit -m "change" && git push -u origin master
```
Wchodzimy na Docker Hub i sprawdzamy czy w naszym rejestrze jest kolejna wersja kontenera.
