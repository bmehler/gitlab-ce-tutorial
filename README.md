# Gitlab CE auf Docker installieren

## Host eintragen
```html
/etc/hosts
127.0.0.1 gitlab.example.com
```
## Docker vom Docker Hub installieren
```html
docker pull gitlab/gitlab-ce
```
## Docker Image überprüfen
```html
docker image ls
```

## Container aufbauen und starten

```html
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 8929:8929 --publish 2289:22 \
  --name gitlab \
  --restart always \
  --volume /Users/Shared/gitlab/config:/etc/gitlab \
  --volume /Users/Shared/gitlab/logs:/var/log/gitlab \
  --volume /Users/Shared/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```

## Container start überwachen

```html
docker container ps -a
```

## Logfile anschauen (Fehler wegen Permissions)
```html
docker logs -f gitlab
```

## Permissions setzen
```html
sudo chmod g+s /Users/Shared/gitlab/data/git-data/repositories
```

## External url und ssh port setzen
gitlab.rb unter /Users/Shared/gitlab/config öffnen und Werte eintragen
```html
external_url "http://gitlab.example.com:8929"
gitlab_rails['gitlab_shell_ssh_port'] = 2289
```

## Container restarten
```html
docker restart gitlab
```

## Gitlab mit folgender Url öffnen
```html
http://gitlab.example.com:8929/

automatischer redirect zu

http://gitlab.example.com:8929/users/password/edit?reset_password_token=5sFJbZ-jnyFuFbbnXK7s
```

## Befehle für den Container

gitlab ist der Name des Containers

```html
Mit docker container ps -a Container Name suchen und dann

docker start gitlab
docker stop gitlab
docker restart gitlab
```
