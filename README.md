
# HAN ICA DWA Casus - Kwizzert
Gemaakt door: Jeffrey Haen & Jevgeni Geurtsen.

# Requirements
De Kwizzert bestaat eigenlijk uit 3 single page web applicaties:

### De Team-app. 
Deze SPA draait op de smartphones van de teams. Deze app kan twee dingen:
- De telefoon (en daarmee het team) aanmelden bij de Kwiz-avond. Een onderdeel van aanmeldprocedure is dat het team een naam voor zichzelf instuurt, en dat de KwizMeestert de aanmelding moet accepteren.
- De huidige vraag tonen, en het team de gelegenheid geven een antwoord in te voeren en in te sturen.

### De KwizMeestert-app. 
Deze SPA draait op de tablet van de KwizMeestert. Hij/zij kan daarmee de volgende taken uitvoeren:
- De Kwiz-avond starten, en openstellen voor aanmeldingen van (smartphones van) teams.
- Aanmeldingen van teams accepteren of weigeren.
- De feitelijke Kwiz starten zodra alle teams zich hebben aangemeld.
- Een Kwiz-ronde (van 12 vragen) starten door uit een menu 3 categorieën te selecteren, en dan op de knop “Start Ronde” (o.i.d.) te drukken.
- Na afloop van een ronde te kiezen of er nog een ronde gestart wordt, of dat de Kwiz-avond beëindigd wordt.
- De KwizMeestert de volgende vraag te laten kiezen. Dit is een interessant schermpje, dat hieronder nader wordt toegelicht onder het kopje User Interface.
- De gekozen vraag starten door op een knop te drukken. Pas dan wordt de vraag getoond op het Scorebord of in de Team-app. Vanaf dat moment kunnen teams hun antwoorden insturen, totdat de KwizMeestert de vraag weer sluit, ook door op een knop te drukken.
- De antwoorden van de teams ter goedkeuring voorleggen aan de KwizMeestert. De KwizMeestert kan zo zelf beslissen of hij/zij antwoorden met spelfouten toch goedkeurt, bijvoorbeeld.

### De Scorebord-app. 
Deze app heeft geen eigen interactie, maar toont, real-time:
- de voortgang: hoeveelste ronde zitten we in, en de hoeveelste vraag van deze ronde.
- de namen van de teams, met daarbij de scores in “rondepunten”, en het aantal goede vragen in deze ronde. Rondepunten worden als volgt verdiend: Na iedere ronde van 12 vragen, krijgt het team dat de meeste vragen goed had 4 ronde punten. Het team dat op één na het meeste vragen goed had krijgt 2 rondepunten, en het team dat op twee na het beste was krijgt nog 1 rondepunt. Alle andere teams krijgen 0.1 rondepunt voor de moeite en de gezelligheid.
- Als er een vraag “loopt” (hij is gestart en nog niet gesloten: teams kunnen nog antwoorden insturen), dan toont het scorebord: de vraag, de categorie waar de vraag bij hoort en welke teams al een antwoord hebben ingestuurd (niet de antwoorden zelf).
- Zodra een vraag gesloten is, toont het scorebord de antwoorden, en wanneer de KwizMeestert een antwoord goed of afkeurt wordt dat ook zichtbaar, en worden de team-scores bijgewerkt.

### Algemeen

- Iedere vraag wordt, tijdens een Kwiz-avond maar één keer gesteld. Als een vraag gesteld is, komt-ie ook niet meer voor in de vragen die aan de KwizMeestert worden voorgesteld. (Categorieën kunnen wel meer dan in meer dan één ronde per Kwiz-avond voorkomen).
- Twee teams mogen niet dezelfde naam hebben. Team-namen mogen niet leeg zijn.
- Nadat een team een antwoord heeft ingestuurd, mag het zich bedenken. Dan kan het team een tweede antwoord insturen, zolang de KwizMeestert de vraag nog niet gesloten heeft. Het laatst ingestuurde antwoord telt.
- Lege antwoorden worden genegeerd door de app. Als een team per ongeluk een leeg antwoord instuurt, dan wordt dat niet aan de KwizMeestert of op het Scorebord getoond.
- Zodra de KwizMeestert de Kwiz-avond afsluit, Toont het scorebord de namen van de teams die nummer 1, 2 en 3 zijn geworden (gemeten aan het aantal rondepunten dat ze gehaald hebben). In dat “slotscherm” ligt er een visuele nadruk op de naam van het team dat nummer 1 werd.

# Schermontwerpen


# Communicatie protocol


# Architectuur


# External libraries


# Code style

