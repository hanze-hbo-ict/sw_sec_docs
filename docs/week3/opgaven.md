# Opgaven week 3: secure software development

Deze week gaan we bezig met een technische opgave én doen we zelfstandig onderzoek naar een belangrijke vraag voor de praktijk: wat is de toegevoegde waarde van security tooling?

## Deel 1: problemen oplossen in een webapplicatie

[Hier](https://github.com/hanze-hbo-ict/sw_sec_docs/tree/master/src/pract-wk3/vulnerable-webapp/) hebben we een eenvoudige python/flask-webapp klaargezet, met drie grote kwetsbaarheden erin. Het is de bedoeling dat je deze kwetsbaarheden opspoort en voor elk een mitigatie aanbrengt in de code. Lees eerst de README en zorg dat de app up-and-running is. Voor Windows-gebruikers: deze app hoef je *niet* in WSL of als Docker-container te draaien.
De kwetsbaarheden betreffen:

* De manier waarop wachtwoorden worden opgeslagen;
* CSRF op het stemformulier;
* _Authorization bypass_, ook wel bekend als [Insecure direct object reference](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html), in bepaalde URL's.

Dat je anoniem mag stemmen is **niet** één van de drie bugs. Kom je er niet uit? Overleg met klasgenoten en/of de practicumdocent.

Laat je oplossing zien d.m.v. screenshots van de code, vóór en na je bugfix. Geef bij elk van de screenshots duidelijk aan om welke bug het gaat en highlight de relevante code. Je mag je uitwerking samengevoegen met die van deel 2 in één document en liefst als pdf inleveren via het Inleverpunt.

## Deel 2: onderzoek naar security tooling

Software-ontwikkelingsprojecten bestaan uit meerdere stappen en omvatten meer dan alleen ontwikkeling en testen. Bij elk project moet bijvoorbeeld rekening worden gehouden met regionale en internationale wetgeving en standaarden, die impact kunnen hebben op de requirements van het project. Deployment en onderhoud zijn daarnaast ook onderdeel van het proces van softwareontwikkeling en in moderne omgevingen maken DevOps-teams (een werkmethode waarbij development en onderhoud & support door hetzelfde team worden uitgevoerd) de grens tussen Software Security en IT Security nog waziger. 

Tijdens deze opdracht kijken we naar de rol die security tooling kan vervullen in een project en voor welke aspecten het minder of helemaal niet nuttig is. Het is voor een bedrijf namelijk heel makkelijk om veel geld uit te geven aan tooling die in de praktijk weinig toegevoegde waarde heeft, maar tegelijkertijd zijn sommige aspecten van software security alleen mogelijk met gebruik van de juiste tooling. 

### Opdracht 1

Voor je begint met je daadwerkelijke analyse is het bijzonder handig om wat extra informatie tot je te nemen. Lees vooral eens onderstaande bronnen door:

 * De [BSIMM software security activity list](https://www.blackduck.com/services/security-program/bsimm-maturity-model.html) is een software-security-framework dat in de praktijk vaak gebruikt wordt. Het framework is onderverdeeld in vier domeinen met elk drie aspecten van het softwareontwikkelingsproces. Onder elk van deze aspecten kun je vervolgens lezen over de verscheidene activiteiten die in de praktijk worden gebruikt. 
 * In [deze whitepaper van de versimpelde implementatie van Microsofts SDL](https://www.microsoft.com/en-us/download/details.aspx?id=12379) kun je lezen over de verschillende eisen die Microsoft stelt aan hun eigen ontwikkelproces. 

Niet alles wat in deze bronnen staat is trouwens per se een goed idee en je moet ze vooral ook niet interpreteren als een harde eis waar elk softwareontwikkelingsproject aan moet voldoen. Het zijn meningen en voorbeelden - al zijn het meningen en voorbeelden van teams met ervaring. Probeer tijdens het lezen van de bronnen alvast te denken aan hoe je de informatie kunt gebruiken om deze opdracht te maken. Hiervoor beantwoord je de volgende vragen:

1. Zijn er activiteiten binnen het softwareontwikkelingsproces waar vaak tooling bij wordt gebruikt? Waarom is dit, denk je? 
2. Zijn er ook activiteiten waar juist weinig of geen tooling wordt toegepast? Wat is de overeenkomst tussen deze activiteiten? 

### Opdracht 2

Kies één (commerciële of niet-commerciële) tool die zich richt op het verbeteren van software security. Hieronder staat een lijst met voorbeelden om uit te kiezen, maar je bent vrij om zelf een andere tool te zoeken. Sommige zijn voorzien van een link die je als startpunt van je leerproces kunt gebruiken. Let er wel op dat, wanneer je zelf een tool kiest, dit er een is die een directe impact heeft op softwareontwikkeling of -onderhoud. Kies dus niet iets als een firewall, VPN, IDS of antivirussoftware. Bij twijfel kun je altijd aan je docent vragen of de tool geschikt is.

**Vulnerability Scanners**

 * [Acunetix](https://www.softwaretestinghelp.com/acunetix-web-vulnerability-scanner-wvs-review/)
 * [Nessus](https://medium.com/@PenTest_duck/offensive-nessus-installation-simple-windows-vulnerability-scanning-2d4d707859ae)
 * OWASP ZAP (is toegestaan, maar omdat deze tool al enigszins bekend is, verwachten we hier wel wat extra diepgang)

**Security Testing Frameworks**

 * [Metasploit](https://medium.com/swlh/intro-to-metasploit-19e3d07ff725)

**[Static Analysis](https://unicorn-dev.medium.com/the-way-static-analyzers-fight-against-false-positives-and-why-they-do-it-743de1f2a1bd)**

 * [PyLint](https://medium.com/@ryangordon210/build-a-python-ci-cd-system-code-quality-with-pylint-f6dea78461c6)
 * [Coverity](https://www.synopsys.com/blogs/software-security/coverity-setting-the-standard/)
 * [snyk](https://eldadfux.medium.com/this-is-how-we-use-snyk-to-protect-our-open-source-projects-from-evil-dependencies-6ee258ca5815)
 * [SonarQube](https://betterprogramming.pub/how-to-improve-code-quality-with-sonarqube-465744eb66db)
 * [Veracode](https://medium.com/@AccompliceVC/the-veracode-journey-origin-and-introspection-13c0c74b82e2)

**Source code compliance scanners / Software Composition Analysis (SCA)**

 * [Black Duck](https://www.synopsys.com/software-integrity/security-testing/software-composition-analysis.html)

**Threat Modeling Tools**

 * [Attack Trees](https://medium.com/@tashjnorris/using-threat-models-for-incidents-and-how-incidents-helped-me-like-attack-trees-a27eb65f9039)
 * [Microsoft SDL](https://www.youtube.com/watch?v=wUt8gVxmO-0)

**Configuratiecheckers**

 * [testssl.sh](https://www.blackhillsinfosec.com/testssl-sh-assessing-ssltls-configurations-at-scale/)
 * Docker Bench for Security

**Load-testers**

 * Zie [https://theqalead.com/tools/load-testing-tools/]( https://theqalead.com/tools/load-testing-tools/)

**Modellen (beide aangestipt in de kennisclips)**

 * [BSIMM](https://www.synopsys.com/software-integrity/software-security-services/bsimm-maturity-model.html)
 * [OWASP SAMM](https://owaspsamm.org/)

Verdiep je na het selecteren van een tool in de functionaliteit ervan d.m.v. featurelists, whitepapers, handleidingen, demovideo’s, Medium-artikelen etc. Let hierbij op de redenen die worden gegeven waarom je het product zou moeten gebruiken, wat het precies doet (bijv. alleen "scanning" is een nogal vage term) en wat de tool belooft op te leveren. 

3. Welke tool heb je onderzocht en in welk deel van het softwareontwikkelingsproces kan de tool het beste worden toegepast (bijv. requirements, ontwerp, realisatie, testen, deployment, onderhoud)? Waarom juist daar en niet een ander deel?
4. Noem een werkzaamheid **binnen dit deel van het softwareontwikkelingsproces** die wel moeten gebeuren, maar waar de tool **niet** bij helpt. Waarom past de tool hier niet bij? 
5. Leg kort uit hoe de tool werkt vanuit een technisch perspectief. M.a.w.: omschrijf de onderliggende technieken die de tool gebruikt om zijn functionaliteit te leveren. *Bijvoorbeeld: Radamsa is een generator voor fuzzing-testcases. Deze tool werkt door a.d.h.v van een set mogelijke wijzigingen (e.g. bit flipping, byte insertion, line deletion, etc.) een gegeven string te muteren. Door vele verschillende versies van deze mutaties te genereren bouwt Radamsa een representatieve set mogelijke mutaties van een realistische inputstring.*
6. Wat voor risico’s helpt te tool om te voorkomen? Noem tenminste één voorbeeld van een risico. Onderbouw je antwoord door uit te leggen hoe de functionaliteit van de tool leidt tot mitigatie van het genoemde risico. In het (onwaarschijnlijke) geval dat de tool geen enkel risico afdekt: onderbouw hoe je tot die conclusie bent gekomen.
7. Met wat voor problemen zul je rekening moeten houden je als je de tool wilt toepassen in een echt project? En belangrijker: waarom verwacht je deze problemen tegen te komen? Noem tenminste één probleem en licht toe. *(Voorbeelden van dergelijke problemen zijn: er is veel specialistische kennis nodig om te tool te gebruiken; kan de tool opschalen voor grotere organisaties; is het veel werk om de tool überhaupt op te zetten; zullen developers de tool willen gebruiken gezien de tijdsdruk waar ze onder werken; vertraagt het andere onderdelen van het ontwikkelproces; kost het veel handmatig werk om te gebruiken of in de bestaande ‘toolchain’ te integreren; past de tool binnen een agile werkproces; etc.)*

### Hoe moet je het inleveren?

Kopieer de eerste twee vragen en geef daarop antwoord. Beantwoord daarna de 5 vragen over de tool. Kopieer de vragen en schrijf je antwoord daar direct onder. Je hoeft slechts een paar zinnen per vraag te schrijven, maar **let erop dat je antwoord duidelijk laat zien dat je een doordachte analyse hebt uitgevoerd**. N.B.: zorg dat je in je antwoord geen tekst van de promotie-/informatiematerialen van de tool kopieert. Er geldt geen minimumlengte, zolang je maar zorgt dat je antwoorden goed onderbouwd zijn en aantonen dat je onderzoek hebt gedaan.

De beide verslagen (deel 1 en 2) mogen worden samengevoegd in één document en liefst als pdf worden ingeleverd via het Inleverpunt.

Wat betreft het gebruik van AI: het is niet toegestaan om je antwoorden te laten genereren, het dient eigen werk te zijn. Hier zal ook op gecontroleerd worden. Wat wel mag, is deelvragen voorleggen aan een AI en de antwoorden hierop, voorzien van bronvermelding en eigen reflectie, mee te nemen in je antwoorden.

Voor **herkansers** geldt dat zij een andere tool dan het voorgaande jaar dienen te kiezen! Hierop zal gecontroleerd worden.