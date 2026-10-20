# Hydra-instructies voor Windows-gebruikers

## WSL installeren (1)

Windows-gebruikers moeten eerst het [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install) (WSL) installeren. De standaard-distributie, Ubuntu, is prima. Na installatie beschik je over een Linux-prompt en kun je onderstaande opdrachten uitvoeren (en nog veel meer - zo heb je WSL nodig om Docker, waar we volgende week mee bezig gaan, te kunnen draaien). [Wargames van Over the Wire](https://overthewire.org/wargames/) is een web-app waar je interactief veel over het gebruiken van verschillende Linuxtools kunt leren. Een must voor ICT'ers. Advies is om te beginnen met de Bandit-wargame. Lees [hier](https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/) hoe je bestanden van en naar je Linux-omgeving kunt kopiëren.

### Mogelijke problemen en oplossingen bij WSL

Heb je WSL al geïnstalleerd maar krijg je de melding "Windows Subsystem for Linux has no installed distributions"? Probeer het volgende commando te geven (op de commandline): ``wsl --install -d ubuntu``

Mocht je tijdens het clonen van een Github-repository de foutmelding "Unable to resolve github.com in WSL" krijgen, dan de volgende stappen doorlopen om de default nameserver aan te passen:

* ``sudo nano /etc/wsl.conf``
* voeg toe:
```
[network]
generateResolvConf = false
```
* ``sudo nano /etc/resolv.conf``
* comment originele nameserver uit (met #)
* voeg toe:
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```
* Opnieuw proberen, of bijv. eerst 'ping google.com'

## Hydra installeren (2)

We beginnen nu met de installatie van [Hydra](https://github.com/vanhauser-thc/thc-hydra). 

Allereerst willen we er zeker van zijn dat alle relevante packages goed geïnstalleerd en up-to-date zijn. De eerste stap is om de package-manager zelf te updaten.
```
sudo apt update
sudo apt install libssl-dev libssh-dev libidn11-dev libpcre3-dev libgtk2.0-dev libmysqlclient-dev libpq-dev libsvn-dev
```
<!-- Mochten git, gcc en/of make nog niet geïnstalleerd zijn, installeer deze dan eerst via je package manager (bijvoorbeeld Ubuntu Linux of WSL: ``sudo apt-get install git gcc make``). -->

De makkelijkste manier om Hydra te installeren is als package:
```
sudo apt install hydra-gtk
```

## Webapp runnen vanuit WSL (3)
Je hebt voor deze opdracht twee opties: je kunt de wachtwoorden van je eigen webapp kraken, of die van een [voorbeeldapp](https://github.com/hanze-hbo-ict/sw_sec_docs/tree/master/src/pract-wk1). 
### Voorbeeldapp
[Hier](https://github.com/hanze-hbo-ict/sw_sec_docs/tree/master/src/pract-wk1) kun je een voorbeeld van een slecht beveiligde webapp vinden die je mag kraken als je, om wat voor reden dan ook, vast loopt met je eigen app. Deze app kun je downloaden als [image op DockerHub](https://hub.docker.com/r/tomerikroos/webapp-hydra), of via git:
```
git clone https://github.com/hanze-hbo-ict/sw_sec_docs.git
cd sw_sec_docs/src/pract-wk1
ls
```
Nu zie je onder anderen de app zelf (app.py) en een requirements-file (requirements.txt). We raden aan om een virtual environment aan te maken:
```
python3 -m venv myenv
source myenv/bin/activate
```
en daarin alle requirements uit requirements.txt te installeren:```python3 -m pip install -r requirements.txt```
Nu kun je de app runnen met ```python3 app.py```.

Vraag eventueel je werkcollegedocent om hulp om de app aan de praat te krijgen.

### Eigen webapp
Ga in je Linux-terminal naar de juiste map (bijv. ``cd /mnt/c/Users/user/swsec/pract-wk1``) en start daar de applicatie (bijv. ``python3 app.py``). Het is aan te raden om eerst een aparte virtual environment aan te maken en daarin de requirements voor je webapp te installeren. Dit werkt grotendeels hetzelfde als onder Windows, alleen de activatie van de venv gaat anders: ``source my_venv/bin/activate``.

## Hydra draaien op een webapp (4)
Ga nu terug naar de [opgaven](https://hanze-hbo-ict.github.io/sw_sec_docs/week1/opgaven.html) en volg de instructies voor het draaien van hydra op de webapp die je in WSL hebt draaien. 