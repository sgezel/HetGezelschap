
## Schema

![[Attachements/Diagram 1.svg|700]]

## Onderdelen van het netwerk


|   |   |   |   |
|---|---|---|---|
|Onderdeel|Type|Locatie|Doel|
|Modem Orange||Kelder Sandor, in kelder met verwarming tegen de linkse muur bij het binnenkomen||
|Patch Panel||Serverkot|verdelen van netwerkkabels|
|Alfred|Server|Serverkot|Op deze server draaien verschillende virtuele machines, en servers|
|Switch||Serverkot||
|Anna|Server|Serverkot|NAS/Storage|
|Weinstein|Server|Serverkot|Media center, hierop staat JellyFin en Komga|
|Midas|Server|Serverkot|Toestel om te downloaden, heeft een aantal terrabyte aan tijdelijke storage. Op dit moment gebruikt voor JDownloader|
|Viene|Server|Serverkot|NAS/Storage|

Zie ook schema van het netwerk.

# Kort overzicht van de virtuele servers en applicaties

Op Alfred draaien er een aantal applicaties en virtuele machines. Hieronder een overzicht:

- Proxmox (192.168.1.7):
	-  [https://192.168.1.7:8006](https://192.168.1.7:8006)
	- Beheer van de virtuele machines
- Ubiquity (192.168.1.4):
	-  [https://192.168.1.4:8443](https://192.168.1.4:8443)
	-  Beheer van  het draadloos netwerk (alle Ubuiquity access points) - Dit zijn de witte ronde schijven
- Proxy (192.168.1.17):
	- Via ssh: 192.168.1.17
	-  Via de proxmox interface > proxy > console
	- Hierop draait Caddy. Dit is een applicatie die een vertaling doet tussen een aanvraag op een specifiek adres, naar een ander adres.  
	  Een voorbeeld hiervan is Sonarr. Deze is op het intern netwerk toegankelijk via [https://sonarr.kasteel-gezel.be](https://sonarr.kasteel-gezel.be). Wanneer Caddy deze aanvraag binnen krijgt zal deze die vertalen naar [http://192.168.1.26:8989](http://192.168.1.26:8989). Een overzicht van de welke reverse proxies er zijn volgt later in dit document.
- PfSense (192.168.1.1):
	-  [https://192.168.1.1](https://192.168.1.1)
	-  Dit is de firewall. Dit is ineens het hart van het netwerk. Dit doet de vertaling van het intern verkeer naar het extern verkeer en omgekeerd. Ook staat deze in voor een aantal interne regels, zoals de \*.kasteel-gezel.be DNS regels
- W10-pro-test (192.168.1.106):
	-  Via RDP    
	- Via Teamviewer (geconfigureerd op Sandor zijn account)
	- Via de proxmox interface > w10test > Console
	- Dit is een toestel dat doorgaans gebruikt wordt voor het uitvoeren van taken van buitenaf. Het gebeurt ook wel dat via dit toestel dingen worden gedaan zoals het uitvoeren van scripts die wat langer duren, of het verplaatsen van bestanden.
- Download (192.168.1.185):
	- Via RDP
	- Via de proxmox interface > Download > Console
	-  Applicaties
		- Qbittorrent: [https://torrent.kasteel-gezel.be](https://torrent.kasteel-gezel.be)
		- Deluge: [http://192.168.1.185:8080](http://192.168.1.185:8080)
		- Jackett: http://192.168.1.185:9117
	- Hierop staan de torrent clients (qBittorrent voor publieke trackers, Deluge voor private trackers) en Jackett. Deze laatste is bedoeld om op uniforme manier te kunnen gaan zoeken op verschillende websites naar de juiste inhoud.  
	  Deze applicaties zijn op hun beurt dan weer toegangkelijk via de RDP, of via hun webinterfaces.
    