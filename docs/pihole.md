# Pi-hole
Der Ad Blocker für dein Netzwerk.

![pihole](https://pi-hole.github.io/graphics/Vortex/Vortex_with_text.png)

Unter [pi-headless/](../pi-headless/) erfährst du wie man auch ohne Bildschirm den Pi in Betrieb nimmt.

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
Falls es einen Fehler gibt, das `curl` nicht gefunden werden kann, einfach mit `apt install curl` nachholen.


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
| https://v.firebog.net/hosts/Easylist.txt ||
| https://v.firebog.net/hosts/AdguardDNS.txt ||
| https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV.txt| SmartTV Liste |
| https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/android-tracking.txt | Android Tracking |


## Regex

[https://docs.pi-hole.net/ftldns/regex/overview/](https://docs.pi-hole.net/ftldns/regex/overview/)


```
(^|\.)buffpanel\.com$
(^|\.)bugsnag\.com$
(^|\.)redshell\.io$
(^|\.)treasuredata\.com$
(^|\.)unity(|3d)\.com$
(^|\.)unityads(|\.co)\.com$
([a-zA-Z0-9-\.]{2,256})(.cn)
([a-zA-Z0-9-\.]{0,256})(sendgrid)(.net)
.*(xn--)([a-zA-Z0-9-\.]{2,256})*(\.[a-z]{2,6})
.*(xn--)([a-zA-Z0-9-\.]{2,256})*(?!\.de)(\.[a-z]{2,6})
^(.+[_.-])?ad[sxv]?[0-9]*[_.-]
^(.+[_.-])?adse?rv(er?|ice)?s?[0-9]*[_.-]
^(.+[_.-])?telemetry[_.-]
^(www[0-9]*\.)?xn--
^adim(age|g)s?[0-9]*[_.-]
^adtrack(er|ing)?[0-9]*[_.-]
^advert(s|is(ing|ements?))?[0-9]*[_.-]
^aff(iliat(es?|ion))?[_.-]
^analytics?[_.-]
^banners?[_.-]
^beacons?[0-9]*[_.-]
^count(ers?)?[0-9]*[_.-]
^mads\.
^pixels?[-.]
^stat(s|istics)?[0-9]*[_.-]
^track(ers?|ing)?[0-9]*[_.-]
^r[0-9]*([-]{1,3}|.)sn-[a-z0-9]{4,}-[a-z0-9]{4,}\.googlevideo
```

### Quick add

```
pihole --regex '^r[0-9]*([-]{1,3}|.)sn-[a-z0-9]{4,}-[a-z0-9]{4,}\.googlevideo' '^track(ers?|ing)?[0-9]*[_.-]' '^stat(s|istics)?[0-9]*[_.-]' '^pixels?[-.]' '^mads\.' '^count(ers?)?[0-9]*[_.-]' '^beacons?[0-9]*[_.-]' '^banners?[_.-]' '^analytics?[_.-]' '^aff(iliat(es?|ion))?[_.-]' '^advert(s|is(ing|ements?))?[0-9]*[_.-]' '^adtrack(er|ing)?[0-9]*[_.-]' '^adim(age|g)s?[0-9]*[_.-]' '^(www[0-9]*\.)?xn--' '^(.+[_.-])?telemetry[_.-]' '^(.+[_.-])?adse?rv(er?|ice)?s?[0-9]*[_.-]' '^(.+[_.-])?ad[sxv]?[0-9]*[_.-]' '.*(xn--)([a-zA-Z0-9-\.]{2,256})*(?!\.de)(\.[a-z]{2,6})' '.*(xn--)([a-zA-Z0-9-\.]{2,256})*(\.[a-z]{2,6})' '([a-zA-Z0-9-\.]{0,256})(sendgrid)(.net)' '([a-zA-Z0-9-\.]{2,256})(.cn)' '(^|\.)unityads(|\.co)\.com$' '(^|\.)unity(|3d)\.com$' '(^|\.)treasuredata\.com$' '(^|\.)redshell\.io$' '(^|\.)bugsnag\.com$' '(^|\.)buffpanel\.com$'
```