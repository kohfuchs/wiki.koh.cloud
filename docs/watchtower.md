# Watchtower
Watchtower prüft deine Laufenden Docker Container auf Updates.
Ist ein neues Image verfügbar, wird dein Aktueller Container gestoppt, das neue Image Heruntergeladen und der Container mit den neuen Image gestartet. So bleiben deine Applikationen immer auf dem neuesten Stand.

## Quick Start

```
docker run -d \
--name watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower
```
