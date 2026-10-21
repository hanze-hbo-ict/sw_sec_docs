# Opgave week 7 – netwerksecurity

Deze opgave is speciaal voor de Deeltijd-variant van het vak Security.

## Side-Channel Attack 
Je probeert in te loggen op een website, waarna je als reactie krijgt dat het wachtwoord niet klopt. Kun je het antwoord van de server gebruiken om het wachtwoord te kraken? 

Ja. Tenminste, als er geen rekening is gehouden met het risico van een timing attack. Een Timing Attack is een vorm van Side-Channel Attack waarbij de responstijd van de server gebruikt wordt om letter voor letter een wachtwoord te kraken. 

Neem als voorbeeld de volgende functie:

```python
def check_password(actual_password, provided_password):
    if len(provided_password) == len(actual_password):
        for i in range(len(provided_password)):
            if provided_password[i] != actual_password[i]:
                return("Incorrect password. Access Denied.")
        return("Password correct. Access Granted.")
    else:
        return("Incorrect password. Access Denied.")
```

De functie gaat karakter voor karakter het gegeven wachtwoord bij langs en kijkt of het overeenkomt met het daadwerkelijke wachtwoord.
Zodra die een verkeerd karakter tegenkomt eindigt de functie en wordt de toegang geweigerd; pas als alle karakters zijn gecheckt wordt de toegang verleend. 

Dit betekent dus dat hoe meer karakters (op een rij, vanaf het eerste karakter) juist zijn, hoe vaker de loop wordt herhaald, en dus hoe langer het duurt voor de functie een antwoord teruggeeft!  

Met deze kennis zouden we kunnen proberen om het wachtwoord te kraken, en dat is ook precies wat we in deze opdracht gaan doen. 

## Opdracht 
We gaan een side-channel attack uitvoeren op een lokale Docker-server. 

### Installaties en verbinding
Zorg ervoor dat je Docker geïnstalleerd hebt en voer de volgende commando’s uit: 

``docker pull el3an0r/hanze-timing-attack``

``docker run -d -p 8080:3840 --name timingattack el3an0r/hanze-timing-attack``

Als het goed is draait er nu een Docker-container met daarop de server. Je kunt het nog even controleren met ``docker ps`` en/of door, bijvoorbeeld met Postman, een Websocket-verbinding te maken met ``localhost:8080``.

### De aanval
Voor de aanval maak je gebruik van [het bestand client.py](https://github.com/hanze-hbo-ict/sw_sec_docs/tree/master/src/pract-wk7/client.py) dat al enkele functies bevat om de verbinding tot stand te laten komen: ``client_connect()`` is een backend-functie die de directe koppeling met de server regelt en eventuele errors afvangt. ``call_server()`` maakt daar weer gebruik van, en kun je direct aanroepen in je oplossing. 

NB: gebruik géén andere soorten aanvallen om het wachtwoord te proberen te kraken! De server is niet bijzonder robuust en als je hem platgooit heb je zowel jezelf als alle andere studenten ermee. 
De functie ``call_server()`` mag naar wens worden aangepast, maar zorg dat je de regel met ``time.sleep(0.001)`` laat staan; dit zorgt ervoor dat jullie de server niet per ongeluk DDoS’en met zijn allen. 

Er staat in deze server één persoon geregistreerd, met gebruikersnaam 000000. Met het volgende stappenplan gaan we erachter komen welk wachtwoord (bestaand uit kleine letters en cijfers) deze persoon heeft. 
 
### Stappenplan 

1. Controleer of de functionaliteit van de verbinding: werkt de test-aanroep onderaan de code? 

2. Als de verbinding werkt zul je eerst een manier nodig hebben om te timen hoe lang de server erover doet om een antwoord te sturen. Pas de code aan zodat je voor elke inlogpoging ziet hoe veel tijd er tussen het versturen van de credentials en het ontvangen van het antwoord zit. 

3. Nu je kunt meten hoe lang de server doet over een antwoord kunnen we beginnen met kraken! Stap één is het bepalen van de lengte van het wachtwoord. Schrijf een functie die de responstijd van wachtwoorden van verschillende lengte meet, en deze gebruikt om de juiste lengte te bepalen. Denk goed na over waar in de code je het tijdsverschil meet. _Hint: variabele vertraging in het netwerk voegt willekeur toe aan de responstijd._ 

4. Wat kun je doen om je metingen betrouwbaarder te maken? Denk hierbij bijvoorbeeld aan een statistische analyse. 

5. Nu je de juiste lengte hebt kun je beginnen met het kraken van het wachtwoord zelf. Doe dit door eerst een ontwerp te maken met [pseudo-code](https://en.wikipedia.org/wiki/Pseudocode) en er met zijn tweeën naar te kijken alvorens je het implementeert. Doe dit vóórdat je het internet raadpleegt voor hulp!<br>
_Hint: je zult teken voor teken aan de slag moeten gaan!_<br>
NB: het wachtwoord bestaat uit alleen kleine letters en cijfers. 

### Verslag

Het verslag is een _lab journal_ waarin we alle denk- en ontwikkelstappen kunnen nalezen, evenals de uitkomsten en conclusies. De hoofdstukindeling dient als volgt te zijn:

|       |       |
| ----- | ----- |
| *Abstract* | Behandelt kort alle gevraagde onderwerpen (intro, methodiek, resultaten en discussie) |
| *Introductie* | Omschrijft in eigen woorden duidelijk de doelstellingen |
| *Methodiek* | Omschrijft volledig & repliceerbaar plan van aanpak<br>Benoemt alle relevante gebruikte technieken en processen |
| *Resultaten* | Omschrijft duidelijk en volledig de uitkomst van opdracht |
| *Discussie* | Reflecteert op mate waarin doelstelling is behaald<br>Reflecteert op minstens één succes & één verbeterpunt van/voor eigen werken |
| *Bronvermelding* | Bronvermelding, netjes & systematisch |

In het hoofdstuk “Discussie” behandel je de volgende vragen: 

* Welke statistieken heb je gebruikt om de metingen betrouwbaar te maken, en met enige zekerheid het juiste teken op elke plek van het wachtwoord te herkennen?
* Welke oplossingen heb je geprobeerd die niet werkten, en waarom werkten ze niet? 
* Welke omstandigheden hebben nog meer invloed op je meetresultaten, buiten de code en het ontwerp om? 
* Welke omstandigheden heb je "in het echt" nog meer, die invloed kunnen hebben op zulke metingen? Denk hierbij aan een heel netwerk in plaats van een lokale server.

Noem in het hoofdstuk “Resultaten” ook het “gestolen” wachtwoord van onze gedupeerde. Als je het wachtwoord niet hebt kunnen vinden resulteert dat niet per se een onvoldoende, maar je zult dan wel een erg goede verslaglegging van je ontwerp- en troubleshooting-processen moeten vastleggen en kunnen aantonen dat je goed over alle obstakels hebt nagedacht. 

### Inleveren 

Voor deze weekopgave lever je de volgende onderdelen in: 

* Jullie versie van het client.py bestand met de code die je hebt gebruikt om de server te kraken, voorzien van eigen commentaar.
* Een .pdf met dezelfde code + commentaar. Dit voor het beoordelen op BrightSpace.
* Een .pdf van de eerste volledige versie van je pseudo-code (als je je pseudo-code schriftelijk hebt gemaakt is een .pdf met/van een foto ook goed).
* Een .pdf van het verslag.