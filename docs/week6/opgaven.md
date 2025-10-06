# Opgave week 6 – security: de verantwoordelijkheid van de ontwikkelaar(?)

## Deel 1: toepassen op je eigen project (50%)

Tijd om alles wat je geleerd hebt toe te passen in de praktijk! Neem een (web)applicatie waar je zelf aan gebouwd hebt, bijvoorbeeld die van Webtechnologie of het IoT-project, en beantwoord de volgende vragen:

1. Teken een DFD van de applicatie. Dit mag je eventueel samen doen met degenen met wie je de applicatie gebouwd hebt. (30%)
2. Benoem de interfaces en pas bij elke interface threat modelling met STRIDE + de eerste letter D van LINDDUN (Detectability) toe. Welke letters zijn van toepassing? Leg kort uit waarom. (30%)
3. Bij welke interface hebben de gevonden kwetsbaarheden bij elkaar genomen de grootste impact? Licht kort toe. (10%)
4. Noem tenminste één tegenmaatregel (denk aan META) die je hiertegen kunt nemen. Laat zien hoe je deze kunt toepassen, bijvoorbeeld met een screenshot van kwetsbare code vóór en na een door jou bedachte _patch_. (30%)

## Deel 2: veilige TPS-reports voor Initech (50%)

Je hebt in deze cursus allemaal tools aangereikt gekregen om veilige(re) applicaties te bouwen. Betekent dit nu dat security exclusief jouw verantwoordelijkheid als engineer<sup>*</sup> is? Ben je als engineer immers niet ook onderdeel van een groter geheel (team, bedrijf, sector, land, EU...) en is security niet eerder een gedeelde verantwoordelijkheid? Welke partijen kun je allemaal aanwijzen en voor welk aspect van security (welk onderdeel van de Software Development Life Cycle) zouden zij verantwoordelijk kunnen/moeten zijn?

Ga eerst over deze vragen in discussie je klasgenoten en vorm zo je eigen mening.

Dan de casus (kenners herkennen in deze casus wellicht delen van de cultfilm [Office Space](https://www.imdb.com/title/tt0151804/), verplichte kost voor elke ICT'er). Je bent engineer<sup>*</sup> bij de firma Initech. Het management heeft het plan opgevat om maandelijks zogenaamde [TPS Reports](https://en.wikipedia.org/wiki/TPS_report#Office_Space) te laten genereren die allerlei informatie bevatten over de productiviteit van elke medewerker. Denk hierbij aan data als: ziekte en ander verzuim, aantal vergaderuren, aantal geschreven regels code, aantal ingediende pull-requests, percentage goedgekeurde pull-requests etc. De rapporten zijn intern en bestemd voor de managers van de betreffende medewerkers. Aan jou is gevraagd om de applicatie te (helpen) ontwikkelen die deze rapporten kan genereren en verdelen onder de juiste personen.

Het moge duidelijk zijn dat, als Initech dit per se wil doen, het heel zorgvuldig moet gebeuren, omdat hier allerlei risico's op de loer liggen, op het gebied van privacy, datalekken, tampering etc. Welke adviezen kun jij aan [de CEO van Initech](https://en.wikipedia.org/wiki/Bill_Lumbergh) geven om deze risico's in ieder geval te minimaliseren?

### Opdracht 1

Noem 3 activiteiten die jij als engineer<sup>*</sup> kunt doen om tot een zo veilig mogelijke applicatie te komen. Leg bij elke activiteit uit in welke fase je deze toepast (Requirements, Ontwerp, Ontwikkeling, Testen of Deployment) en waarom deze bijdraagt aan een veilige applicatie.

_Voorbeeld: in de Testfase draaien wij als ontwikkelteam een SAST-tool over de code om veelvoorkomende fouten er alvast uit te halen._

### Opdracht 2

Je bent natuurlijk niet de enige binnen dit project. Noem 3 andere partijen die volgens jou ook een rol (zouden moeten) hebben bij de security van de TPS Reports, plus bij elk een korte beschrijving wat die rol dan zou moeten inhouden en in welke fase(s) van de SDLC deze van toepassing is.

Met _partijen_ bedoelen we onder andere: andere teamleden, andere functies of afdelingen binnen hetzelfde bedrijf, de klant, andere bedrijven, providers, (cloud)hosts, vakbonden, politie, bestuursorganen zoals gemeentes, provincies, de Tweede Kamer, de regering en de EU maar ook bijvoorbeeld de Autoriteit Persoonsgegevens. Eigen toevoegingen zijn van harte welkom!

_Voorbeeld: er moet een security-expert (intern of van een extern bureau) bij het project betrokken worden, zodat diegene de requirements, ontwerpen, gerealiseerde code en de uiteindelijke setup kan controleren op veiligheidsissues._

### Oplevering

Maak van bovenstaande zes punten een lopend verhaal, en voeg een korte inleiding en conclusie toe. Schrijf het in de vorm van een advies aan het management van de firma Initech. Richtlijn: 1 A4'tje, ongeveer 300 woorden.

## Hoe moet je het geheel inleveren?

Het threat modelling-rapport en het advies aan Initech (deel 1 en 2) mogen worden samengevoegd in één document en als doc(x) of pdf worden ingeleverd via het Inleverpunt. Bij deel 1: vermeld duidelijk met wie je samen de DFD hebt gemaakt (mag evt. met je hele projectgroep) en met wie je eventueel als duo hebt samengewerkt. **Bij deel 2: dit is individueel!**

-----
<sup>*</sup> _Lees hier, afhankelijk van je gekozen richting, software engineer danwel network & security engineer._
