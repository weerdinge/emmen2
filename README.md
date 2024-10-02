
Netwerken
Fortigate
Stap 1: Inloggen op FortiGate
Open een webbrowser en voer het IP-adres van je FortiGate-apparaat in (standaard is dit meestal 192.168.1.99).

Log in met je gebruikersnaam en wachtwoord. Standaard:

Gebruikersnaam: admin

Wachtwoord: leeg (geen wachtwoord, tenzij eerder ingesteld)

Stap 2: Toegang tot de Interface Configuratie
Zodra je bent ingelogd, kom je terecht op het Dashboard.

Klik in het linkermenu op Network (Netwerk) en daarna op Interfaces.

Hier zie je een lijst van alle beschikbare interfaces op je FortiGate-apparaat.


Stap 3: Een Nieuwe Interface Toevoegen
Om een nieuwe interface toe te voegen of een bestaande interface te configureren, volg je deze stappen:

VLAN's Aanmaken op Port 4

Volg deze stappen om VLAN's aan te maken op Port 4 van een FortiGate-apparaat:


Stap 1: Navigeren naar de Interface Instellingen

Ga naar het Dashboard en klik in het linkermenu op Network > Interfaces.

Hier zie je een lijst met alle fysieke interfaces, inclusief Port 4.


Stap 2: Een VLAN Interface aanmaken op Port 4

Klik op Create New in het Interfaces-scherm.

Kies VLAN als Type interface.


Stap 3: VLAN-instellingen Configureren

Interface: Selecteer Port 4 als de fysieke interface waarop de VLAN’s zullen worden gemaakt.

VLAN ID: Geef het VLAN een uniek ID-nummer (bijvoorbeeld 10 voor de eerste VLAN).

Elk VLAN moet een uniek VLAN ID hebben (bijv. 10 voor Sales, 20 voor HR, enz.).

Alias: Geef de VLAN een beschrijvende naam, zoals VLAN_Sales, VLAN_HR, of VLAN_IT, zodat het gemakkelijk te identificeren is.

IP/Netmask: Stel een IP-adres en subnetmasker in voor de VLAN. Bijvoorbeeld:

VLAN_Sales: 192.168.10.1/24

VLAN_HR: 192.168.20.1/24

VLAN_IT: 192.168.30.1/24

Administrative Access: Kies welke toegangsmethoden toegestaan zijn (bijv. HTTPS, Ping, SSH).

Klik op OK om de VLAN-interface op Port 4 aan te maken.

Stap 4: Herhaal voor Andere VLAN’s

Als je meer VLAN’s wilt aanmaken op Port 4, herhaal je stap 3 en 4.

Voor elk VLAN gebruik je een uniek VLAN ID en een andere IP-range om conflicten te vermijden.


Firewall Policy
Login banner activeren
config system global
set pre-login-banner enable
set post-login-banner enable
end

Stap 1: Toegang tot de Firewall Policy Sectie
Log in op je FortiGate-apparaat.

Ga in het linkermenu naar Policy & Objects en selecteer IPv4 Policy.

Stap 2: Een Nieuwe Policy Maken voor Verkeer naar Internet
Je maakt eerst een policy die toestaat dat elk VLAN op Port 4 toegang heeft tot het internet.

Klik op Create New.

Vul de volgende instellingen in:

Name: Geef de policy een duidelijke naam, bijvoorbeeld VLAN_to_Internet.

Incoming Interface: Selecteer de interface van het VLAN dat je wilt toestaan (bijv. VLAN_Sales op Port 4).

Outgoing Interface: Selecteer de WAN-interface (bijv. port1 of de interface die met het internet verbonden is).

Source: Kies de bron (meestal all of een specifieke IP-range voor het VLAN).

Destination: Selecteer all om al het verkeer naar het internet toe te staan.

Service: Kies de service die je wilt toestaan, bijvoorbeeld ALL (voor alle services zoals HTTP, HTTPS, etc.). Als je bepaalde services wilt beperken, kun je specifieke services zoals HTTP, HTTPS, DNS kiezen.

Action: Selecteer Accept om het verkeer toe te staan.

Klik op OK om de policy aan te maken.

Herhaal voor Andere VLAN's

Voor elk VLAN dat toegang moet hebben tot het internet (bijv. VLAN_HR of VLAN_IT), maak je een aparte policy aan met dezelfde stappen hierboven, maar selecteer de juiste Incoming Interface voor elk VLAN.

Stap 3: Policies Maken voor Verkeer Tussen VLAN's
Indien je toestaat dat verkeer tussen de VLAN's mogelijk is, moet je hiervoor policies aanmaken. Bijvoorbeeld, je wilt dat VLAN_Sales en VLAN_IT met elkaar kunnen communiceren.

Klik opnieuw op Create New.

Vul de volgende instellingen in:

Name: Geef de policy een naam, zoals VLAN_Sales_to_VLAN_IT.

Incoming Interface: Selecteer de interface van het eerste VLAN (bijv. VLAN_Sales).

Outgoing Interface: Selecteer de interface van het tweede VLAN (bijv. VLAN_IT).

Source: Kies de bron (bijv. all of een specifiek IP-bereik van VLAN_Sales).

Destination: Kies de bestemming (bijv. all of het IP-bereik van VLAN_IT).

Service: Kies ALL om al het verkeer tussen deze VLAN's toe te staan, of kies specifieke services.

Action: Selecteer Accept.

Klik op OK om de policy op te slaan.

Voorbeeld:



Switch
Hostname: hostname Switch

