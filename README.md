# Grafana TIG-stack voor Raspberry Pi (NL)

Om een jump-start te kunnen maken met een monitoring tool op een Raspbery Pi is dit een image waarop de software stack 'Grafana-Influx-Telegraf' is geïnstalleerd en geconfigureerd.

Deze image is gemaakt met de pi-gen tool waarmee ook de officiële Raspberry Pi images gemaakt worden. Het is een 'Raspberry Pi OS Lite (64-bit)' versie zonder desktop environment. Als extra is Telegraf-Influx-Grafana geinstalleerd en enkele hulpprogramma's. Tevens worden enkele configuratie aanpassingen gemaakt zodat er snel een werkende monitoring tool is.

# Aanpassingen aan de standaard image

- Keys en repository's van Grafana en Influxdata geïnstalleerd
- Influxdb, Telegraf, Grafana en afhankelijkheden geïnstalleerd
- snmpd en afhankelijkheden geïnstalleerd (monitoring eth0 van de Raspberry Pi)
- Extra mibs geïnstalleerd (monitoring interfaces)
- Telegraf geconfigureerd (Ping test naar 8.8.8.8 en monitor interface eth0)
- snmpd geconfigureerd (community public)
- Automatisch opstarten van Grafana, Telegraf en Influxdb
- Locale NL geïnstalleerd

# Installatie

Gebruik de 'Rapberry Pi imager' software (https://www.raspberrypi.com/software/) om de image te installeren.
Kies bij 'Operating System' voor 'Use custom' en selecteer het gedownloade bestand 'GrafanaPi.img'. Kies bij storage de SD-kaart van de Raspberry Pi.
Kies bij 'OS customisation' voor 'EDIT STTINGS' en maak de gewenste aanpassingen (vergeet niet SSH te enablen).
