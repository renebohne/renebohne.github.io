---
layout:     post
title:      "IoT Teil 1: Espruino flashen"
subtitle:   "IoT mit ESP8266 und Espruino"
date:       2016-10-17 08:00:00
author:     "René"
header-img: "img/bg-IoT.jpg"
tags: IoT esp8266 tutorial project
---

In diesem Tutorial werden wir einen ESP8266 mit Espruino bespielen, um in Javascript einfache IoT Anwendungen zu implementieren.

# Hardware: nodeMCU

Es gibt viele Boards mit einem ESP8266 Chip. Ich verwende in diesem Tutorial das nodeMCU-Board, das es z.B. bei Watterott für unter 10 Euro gibt. Für dieses Tutorial benötigen wir zwei dieser Boards.
Das tolle am ESP8266 ist, dass er WLAN kann. Wir können ihn mit einem Accesspoint verbinden und so Daten ins lokale Netzwerk oder ins Internet senden und Daten von dort empfangen.

![nodeMCU Board](https://raw.githubusercontent.com/nodemcu/nodemcu-devkit-v1.0/master/Documents/NodeMCU_DEVKIT_1.0.jpg){: .center-image }

## Pins

Das nodeMCU Board hat viele Pins, die wir als Ein- und Ausgänge verwenden können. Das folgende Schema zeigt die umfangreichen Möglichkeiten:

![nodemcu pins](https://raw.githubusercontent.com/nodemcu/nodemcu-devkit-v1.0/master/Documents/NODEMCU_DEVKIT_V1.0_PINMAP.png)


# Software: Espruino

Auf dem nodeMCU läuft von Haus aus ein lua Interpreter. Wir wollen aber Javascript anstelle von der lua Programmiersprache verwenden. Espruino wurde ursprünglich für andere Mikrocontroller entwickelt, aber vor einiger Zeit wurde damit begonnen, diese Programmierumgebung auf den ESP8266 zu portieren. Das Projekt ist mittlerweile weit fortgeschritten, aber manche Espruino Features sind noch nicht (fehlerfrei) implementiert. Die einfachen Funktionen, die wir für unser Tutorial verwenden, funktionieren aber zuverlässig.

## Espruino auf den nodeMCU flashen

Auf dem nodeMCU Board ist ein Taster namens FLASH. Dieser muss gedrückt gehalten werden während das USB Kabel in den PC gesteckt wird. Das Board wird dadurch in den FLASH-Modus versetzt.

Es gibt verschiedene Werkzeuge, um neue Firmware auf diese Boards zu laden. Unter Windows verwende ich nodemcu-flasher:
[https://github.com/nodemcu/nodemcu-flasher](https://github.com/nodemcu/nodemcu-flasher){:target="_blank"}

Wir wollen aber nicht die nodeMCU Firmware auf das Board spielen, sondern die Espruino Firmware. Diese gibt es in Form einer ZIP-Datei hier:
[http://www.espruino.com/Download](http://www.espruino.com/Download){:target="_blank"}

Die Datei müssen wir herunterladen und entpacken. In dem entpackten Ordner gibt es einen Unterordner mit der Zeichenkette esp8266 im Namen. Ich habe Version 1v87 heruntergeladen, entsprechend heißt der Ordner bei mir espruino_1v87_esp8266.

In diesem Ordner befinden sich sieben Dateien. Uns interessieren drei von ihnen, die wir in nodemcu-flasher in dem Config-Tab wie im Screenshot dargestellt einstellen:

![config tab]({{ site.baseurl }}/img/nodemcu-flasher-config.png){: .center-image }

Im Advanced Tab stellen wir sicher, dass folgende Einstellungen ausgewählt sind:

![advanced tab]({{ site.baseurl }}/img/nodemcu-flasher-advanced.png){: .center-image }

Nun kann der serielle Port ausgewählt werden, an dem der nodeMCU hängt und der Upload der Firmware gestartet werden. Das dauert wenige Minuten. Wir bereiten beide Boards so vor.
Nach dem erfolgreichen Upload kann nodemcu-flasher geschlossen werden.

## Espruino benutzen

Espruino ist ein Javascript-Laufzeitinterpreter. Das bedeutet, dass man sich über eine virtuelle serielle Verbindung (via USB) oder sogar über WLAN mit dem nodeMCU verbinden kann und in einem Terminalprogramm Befehle eingibt, die eine Ausgabe erzeugen oder einfach nur vom Mikrocontroller ohne Rückmeldung ausgeführt werden. Der Programmcode kann zur Laufzeit verändert werden, wir können also Programme direkt auf dem nodeMCU schreiben. Anstelle eines Terminprogramms (wie z.B putty) verwenden wir aber in diesem Tutorial die Espruino Web-IDE Extension für den Chrome Browser:
https://chrome.google.com/webstore/detail/espruino-web-ide/bleoifhkdalbjfbobjackfdifdneehpo

In der Espruino Web-IDE muss nur der serielle Port des nodeMCU ausgewählt werden und ggf. in den Einstellungen die Baudrate auf 115200 baud angepasst werden. Dann verbindet man die IDE mit dem Board und falls keine Nachrichten erscheinen, drückt man kurz den Reset-Knopf des Boards.

Nun können Befehle eingegeben werden. Im folgenden Abschnitt wird eine WLAN-Verbindung zu einem Accesspoint aufgebaut.

## WLAN konfigurieren

In diesem Code-Schnipsel müssen my-ssid und my-pwd durch die Zugangsdaten des Accesspoints ersetzt werden und den beiden Boards sollten eindeutige Namen gegeben werden anstelle von IoTNode1:

```
var wifi = require("Wifi");
wifi.connect("my-ssid", {password:"my-pwd"}, function(err){
  console.log("connected? err=", err, "info=", wifi.getIP());
});
wifi.stopAP();
wifi.setHostname("IoTNode1")
wifi.save();
```

Diese Zeilen kann man einfach in der Espruino Web-IDE eingeben. Die Zugangsdaten für das WLAN werden gespeichert und müssen beim nächsten mal nicht neu eingegeben werden.

Mehr Informationen zu diesem Thema gibt es hier:
[http://www.espruino.com/ESP8266_WifiUsage](http://www.espruino.com/ESP8266_WifiUsage){:target="_blank"}

# Ausblick

Bisher haben wir nur die Hardware vorbereitet und sind bereit für die erste Internet of Things Anwendung. Diese folgt bald im zweiten Teil dieses Tutorials.
