Pobierzmy licencję trial na GitLab (Jenkins CI działa tylko w wersji EE):
```
https://about.gitlab.com/free-trial/
```
Na serwerze GitLab:
```
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get install -y curl openssh-server ca-certificates
sudo apt-get install -y postfix
sudo curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash 
sudo EXTERNAL_URL="http://[nazwahosta]" apt-get install gitlab-ee
```
Wejdzmy na stronę:
```
http://gitlab
```
Ustawmy licencję:
```
Admin Area (klucz francuski, za menu po lewej stronie na górze) 
  -> License 
  -> Upload New License
```
Konfiguracja użytkownika dla Jenkinsa:
```
Admin Area (klucz francuski, za menu po lewej stronie na górze)
  -> Users
  -> New user (zielony przycisk po prawej)
  -> Name: jenkins
  -> Access level: Admin
```
Jak zostanie stworozny użytkownik przejdz do zakładki:
```
Impersonation Tokens
  -> Name: jenkins
  -> Scopes: api
```
Jak już stworzysz token, to go skopjuj i kliknij guzik edit w prawym górnym rogu strony i wypełnij hasło, nastęnie zapisz zmiany.

Nowy projekt (repozytorium) towrzymy poprzez kliknięcie na plus (+) w prawym górnym rogu, następnie New project, nazywamy go Cmentarna-Polka.

Następnie podłączamy się do naszego repozytorium z serwera GitLab:
```
git --version
git clone http://gitlab/root/Cmentarna-Polka.git
cd Cmentarna-Polka
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```
