Pobranie token z Gitlab do Jenkinsa:
```
http://gitlab

Admin Area -> Users -> jenkins -> Impersonation Tokens
  -> Skopiuj token
```
Instalacja wtyczki GitLab w Jenkinsie:
```
http://jenkins:8080

Zarządzaj Jenkinsem -> Zarządzaj wtyczkami -> Dostępne:
  -> GitLab
    -> Zainstaluj bez restartu
    -> Uruchom ponownie kiedy wtyczka zostanie zainstalowana
```
Konfiguracja połączenia pomiędzy Jenkins a GitLab:
```
Zarządzaj Jenkinsem -> Skonfiguruj system -> GitLab
  -> Connection Name -> GitLab
  -> GitLab Host URL -> http://gitlab
  -> Credentials -> Add
    -> Domain: Global
    -> Kind: GitLab API token
      -> Scope: Global
      -> API token: [token-skopiowany-z-gitlaba]
      -> ID: jenkins
  -> Test Connection
```
Dodanie projektu w Jenkins:
```
Nowy projekt
  -> Nazwa: Cmentarna-Polka-Deploy
  -> Ogólny projekt
    -> Repozytorium kodu
      -> Git
        -> Repository URL: http://gitlab/root/Cmentarna-Polka.git
        -> Credentials
          -> Add: Jenkins
            -> Username: jenkins
            -> Password: [hasło-użytkownika-jenkins-zalozonego-na-gitlab]
            -> ID: jenkins
          -> Wybierz z listy jenkins
      -> Zaznacz pole przy "Build when a change is pushed to GitLab. GitLab CI Service URL: http://jenkins:8080/project/Cmentarna-Polka-Deploy"
  Kliknij guzik Zapisz.
```
Stworzenie użytkownika dla GitLab:
```
Zarządzaj Jenkinsem -> Zarządzaj użytkownikami -> Stwórz użytkownika
  -> login: gitlab
```
Nowy projekt w GitLab w połączeniu z Jenkinsem:
```
http://gitlab

Admin Area -> Settings -> Outbound requests -> Expand -> Allow requests to the local network from hooks and services -> Save Changes

Otwórz projekt Cmentarna-Polka -> Settings -> Integration -> Project services -> Jenkins CI (przewiń w dół aby znaleźć na liście)
  -> Active
  -> Jenkins url: http://[jenkins]:8080/
  -> Project name: Cmentarna-Polka-Deploy
  -> login: [gitlab-user-zalozony-w-jankins]
```
Test działania poprzez dodanie pliku do naszego repo z serwera gitlab:
```
touch index.html
git add index.html
git commit -m "add index.html"
git push -u origin master
```
