# Rancher

![Rancher Logo](https://rancher.com/imgs/rancher-logo-horiz-color.png "Rancher Logo")

.. ist eine Plattform die es dir erlaubt Docker container und auch Kubernetes Netzwerke zu erstellen und zu verwalten.

Der YouTube Kanal Techno Tim [erklährt](https://www.youtube.com/watch?v=oILc0ywDVTk "YouTube Video 'Docker, Rancher, Kubernetes... Minecraft? (Rancher Setup and Install Tutorial)' von Techno Tim") eine alternative, welche mit Kuberneties funktioniert.


## Quick Start

> Der Single Node Docker Container ist für die Testumgebung Zuhause gedacht und wird nicht für die Verwendung in Enterprise umgebungen Empfohlen!

```
docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest
```

## __WIP__
