# Zentrale Luftbefeuchtung selber bauen
Wir wohnen in einem gut gedämmten Haus mit zentraler Lüftungsanlage und im Winter sinkt die Luftfeuchtigkeit gerne mal auf um die 30%, wenn es draußen kälter als 5° C wird.

Ich habe mehrere Jahre eine dezentrale Luftbefeuchtung in den Schlafzimmern eingesetzt. Die macht aber vergleichsweise viel Arbeit, da ich regelmäßig den Wasserstand der drei Luftbefeuchter nachsehen und eventuell nachfüllen musste. Vom Stromverbrauch mal ganz abgesehen. Daher war mir klar, dass ich langfristig eine zentrale Lösung brauche.

Im Internet sind Lösungen für die zentrale Luftbefeuchtung über das Lüftungssystem verfügbar, sie waren mir aber mit mehreren tausend Euro plus Installation durch eine Fachfirma zu teuer. Es hat mir aber bestätigt, dass das System an sich machbar ist, weswegen ich nach einem anderen Weg gesucht habe:

|  |  |  |
|--|--|--|
| ![zentrale Luftbefeuchtung](https://github.com/nemiah/zentraleLuftbefeuchtung/blob/main/bilder/bild1.jpg)  | ![zentrale Luftbefeuchtung](https://github.com/nemiah/zentraleLuftbefeuchtung/blob/main/bilder/bild2.jpg) | ![zentrale Luftbefeuchtung](https://github.com/nemiah/zentraleLuftbefeuchtung/blob/main/bilder/bild3.jpg) |




## Teileliste (Amazon Partner-Links):

Bitte die Links in einem neuen Fenster öffnen mit "Strg"/"Cmd ⌘" + Klick.

Behälter:

- [70L Kiste luftdicht, transparent](https://amzn.to/4fTJnAO)

Filter:

- [Filter](https://amzn.to/4gnNftT)
- [Gewindestangen 100mm](https://amzn.to/3OIpMro) 
- [Muttern](https://amzn.to/49lLVVM) 
- [Edelstahlplatte](https://amzn.to/49jSNTL)
- [Metallbohrer 3mm](https://amzn.to/3ZFzaSI) 

Überlaufschutz:

- [Überlaufschlauch](https://amzn.to/4f5Wmy9)
- [Schlauchschellen](https://amzn.to/49m5M7w)
- [Schlauchverschraubung](https://amzn.to/3BgbZ8s)
- [Durchführung](https://amzn.to/3VPSJ8P)
- [Schlauchtülle](https://amzn.to/49UgiD7)
- [Reduzierstück 1" auf 3/4"](https://amzn.to/41KZ6hv)
- [Kugelhahn](https://amzn.to/49pJx0l)
- [Lochsäge 35mm](https://amzn.to/3BA6BNE) 

Nachfüllen:

- [Schwimmerventil](https://amzn.to/4gbqqtm)
- [Kugelhahn](https://amzn.to/41gkyux)
- [Lochsäge 22mm](https://amzn.to/4f0L2TT) 

Nachfüll-Steuerung:

- [2 Wege Motorkugelhahn](https://amzn.to/3BfEd32)
- [Raspberry Pi](https://amzn.to/3ZLa8R8)
- [Netzteil](https://amzn.to/4gqz07O)
- [4-Fach Relais für Raspberry Pi](https://amzn.to/4gPdJo7)
- [Anschlussleitung](https://amzn.to/3P8nfHj)
- [Klemmen](https://amzn.to/49TQgjs)

Luftanschluss:

- [160mm Lochsäge](https://amzn.to/3OHbPKk)
- [Dichtungsband](https://amzn.to/3D1pSrD) 
- [Wandflansch 160mm](https://amzn.to/4fVTa9J)
- [Wickelfalzrohr 160mm](https://amzn.to/3ZnSylR) 
- [Bogen 160mm 90°](https://amzn.to/3ZGbZYN) 
- [Bogen 160mm 30°](https://amzn.to/3BhAPoh) 
- [Bogen 160mm 15°](https://amzn.to/4in4iOd) 
- [Alu Flexrohr](https://amzn.to/3VNkv5Z) 
- [Rohrschellen](https://amzn.to/3Zpq778) 
- [Gewindeeinsätze](https://amzn.to/4g2ppEe) (dann können die Löcher in der Decke kleiner sein)
- [Stockschrauben](https://amzn.to/3VqEBTj) 
- [Dübel](https://amzn.to/4fYqzAw) 
- [Betonbohrer](https://amzn.to/4g0zmBT) 
- [M4 Schrauben](https://amzn.to/3ZmL9Ub) 
- [M4 Muttern](https://amzn.to/3OIL6gq) 

 
 Schalldämmung:
 
 - [Schallschutz-Schaumstoff glatt](https://amzn.to/3ZnOKB7) 
 - [Pyramidenschaumstoff](https://amzn.to/49kQIad) 

##  Zusammenbau

### Behälter vorbereiten

Ok, fangen wir mit dem Behälter an. Es gilt, ein paar Löcher zu bohren:

- 2 Löcher für die Luft, 
- 1 Loch für das Frischwasser und 
- 1 Loch für den Überlaufschutz

## Code für die Steuerung

	# GPIO-Bibliothek laden
	import RPi.GPIO as GPIO
	import time

	GPIO.setmode(GPIO.BCM)

	GPIO.setup(4, GPIO.OUT)
	GPIO.setup(26, GPIO.OUT)

	GPIO.output(4, True)
	GPIO.output(26, True)

	time.sleep(60 * 20)

	GPIO.output(26, False)

	time.sleep(30)
	GPIO.output(4, False)

	GPIO.cleanup()

Das Ganze dann zum Beispiel zweimal am Tag per cron ausführen:

	0 6,18 * * * /usr/bin/python onoff.py

## Anmerkungen
Wenn du Verbesserungsvorschläge hast, dann mach gerne ein [Issue](https://github.com/nemiah/zentraleLuftbefeuchtung/issues) dazu auf.
