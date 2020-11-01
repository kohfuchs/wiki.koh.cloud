# Healthchecks.io
Healthchecks ist ein Monitoring tool geschrieben in Python.
Es bietet dir die möglichkeit Cronjobs zu überwachen, ohne auf dem Host eine zusätzliche Software zu installieren.

## Zusätzliche Software
Für meine Instanz Nginx als Reverse Proxy für SSL benötigt.

* `nginx`

## Docker Command aus der Doku
Mit diesem Docker command kannst du schnell und einfach den container von  `linuxserver/healthchecks`zu starten.

```
docker create \
--name=healthchecks \
-e PUID=1000 \
-e PGID=1000
-e SITE_ROOT=<SITE_ROOT> \
-e SITE_NAME=<SITE_NAME> \
-e DEFAULT_FROM_EMAIL=<DEFAULT_FROM_EMAIL> \
-e EMAIL_HOST=<EMAIL_HOST> \
-e EMAIL_PORT=<EMAIL_PORT> \
-e EMAIL_HOST_USER=<EMAIL_HOST_USER> \
-e EMAIL_HOST_PASSWORD=<EMAIL_HOST_PASSWORD> \
-e EMAIL_USE_TLS=<EMAIL_USE_TLS> \
-e ALLOWED_HOSTS=<ALLOWED_HOSTS> \
-e SUPERUSER_EMAIL=<SUPERUSER_EMAIL> \
-e SUPERUSER_PASSWORD=<SUPERUSER_PASSWORD> \
-p 8000:8000 \
-v <path to data>:/config \
--restart unless-stopped \
linuxserver/healthchecks
```

Hier die Doku zur config [https://github.com/healthchecks/healthchecks/#configuration](https://github.com/healthchecks/healthchecks/#configuration)


## Docker Command mit Telegram

Hier der Container der bei mir läuft.

Zusätzlich habe ich folgende funktionen gesetzt/aktiviert:

* `REGISTRATION_OPEN=False`
 		- Diese funktion verhindert das sich fremde an dieser Instanz anmelden können. Standart ist `True` - also verfügbar für jeden

```
docker create \
--name=healthchecks \
-e PUID=1000 \
-e PGID=1000 \
-e SITE_ROOT=monitor.example.com \
-e SITE_NAME=ExampleMonitor \
-e DEFAULT_FROM_EMAIL=admin@example.com \
-e EMAIL_HOST=smpt.example.com \
-e EMAIL_PORT=587 \
-e EMAIL_HOST_USER=admin@example.com \
-e EMAIL_HOST_PASSWORD=password \
-e EMAIL_USE_TLS=True \
-e REGISTRATION_OPEN=False \
-e SUPERUSER_EMAIL=admin@example.com \
-e SUPERUSER_PASSWORD=password \
-e TELEGRAM_BOT_NAME=@botname \
-e TELEGRAM_TOKEN=<api_key> \
-p 8000:8000 \
-v /srv/hc_config/:/config \
--restart unless-stopped \
linuxserver/healthchecks
```

## PosgreSQL als DB
> Der Container von Linux Server bietet diese funktion derzeit nicht an.
> Ein fix wurde schon erstellt, allerdings ist dieser noch nicht released?. -- [Github Pull](https://github.com/linuxserver/docker-healthchecks/pull/32)

```
-e DB=postgres \
-e DB_HOST=localhost \
-e DB_PORT=5432 \
-e DB_NAME=db_name \
-e DB_USER=db_user_name \
-e DB_PASSWORD=db_password \
```



## Reverse Proxy


```
server {
    listen 80;
    listen [::]:80;
    server_name monitor.example.com;

    location ^~ / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Host $host/office;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        proxy_redirect off;
        proxy_pass http://127.0.0.1:8000/;
      }
}
```
Zum schluss lassen wir noch von [`certbot`](/certbot) ein SSL Zertificat für unsere Domain erstellen.


## Tipp
Wie immer bei einem Service der mit Docker läuft, empfiehlt es sich [Watchtower](/watchtower) mit laufen zu lassen.
