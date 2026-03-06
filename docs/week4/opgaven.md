# Opgave week 4: threat modelling

We gaan deze week bezig met het bepalen van risico’s van een geheel systeem in een voorbeeldcasus aan de hand van de STRIDE-methode. 

## Casus

Een Gronings **deelmobiliteitsbedrijf** lanceert de app *GroenRijden*, waarmee gebruikers in de stad elektrische deelfietsen en -steps kunnen huren. De app biedt de volgende functionaliteit:

1. **Voertuig zoeken en ontgrendelen**: de app toont beschikbare voertuigen op een kaart (op basis van de GPS-locatie van de gebruiker en van de voertuigen). Een voertuig wordt ontgrendeld door met de app een Bluetooth-verbinding te maken met het slot.
2. **Rit registreren**: tijdens een rit wordt de route van het voertuig continu bijgehouden via GPS. Aan het einde van de rit vergrendelt de gebruiker het voertuig weer via de app. De ritgegevens (start- en eindlocatie, route, duur, afstand) worden opgeslagen.
3. **Betalen**: de ritprijs wordt berekend op basis van duur en afstand. De gebruiker betaalt via een gekoppelde creditcard of iDEAL. De betalingen worden afgehandeld door een externe betaalprovider (PSP).
4. **Beloningssysteem**: op basis van rijgedrag (snelheid, parkeren in aangewezen zones) krijgen gebruikers punten die korting opleveren. De app houdt een persoonlijk profiel bij met ritstatistieken en een gedragsscore.
5. **Gemeentekoppeling**: de app deelt geanonimiseerde data over parkeergedrag en ritpatronen met de gemeente Groningen, die dit gebruikt voor handhaving van parkeerzones en voor verkeersbeleid.

Het systeem bestaat uit de volgende onderdelen:

- De **mobiele app** (iOS/Android), geïnstalleerd op het toestel van de gebruiker.
- Een **centrale back-end server** met een API, die de app-logica en gebruikersdata beheert.
- Een **gebruikersdatabase** met accountgegevens, rithistorie, betaalgegevens en gedragsscores.
- **IoT-modules in de voertuigen**: elk voertuig heeft een Bluetooth-slot en een GPS/4G-module die locatiegegevens naar de back-end stuurt.
- De **externe betaalprovider** (PSP), die creditcard- en iDEAL-transacties verwerkt.
- Een **API-koppeling met de gemeente** voor het delen van geanonimiseerde gebruiksdata.

Gebruikers registreren zich met e-mailadres, telefoonnummer en betaalgegevens. De authenticatie verloopt via e-mail/wachtwoord met optionele tweefactorauthenticatie (2FA) via SMS.

## Opdrachten

1.\ Teken het Data Flow Diagram (DFD) van de beschreven casus. Het diagram moet het systeem op een niveau laten zien dat geschikt is voor een risicoanalyse. Zorg dat de DFD overzichtelijk en navolgbaar neergezet wordt. Dit kan op papier, maar mag uiteraard ook met een softwaretool (zie onderstaande lijst). Tip: nummer de interfaces, zodat je er bij 2 en 3 gemakkelijk naar kunt verwijzen.

2.\ Pas threat modelling toe op je DFD. Geef in je DFD aan waar welke risico’s zitten. Beperk je hierbij tot de _interfaces_: plekken waar data over een trust boundary gaat. Gebruik hiervoor de STRIDE-methodiek:

* <b>S</b>poofing: je voordoen als iemand anders of een ander systeem, bijv. doordat er geen wachtwoordeisen zijn.
* <b>T</b>ampering: aanpassen van data op een systeem of netwerk, bijv. door XSS.
* <b>R</b>epudiation: kunnen ontkennen van iets wat je gedaan hebt, doordat er geen logging is.
* <b>I</b>nformation Disclosure: ongeautoriseerd toegang verschaffen tot data, bijv. mogelijk gemaakt door *plain text* versturen van data.
* <b>D</b>enial of Service: werking van services verhinderen, bijv. door een DDOS-aanval.
* <b>E</b>levation of Privilege: toegang krijgen tot rechten die je niet had, bijv. door gebruik te maken van kwetsbaarheden in verouderde software.

3.\ Geef per interface minstens één concreet aanvalsscenario waarin één of meer van de door jou gekozen STRIDE-letters terugkomen.

4.\ Maak nu een lijst van de interfaces, gesorteerd op prioriteit, dus de in jouw optiek meest kwetsbare bovenaan. Onderbouw je keuze!

5.\ Beschrijf voor de top 3 van kwetsbare interfaces welke maatregelen er genomen kunnen worden (geef meerdere opties; denk ook aan tijd-/geld-investering van het bedrijf!). Denk hierbij aan de afkorting META:

* <b>M</b>itigate: een tegenmaatregel implementeren
* <b>E</b>liminate: de interface geheel verwijderen
* <b>T</b>ransfer: de verantwoordelijkheid overdragen aan een andere partij
* <b>A</b>ccept: het risico voor lief nemen en niets doen

*Tip: je kunt 2 t/m 5 grotendeels in één keer maken door gebruik te maken een tabel met kolommen voor de interfaces, de STRIDE-letters, de scenario's, de prioriteiten en de tegenmaatregelen, en deze te sorteren op prioriteit. Zie bijvoorbeeld de Excel-sheet die op BrightSpace staat. Denk er wel om dat je de **onderbouwing** van je prioritering erbij vermeldt!*

## Tools voor het tekenen van DFD's

De DFD is de basis voor de opdracht van deze (en volgende) week. Je mag hem op papier tekenen of desnoods in MS Paint, maar er zijn betere (gratis) tools beschikbaar die je het leven wat gemakkelijker kunnen maken, zoals:

* [Draw.io](https://app.diagrams.net/), met DFD-ondersteuning toegevoegd via 'Meer vormen'/'More shapes'
* [LucidChart](https://www.lucidchart.com/pages/data-flow-diagram), gratis versie met max. 60 elementen
* [Miro](https://miro.com/templates/data-flow-diagram/)
* [Drawboard PDF](https://www.drawboard.com/pdf/)
* [GraphViz](https://graphviz.org/)
* [SDL: de Microsoft Threat Modeling Tool](https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling)

Om maar een paar te noemen. Aanvullingen (in de vorm van een [pull request](https://github.com/hanze-hbo-ict/sw_sec_docs)) zijn van harte welkom.