Timestamps: service timestamps debug datetime msec and service timestamps log datetime msec

Password Encryption: service password-encryption

Enable Password: enable secret 5 

Local User: username admin password 7

Domain Name: ip domain-name Parker.int

VLAN Policy: vlan internal allocation policy ascending

SSH: ip ssh version 2

Interface Configuration:

interface FastEthernet1/0/1 (and other interfaces)

switchport access vlan <vlan_number>

switchport mode access (or trunk as needed)

switchport trunk encapsulation dot1q (for trunk interfaces)

switchport trunk allowed vlan <vlan_list>

VLAN Configuration:

interface Vlan<vlan_number>

ip address <ip_address> <subnet_mask> (for VLANs with IP addresses)

SNMP: snmp-server community public RO and snmp-server community private RW

Login Banner: banner login ^CBeheerder: Boaz^C

Line Configuration:

line con 0 and line vty 0 4 (or 5 15)

login local

transport input ssh


Save the Configuration
Save: Type copy running-config startup-config and press Enter to save the current configuration to the startup configuration, which will be loaded when the switch reboots.



Windows
voor het ad pas de IP en computer naam aan!
AD 
DNS https://www.youtube.com/watch?v=6l2T7-4dJis&t=139s&ab_channel=NetITGeeks
DHCP als je 2 scopes  hebt zorg ervoor  dat je  de subnet aangepast word
OU  https://www.youtube.com/watch?v=cETbT22TWEE
Share https://www.youtube.com/watch?v=sJ_E7I4CHw0
Policies https://www.youtube.com/watch?v=BdXauD16f-w
PRTG https://www.youtube.com/watch?v=VhzabVyLUV4


simpel stap voor stap uitleg 

Linux

Installatiehandleiding voor Linux en Nextcloud via Docker


waarom docker?

Gemakkelijk Herstellen: Als er iets kapot gaat met een applicatie, kun je de container eenvoudig verwijderen en opnieuw opzetten. Dit bespaart tijd en moeite
en waarom niet :)

1. Installeer Docker

Let op: Tijdens de installatie van Linux, selecteer niet de Nextcloud-optie.

Voer de volgende stappen uit om Docker te installeren:

Installeer Docker met de volgende command:

Command: sudo apt install docker.io

Voer alleen stap 1 uit van deze handleiding voor Docker Compose:
Install Docker-Compose <-  Link

Start de Docker-service met:
Command: sudo systemctl start docker

Controleer of Docker correct werkt door het testcommando uit te voeren:
Command: docker run hello-world

Tip: Gebruik altijd sudo voor Docker-commando’s, anders werkt het niet!



Voorbeeld:

2. Nextcloud Installatie via Docker

Volg deze stappen om Nextcloud te installeren via Docker:

installeer mariadb (deze stap geld ook voor wordpress)

Command: sudo apt install mariadb-server

Command: sudo systemctl status mariadb 

Command: sudo systemctl start mariadb (als die uit staat)




Bezoek de officiële Docker Hub-pagina van Nextcloud:

Nextcloud Docker Image <-  Link
maak wachtwoorden in de yaml file aan!  verder niks veranderen

Wordpress docker image <- Link

  


Scroll naar beneden voor de voorbeeld docker-compose.yml-file.
als je het niet kan vinden CTRL + F zoek naar "compose"

Maak een nieuwe directory voor Nextcloud aan en navigeer ernaartoe:

Command: mkdir nextcloud

Command: cd nextcloud

Maak de docker-compose.yml-file aan:

Command: sudo nano docker-compose.yaml

Kopieer de docker-compose.yml-file van de Docker Hub-pagina (gebruik SSH voor eenvoudig kopiëren en plakken) en plak deze in het bestand.

Sla de wijzigingen op door CTRL + X in te drukken, gevolgd door Y en druk op Enter.



Start de Nextcloud Container
Nadat je de docker-compose.yml-file hebt aangemaakt en opgeslagen, kun je de Nextcloud-container starten met behulp van Docker Compose. Volg deze stappen:

Zorg ervoor dat je je in de directory bevindt waar je de docker-compose.yml-file hebt opgeslagen. Als je dat nog niet gedaan hebt, navigeer er naartoe met:

Command: cd nextcloud

Voer het volgende commando uit om de Nextcloud-container te starten:

Command: sudo docker-compose up -d

Uitleg:

De up-optie start de container(s) gedefinieerd in de docker-compose.yml-file.

De -d-vlag staat voor "detached" mode, wat betekent dat de containers op de achtergrond draaien, zodat je de terminal kunt blijven gebruiken.

Controleer of de containers correct draaien:

Command: sudo docker-compose ps


Start de WordPress-container

Nadat je de docker-compose.yml-file hebt aangemaakt en opgeslagen, kun je de WordPress-container starten met behulp van Docker Compose. Volg deze stappen:

Navigeer naar de juiste directory:
Zorg ervoor dat je je in de directory bevindt waar je de docker-compose.yml-file hebt opgeslagen. Als je dat nog niet hebt gedaan, navigeer er naartoe met het volgende commando:
Commando:mkdir wordpress & cd wordpress

Voer het volgende commando uit om de Wordpress-container te starten:

Command: sudo docker-compose up -d

Uitleg:

De up-optie start de container(s) gedefinieerd in de docker-compose.yml-file.

De -d-vlag staat voor "detached" mode, wat betekent dat de containers op de achtergrond draaien, zodat je de terminal kunt blijven gebruiken.

Controleer of de containers correct draaien:

Command: sudo docker-compose ps


