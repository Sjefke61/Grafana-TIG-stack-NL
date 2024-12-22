# Grafana TIG-stack voor Raspberry Pi (NL)

Om een jump-start te kunnen maken met deze monitoring tool, een Raspberry Pi image waarop de software stack 'Grafana-Influx-Telegraf' is geïnstalleerd en geconfigureerd.

Deze image is gemaakt met de pi-gen tool waarmee ook de officiële Raspberry Pi images gemaakt worden. Het is een 'Raspberry Pi OS Lite (64-bit)' versie zonder desktop environment. Als extra is Telegraf-Influx-Grafana geinstalleerd en enkele hulpprogramma's. Tevens worden enkele configuratie aanpassingen gemaakt zodat er snel een werkende monitoring tool beschikbaar is.

# Aanpassingen aan de standaard image

- Keys en repository's van Grafana en Influxdata geïnstalleerd
- Influxdb, Telegraf, Grafana en afhankelijkheden geïnstalleerd
- snmpd en afhankelijkheden geïnstalleerd (monitoring eth0 van de Raspberry Pi)
- Extra mibs geïnstalleerd (monitoring interfaces)
- Telegraf geconfigureerd (Ping test naar 8.8.8.8 en monitor interface eth0)
- snmpd geconfigureerd (community public)
- Automatisch opstarten van Grafana, Telegraf en Influxdb
- Locale NL geïnstalleerd
- Automatisch updaten van de Raspberry Pi

# Installatie

Gebruik de 'Rapberry Pi imager' software (https://www.raspberrypi.com/software/) om de image te installeren.
- Kies bij 'Operating System' voor 'Use custom' en selecteer het gedownloade bestand 'GrafanaPi.img'.
- Kies bij storage de SD-kaart van de Raspberry Pi.
- Kies bij 'OS customisation' voor 'EDIT STTINGS' en maak de gewenste aanpassingen (vergeet niet SSH te enablen).

Nadat de Raspberry Pi is opgestart is moet het IP-nummer opgezocht worden welke de Pi van de DHCP-server heeft gekregen. Dit kan op de volgende manieren:
- Kijk op de DHCP-server welk IP-nummer is uitgedeeld aan host-name 'Grafana'.
- Beeldscherm aansluiten op de Raspberri Pi, inloggen, hostname -I
- Netwerkscanner

# Grafana

Start Grafana op in een webbrowser: http://IP-nummer:3000 en login met de default admin credentials.
Configureer als eerste de datasource:
- Menu -> Connections -> Data sources, kies InfluxDB, URL: http://localhost:8086 (zoals het voorbeeld), Database: grafana, Save & test

Importeer het dashboard
- Menu -> Dashboards -> New, Import -> Upload dashboard JSON file en kies het gedownloade bestand: Grafana-dashboard.json

Maak dit dashboard default
- Meru -> Administration -> General -> Default preferences, Home Dashboard, kies Dashboards/Status, Save

Kies voor 'Home' en het dashboard met twee voorbeeld grafieken zal verschijnen. Derze grafieken zijn hierna gemakkelijk te kopieëren en aan te passen.

# Telegraf

Login met behulp van SSH in op de Raspberry PI. In het configuratiebestand /etc/telegraf/telegraf.conf wordt bepaald welke gegevens worden toegevoegd aan de Influx database. Bijvoorbeeld toevoegen van een ping test naar IP-nummer 8.8.4.4:
```
[[inputs.ping]]
  urls = ["8.8.4.4"]
  count = 1
  method = "exec"
[inputs.ping.tags]
  name = "ping-4"
```

Bijvoorbeeld toevoegen van een interface van de router:
```
[[inputs.snmp]]
  agents = ["udp://192.168.1.1"]
  version = 2
  community = "public"
  path = ["/usr/share/snmp/mibs"]

[[inputs.snmp.table]]
    oid = "IF-MIB::ifTable"
    name = "interface"
    inherit_tags = ["source"]

  [[inputs.snmp.table.field]]
      oid = "IF-MIB::ifDescr"
      name = "ifDescr"
      is_tag = true
```

Om de aanpassingen van telegraf.conf actief te maken: sudo service telegraf restart

Hierna kunnen binnen Grafana de grafieken toegevoegd worden.
