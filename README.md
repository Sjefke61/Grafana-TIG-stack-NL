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

Gebruik de 'Rapberry Pi imager' software (https://www.raspberrypi.com/software/) om de image te installeren. Kies bij 'Operating System' voor 'Use custom' en selecteer het gedownloade bestand 'GrafanaPi.img'. Kies bij storage de SD-kaart van de Raspberry Pi.

![image](https://github.com/user-attachments/assets/8e4cd44c-cb97-47f5-9b36-7af5fc9aa03a)

Kies bij 'OS customisation' voor 'EDIT STTINGS' en maak de gewenste aanpassingen:

![image](https://github.com/user-attachments/assets/9f97031c-e19c-4012-b69f-917b7f1cf7c2)

![image](https://github.com/user-attachments/assets/e11943c9-463b-47c7-9b6e-7c1656886a10)


Kies na de aanpassingen voor 'YES'

![image](https://github.com/user-attachments/assets/0ca4f889-d3cc-45cf-9e15-0d1a7d217162)
