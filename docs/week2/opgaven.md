# Opgaven week 2: hacking the Juice Shop

In dit practicum gaan we aan de slag met het opsporen van beveiligingsproblemen binnen een webshop-applicatie. Voor deze opdracht werken we met Docker en OWASP ZAP (Open Web Application Security Project – Zed Attack Proxy).

## Installatie van OWASP ZAP

[Download](https://www.zaproxy.org/download/) de software. Voltooi de installatie en start de software op. Krijg je tijdens de installatie een foutmelding met betrekking tot de Java-JDK of -JRE? Het kan helpen om [de JDK van Adoptium](https://adoptium.net/) te installeren. **Denk erom dat je bij de stap 'Custom Setup' de optie 'Set or override JAVA_HOME variable' aanzet!**

Om ZAP te leren kennen, begin je met een "Automated scan". Als OWASP ZAP is opgestart kun je hier direct voor kiezen. Na deze keuze kan er een URL ingevoerd worden. Dit is de URL naar een webapplicatie, inclusief de poort. Kies hierna "Aanval". OWASP ZAP zal de gekozen website inladen en past o.a. een fuzzer toe op plekken waar data ingevoerd kan worden. Alle gevonden kwetsbaarheden en uitgevoerde requests worden in de onderste balk gelogd. **Gebruik nu nog niet de Juiceshop**, maar kies bijvoorbeeld je eigen webapp van het vak Webtech. Je zult verbaasd staan hoeveel kwetsbaarheden ZAP zal vinden!

Als je kiest voor "Manual Explore", kun je met een browser naar keuze door een opgegeven website navigeren, terwijl alle requests worden gelogd en eventueel (met aangebrachte wijzigingen) later opnieuw verzonden kunnen worden.
 
Aanvullende informatie is [hier](https://www.zaproxy.org/getting-started/) te vinden.

## Installatie van Docker

We gaan in deze opdracht aan de slag met de Juice Shop-webapplicatie, die een aantal grote beveiligingslekken heeft. De Juice Shop-applicatie gaan we via Docker draaien op je computer. Hierna gaan we beveiligingslekken opsporen in de applicatie.

Met Docker is het mogelijk om een webapplicatie te starten in een vooropgezette omgeving, ook wel *container* genoemd. Je kunt een Docker-container downloaden en deze bevat dan zowel een volledige ingerichte serveromgeving als een geïnstalleerde en geconfigureerde webapplicatie. Let op: als je VM-software hebt geïnstalleerd, zal Docker mogelijk niet werken. Maak in dit geval een Virtual Machine naar keuze (een servervariant van Linux is vaak het snelst) en installeer Docker in deze VM.

Download en installeer Docker via [deze link](https://docs.docker.com/get-docker/).

## Installatie van de Juice Shop-container

Download en draai nu de Juice Shop Docker-container met de volgende commando’s:
```
docker pull bkimminich/juice-shop
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

Als alles goed is gegaan, kun je de applicatie bereiken via [http://localhost:3000](http://localhost:3000) in de browser.

Let even op het gebruik van het Docker **run**-commando. Dit is een combinatie van **create** (container aanmaken) en **start** (container starten). De parameter --rm zorgt ervoor dat een eventuele bestaande container eerst wordt weggegooid. Als je de Juice Shop vaker wilt openen en sluiten, kun je beter eenmalig **create** doen en dan met **start** en **stop** steeds dezelfde container activeren en weer afsluiten:
```
docker create -p 3000:3000 --name juiceshop bkimminich/juice-shop
docker start juiceshop
docker stop juiceshop
```

Klik eerst eens door de Juice Shop heen en plaats bijvoorbeeld een bestelling.
  
## De opdracht: het opsporen van beveiligingsproblemen

Nu gaan we daadwerkelijk aan de slag met het opsporen van beveiligingsproblemen in de Juice Shop. Hiervoor is het belangrijk dat ZAP zonder problemen draait en dat de Juice Shop werkt op je eigen computer.

1\. Met SQL-injectie is het mogelijk om via een invoerveld eigen SQL-statements door een webapplicatie uit te laten voeren. Denk aan [het verwijderen van tabellen](https://xkcd.com/327/) of het omzeilen van de wachtwoord-check bij inloggen. Met dit laatste ga je aan de slag: probeer als administrator in te loggen zonder een wachtwoord op te geven!

Toon je antwoord aan met een of meer screenshots waaruit duidelijk naar voren komt dat je succesvol bent ingelogd. Laat ook de invoer zien die deze illegale inlog mogelijk maakt. Beschrijf hierbij kort welke stappen je hebt uitgevoerd om tot je antwoord te komen. (20%)

2\. Er zit een groot probleem in de Juice Shop waardoor het mogelijk is om een bestelling te plaatsen met een negatief totaalbedrag. Hierdoor zou je in theorie geld toe moeten krijgen. Ga op zoek naar een manier om dit te veroorzaken. Tip: via ZAP zie je alle uitgaande requests. Zet eens een paar producten in je winkelmandje, pas wat aan en ga op zoek naar PUT- of POST-requests die je aan kunt passen. Om een bestelling te plaatsen zul je eerst moeten inloggen. Hiervoor kun je een account aanmaken, of je maakt gebruik van de resultaten van je hack-werk bij opgave 1...

Toon je antwoord aan met de PDF van je bestelling waar een negatief te betalen bedrag op staat. Laat daarnaast je aangepaste request zien en beschrijf welke stappen je hebt uitgevoerd om tot je antwoord te komen. (40%)

3\. Ga zelf op zoek naar **nog twee beveiligingslekken** en toon ook deze weer aan door middel van screenshots en, indien van toepassing, aangepaste requests. Beschrijf daarnaast welke stappen je hebt uitgevoerd om tot je antwoord te komen. (40%)

Enkele suggesties om te proberen:

* Laat een review achter onder andermans naam.
* Laat d.m.v. Cross-Site Scripting (XSS) de website een ongewenste pop-up openen. *Tip: Met behulp van alert() in javascript is het mogelijk om een pop-up venster te openen. De slides van week 2 bevatten voorbeeldcode die je hiervoor kunt gebruiken.*
* Ontdek het patroon in de kortingscoupons en maak je eigen coupon om tot wel 90% korting te krijgen!

Of bedenk zelf iets!