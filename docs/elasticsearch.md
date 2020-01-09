# Elastic Search
> für Ubuntu oder [Debian-Derivate](https://de.wikipedia.org/wiki/Liste_von_Linux-Distributionen#Debian-Derivate)

## 1. Install ES
```
sudo apt install openjdk-11-jre
```
```
sudo apt install apt-transport-https
```
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
```
sudo echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | tee -a /etc/apt/sources.list.d/elasticsearch.list
```
```
sudo apt update && sudo apt install elasticsearch
```


### ES config
```
vim /etc/elasticsearch/elasticsearch.yml
```
ändere `network.host: 127.0.0.1`

### Restart
```
sudo systemctl daemon-reload && sudo systemctl enable elasticsearch && sudo systemctl start elasticsearch
```
---
### Check if Running
```
curl -XGET '127.0.0.1:9200/?pretty'
```

Falls der Dienst nicht startet, kann es sein, dass man zuwenig RAM hat, dann muss man in der `/etc/elasticsearch/jvm.options` zb auf 512m runtergehen.

## 2. Install „ingest-attachment“

Installiere das „ingest-attachment“-Plugin (required for PDF, PPT, XLS etc.)
```
sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install ingest-attachment
```
Nach erfolgreicher Installation, ES neustarten mit:

```
sudo systemctl restart elasticsearch
```



## 3. Install Tesseract OCR

Wenn nötig können wir OCR mit installieren

```
sudo apt install tesseract-ocr tesseract-ocr-eng tesseract-ocr-deu tesseract-ocr-fra
```

## Zusatz

Falls alle Sprachen verwendet werden sollen:
```
sudo apt install tesseract-ocr tesseract-ocr-all
```
