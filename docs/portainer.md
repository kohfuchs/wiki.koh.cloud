# Portainer
![Portainer Logo](https://raw.githubusercontent.com/portainer/portainer/develop/app/assets/images/logo_alt.png "Portainer Logo")

Deine Docker Verwaltung.

[Demo hier verfügbar.][Portainer Demo]

## Intro

[Portainer] ist ein Tool, welches eine Weboberfläche hostet (als [Docker Container]) um [Docker] hosts oder "swarm clusters" zu verwalten.

Es können folgende Docker Ressourcen verwaltet werden:

- containers

- images

- volumes

- networks

- App Templates um deployment noch mehr zu beschleunigen

und mehr

[Portainer]: https://www.portainer.io/
[Docker]: https://www.docker.com/
[Docker Container]: https://www.docker.com/resources/what-container
[Portainer Demo]: http://demo.portainer.io/

## Installation

Die [Portainer] Server-Software kann einfach in einer bestehenden [Docker] Umgebung (nur Linux) wie folgt installiert werden:
```
docker volume create portainer_data
docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```
Und schon wurde ein Container erstellt und die Weboberfläche ist über den Docker host Port :9000 erreichbar.


## Alternative

![Rancher Logo](https://rancher.com/imgs/rancher-logo-horiz-color.png "Rancher Logo")

> [Hier gehts zum wiki ->](/rancher)

Der YouTube Kanal Techno Tim [erklährt](https://www.youtube.com/watch?v=oILc0ywDVTk "YouTube Video 'Docker, Rancher, Kubernetes... Minecraft? (Rancher Setup and Install Tutorial)' von Techno Tim") eine alternative, welche mit Kuberneties funktioniert.

Rancher [https://rancher.com/quick-start/](https://rancher.com/quick-start/)

### Single node Quick start

```
docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest

```
