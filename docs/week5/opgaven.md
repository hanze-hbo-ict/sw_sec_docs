# Opgaven week 5: cryptografie en privacy threat modelling

We gaan ons deze week verdiepen in de wondere wereld van de cryptografie, om de technieken die zo belangrijk zijn voor security en privacy beter te begrijpen. Daarnaast gaan we bezig met het bepalen van privacyrisico’s van een voorbeeldcasus aan de hand van de LINDDUN-methode. 

## Deel 1: cryptografie (50%)

* Windows: [download](https://www.cryptool.org/en/ct2/downloads/) en installeer CrypTool 2.
* Mac: je zou bijvoorbeeld [Wine](https://www.winehq.org/) kunnen gebruiken om de Windows-executable te draaien.
* Linux: [in deze video](https://www.youtube.com/watch?v=nTEj-lZ2V38) kun je zien hoe je het onder Linux kunt installeren.

Kies _Main functions_ > _Create a new workspace with the graphical editor_ om op een grafische manier inputs, encryptie-algoritmes en outputs aan te maken en met elkaar te verbinden.

CrypTool heeft wat _quirks_ waar je rekening mee moet houden. Hier wat tips om je te helpen:

* Zodra je op de Play-knop drukt om de encryptie te activeren, kun je je workspace niet meer editen. Druk eerst op Stop om weer aanpassingen te kunnen maken.
* Bovenin de linkerbalk kun je zoeken op de naam van componenten. Dat is vaak de snelste manier om een component te vinden.
* Je kunt componenten vanuit de linkerbalk in de workspace slepen. Standaard worden ze vrij klein weergegeven. Maak ze groter door erop te klikken en dan aan de rechter onderhoek te trekken.
* Verplaatsen kan door aan één van de andere drie hoeken te trekken.
* Als je een component groter maakt, kun je bijvoorbeeld de instellingen beter zien.
* Componenten hebben vaak meerdere input- en outputmogelijkheden. Hover over de kleine pijltjes links-rechtsboven heen om te zien wat voor input/output er verwacht wordt. Verbinden doe je door van het outputpijltje van de ene component naar het inputpijltje van de andere te slepen.
* De pijltjes zijn erg klein dus let goed op dat je de juiste verbinding aanmaakt!

### Opdracht 1.1: Caesar Cypher

Als opwarmer bekijken we het klassieke voorbeeld van een zeer eenvoudige vorm van encryptie: substitutie. Substitutie betekent letterlijk vervanging en in dit geval wordt elke letter uit het alfabet vervangen door een letter die een vast aantal posities verderop in het alfabet staat.

1.1.a.\ Maak een Caesar-encryptie aan die een stukje Engelse tekst van enkele regels (plaats dit in een Text Input) versleutelt, op basis van een zelfgekozen _key_, en laat de uitvoer zien in een Text Output. De key kun je instellen via "Key as integer" of door er een Number Input aan te koppelen. Zorg dat bij de instellingen de Action op "Encrypt" staat.

1.1.b.\ Maak een tweede Caesar-component aan die de output weer ontsleutelt, in eerste instantie op basis van de bij 1.1.a handmatige ingestelde key. Laat het resultaat zien in een nieuwe Text Output.

1.1.c.\ Voeg een Frequency Test (frequentie-analyse) op de output van de encryptie toe en sluit de uitkomst hiervan aan op een Caesar Analyzer (instelling Language: English). Sluit ook de versleutelde tekst aan op deze Analyzer.

1.1.d.\ Tot slot: sluit de uitvoer van de Analyzer aan op de tweede Caesar-component (de ontsleutelaar, met Action: Decrypt). De handmatig ingestelde key verdwijnt nu. Druk op de Play-knop en als het goed is zie je dat de Analyzer je oorspronkelijke tekst gereconstrueerd heeft.

Maak een screenshot van je workspace en leg in een paar zinnen in eigen woorden uit hoe deze combinatie van componenten werkt.

### Opdracht 1.2: symmetrische encryptie met AES

Zoals je hebt gezien, zijn substitutiealgoritmes gemakkelijk te kraken met frequentieanalyse. Moderne algoritmes voegen daarom technieken toe zoals matrixvermenigvuldiging, een geheime sleutel en de XOR-operator. [Lees hier meer over de symmetrische Advanced Encryption Standard (AES)](https://www.geeksforgeeks.org/advanced-encryption-standard-aes/).

Maak voor deze opdracht een nieuwe workspace aan.

1.2.a.\ Plaats een AES Visualization in de workspace. Sluit hier twee Text Inputs op aan, eentje voor de key en eentje voor de te versleutelen tekst. Om het helemaal goed te laten werken, zet je tussen elke Text Input en de AES een String Decode, die tekst omzet in bytes. Denk er ook om dat de lengte van de key overeenkomt met de _keysize_ van AES (bijv. 128 bits = 16 bytes = key van 16 letters). Sluit tot slot een Text Output aan op de AES. Druk op Play en klik met Next door de visualisatie heen die in de AES-component wordt getoond. Als je het principe op een gegeven moment snapt, kun je met _Skip Round_ de zaken wat versnellen.

1.2.b.\ Vervang de AES Visualization door een gewone AES-component, met Action: Encrypt. Verifieer dat (het eerste gedeelte van) de output niet verandert. De Visualization encodeert alleen het eerste stuk van de input, ter grootte van de keysize. De normale AES encodeert de volledige aangeleverde tekst (door de key zo vaak als nodig te herhalen).

1.2.c.\ Maak een tweede AES-component aan, met Action: Decrypt. Sluit deze aan op de Text Output met de geëncrypte tekst, en op dezelfde sleutel die je ook voor het encrypten gebruikt hebt (dit is waarom het symmetrische encryptie heet). De uitvoer van de tweede AES leid je via een String Encode naar een Text Output, waar je als het goed is na een druk op Play de oorspronkelijke tekst weer terugvindt.

Graag weer een screenshot van je workspace, plus een samenvatting in eigen woorden van hoe AES werkt (max. 5 regels).

### Opdracht 1.3: asymmetrische encryptie met RSA

Nog veiliger is asymmetrische encryptie, waarbij er voor de versleuteling en ontsleuteling aparte keys worden gebruikt. Deze keys worden altijd in een paar gegenereerd, volgens een complex wiskundig algoritme. De typische use case is dat een gebruiker het publieke deel van het sleutelpaar publiceert. Wie hem of haar een bericht wil sturen, moet het versleutelen met deze public key. De ontvanger is vervolgens de enige die het kan ontsleutelen, met behulp van het private deel van het sleutelpaar (de private key). Dit gaan we nu nabootsen.

Maak voor deze opdracht weer een nieuwe workspace aan.

1.3.a.\ Plaats een RSA-component met Action: Encryption in de workspace. Maak een RSA Key Generator aan (de standaardinstellingen zijn prima) en sluit deze op de juiste manier aan op de RSA (N en **e**). Op de Message-input van de RSA sluit je een Text Input met de te versleutelen tekst aan, via een String Decode. De Message-output van de RSA (Byte[]) schrijf je naar een Text Output. Je hebt nu de input versleuteld met de publieke sleutel (e).

1.3.b.\ Plaats een tweede RSA-component, nu met Action: Decryption, in de workspace. Sluit hem aan op de Message-output van de RSA, en op de RSA Key Generator (het private gedeelte, N en **d**). De output gaat weer via een String Encode naar een Text Output, waar je als het goed is de oorspronkelijke tekst ziet verschijnen.

1.3.c.\ (optioneel, maar wel leuk) Werk samen met een klasgenoot. Deel je publieke sleutel (N en e) met diegene en vraag om jou een daarmee gecodeerd bericht terug te sturen. Ontsleutel dit met je private sleutel (N en d). Als dit gelukt is, draai je de rollen om.

Graag een screenshot van je RSA-workspace, plus een samenvatting in eigen woorden van hoe het algoritme werkt (max. 5 regels).

## Deel 2: privacy threat modelling (50%)

We gebruiken hiervoor dezelfde casus als vorige week. De DFD kun je dus hergebruiken!

2.1.\ Pak je Data Flow Diagram van vorige week erbij. Tip: nummer behalve de interfaces (wat je al gedaan had) nu ook de data stores, zodat je er bij 2.2 en 2.3 gemakkelijk naar kunt verwijzen.

2.2.\ Definieer welke privacyrisico’s er **per interface** (plekken waar data over een trust boundary gaat) én **per data store** in de DFD aanwezig zijn. Maak hierbij gebruik van de LINDDUN-afkorting om de types risico’s aan te geven in de DFD:

* <b>L</b>inkability: data aan elkaar koppelen.
* <b>I</b>dentifiability: subject identificeren op basis van data.
* <b>N</b>on-<b>r</b>epudiation: opgeslagen data niet kunnen aanpassen of verwijderen.
* <b>De</b>tectability: kunnen vaststellen dát er data is over een subject.
* <b>Di</b>sclosure of information: data wordt ongevraagd openbaar.
* <b>U</b>nawareness: data wordt verwerkt zonder dat het subject het weet.
* <b>N</b>on-<b>c</b>ompliance: data wordt niet conform de wet- en regelgeving verwerkt.

2.3.\ Geef per interface en data store minstens één concreet aanvalsscenario waarin één of meer van de door jou gekozen LINDDUN-letters terugkomen. Hierbij komt ook kijken:

* Wat voor privacygevoelige informatie er over de interface gaat of in de data store staat.
* Wat voor probleem het is als deze informatie uitlekt, voor de verschillende stakeholders (denk aan studenten, de bouwer van de app, de leveranciers van andere systemen zoals Osiris, de Hanze).

2.4.\ Maak nu een lijst van de interfaces en data stores, gesorteerd op prioriteit, dus de in jouw optiek meest kwetsbare bovenaan. Onderbouw je keuze!

2.5.\ Bedenk voor de top 3 van kwetsbare interfaces zo veel mogelijk maatregelen om de gevonden risico’s te verminderen.

*Tip: je kunt 2 t/m 5 grotendeels in één keer maken door gebruik te maken een tabel met kolommen voor de interfaces en data stores, de letters L I Nr De Di U Nc, de scenario's (incl. type data en stakeholders), de prioriteiten en de tegenmaatregelen, en deze te sorteren op prioriteit. Zie bijvoorbeeld de Excel-sheet die op BrightSpace staat. Denk er wel om dat je de **onderbouwing** van je prioritering erbij vermeldt!*