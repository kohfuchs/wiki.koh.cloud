# Pi-hole
Der Ad Blocker für dein Netzwerk.

## Intro
Pi-hole ist eine Software die sowohl auf einem Raspberry Pi Zero, Pi 1-4, als auch auf einem Heimserver Laufen kann.
Je nach deinen Anforderungen. 

Die funktionsweiße ist dabei einfach erklärt. Werbung wird von den meisten Webseiten und Services von so genannten Ad-Servern nachgeladen. 
Wenn wir uns also eine Webseite aufrufen, ladet diese die Werbung von einem anderen Server nach. Das unterbinden wir indem wir dem Pi-hole eine liste von IP´s und Domains eben dieser Ad-Server geben. 
Der Pi leitet dann die Anfrage auf 127.0.0.1 um, also ins leere.

Das hat einen tollen neben effect, wir können mehr als nur Werbung blocken. Eigentlich alles was über das Netzwerk Kommuniziert, z.B. tracking Dienste und sogar ungewohlte Webseiten.


## Installation
Dank Script wirklich einfach

```
curl -sSL https://install.pi-hole.net | bash
```
Falls es einen Fehler gibt, das `curl` nicht gefunden werden kann, einfach mit `apt intall curl` nachholen.


## Verwendung
Jetzt hast du deinen eigenen kleinen DNS Server der dir das LAN von Werbung frei hält.
Um ihn zu benutzen gibt es zwei möglichkeiten.

1. DNS der einzelnen Geräte auf das Pi-hole zeigen lassen - _So können nur einzelne Geräte gefiltert werden_


2. Den DNS des Routers auf des Pi-hole zeigen lassen - _So werden alle Geräte im LAN gefiltert_


## Tuning
Pi-hole wird besser, je mehr IP's man block.
Das geht am besten mit sogenanten Listen.
Diese findet man überall auf GitHub und im Netz. Hier ein paar Vorschläge.

Listen könnt ihr aktuell halten mit `pihole -g`
> Das geht auch per Cronjob ;)


| Link | Beschreibung |
|:----|:----|
| https://raw.githubusercontent.com/RPiList/specials/master/notserious | Sempervideo Liste für Fakeshops |
| https://raw.githubusercontent.com/RPiList/specials/master/Win10Telemetry | Sempervideo Liste für die WIN10 Telemetry Dienste |
| https://raw.githubusercontent.com/RPiList/specials/master/easylist | Sempervideo Liste für einfach Werbung |
| https://v.firebog.net/hosts/Easylist.txt ||
| https://v.firebog.net/hosts/AdguardDNS.txt ||
| https://raw.githubusercontent.com/chadmayfield/my-pihole-blocklists/master/lists/pi_blocklist_porn_all.list ||