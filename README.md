
# HAN ICA DWA Casus - Kwizzert
Gemaakt door: Jeffrey Haen & Jevgeni Geurtsen.

# Inhoudsopgave

1. [Systeemeisen](#systeemeisen)
1. [Schermontwerpen](#schermontwerpen)
1. [Communicatie protocol](#communicatie-protocol)
1. [Architectuur](#architectuur)
1. [Externe frameworks](#externe-frameworks)
1. [Code styling](#code-styling)


# Systeemeisen
Het Kwizzert systeem bestaat uit 3 single page web applicaties:

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
Alle schermontwerpen van de client-side applicaties zijn [hier](https://github.com/jeffreyhaen/ICA-Kwizzert-api/tree/master/wireframes) te vinden.


# Communicatie protocol
...


# Architectuur
Om het Kwizzert systeem te realiseren zijn twee applicaties ontwikkelt. De twee applicaties communiceren met elkaar wisselen data over websockets. Eén applicatie zal als server (api) dienen. De andere applicatie zal als client dienen en is afhankelijk van de server om zijn informatie op te halen en te versturen. De server heeft een connectie met een database om informatie vast te leggen.

## Applicaties

### Server
De server werkt gedeeltelijk als een REST api om onder andere nieuwe teams te kunnen registreren. Het andere gedeelte van de server zorgt ervoor om geselecteerde vragen en antwoorden tussen teams te communiceren met behulp van websockets.

- *Softwareplatform:* Nodejs, omdat het gebruik van Nodejs een vereiste van de opdracht is.
- *Websockets:* Socket.io, omdat het gebruik van websockets een vereiste van de opdracht is en we opzoek zijn naar een mechanisme dat oude browsers ondersteund en gemakkelijk te gebruiken is. Socket.io biedt deze mogelijkheden.
- *Database:* MongoDb, omdat we gegevens zoals, vragen, antwoorden en teams op willen slaan. Om snel te kunnen querien op deze data, willen we gebruik maken van een database.
- *Model validatie:* Mongoose, omdat we data validatie op één plek willen vastleggen. Daarnaast willen we hiermee voorkomen dat de database corrupte data bevat.

### Client
De client is opgedeeld in drie onderdelen, de Team-app, de KwizMeestert-app en de Scoreboard-app.

- *Softwareplatform:* Nodejs, omdat het gebruik van Nodejs een vereiste van de opdracht is.
- *User Interface framework:* React, omdat het gebruik van React een versite van de opdracht is.
- *User Interface styling:* Bootstrap, omdat we een gelikte weergave van de user interface willen bieden, zonder zelf al te veel styling te hoeven maken.
- *Code structure:* Redux, omdat op veel plekken een bepaalde toestand moeten bijhouden en opvragen. Met Redux kunnen we ervoor zorgen dat React componenten niet afhankelijk zijn van bepaalde data of user input.

## Modellen en data structuur
Onderstaand zijn de verschillende modellen te zien die in een model validatie framework zullen worden vast gelegd. Deze data structuur wordt ook op dezelfde manier in de database opgeslagen.

*Game*
{
    *MaxRounds*: Number,
    *Rounds*: [ref Round],
    *Teams*: [ref Team],
}

*Round*
{
    *Questions*: [ref Question],
}

*Category*
{
    *Name*: String,
}

*Question*
{
    *Category*: ref Category,
    *Name*: String,
}

*Answer*
{
    *Question*: ref Question,
    *Value*: String,
}

*Team*
{
    *Name*: String,
}


# Externe frameworks
Hieronder staan alle bewust gebruikte bibliotheken binnen het Kwizzert systeem (Server en Client).

- [React](https://facebook.github.io/react/)
- [Node.js](https://nodejs.org/)
- [Socket.io](https://socket.io/)
- [MongoDb](https://www.mongodb.com/)
- [Mongoose](http://mongoosejs.com/)
- [Redux](http://redux.js.org/)
- [Immutability-Helper](https://github.com/kolodny/immutability-helper)


# Code styling
Tijdens de ontwikkeling van zowel de kwizzert-api als de kwizzert app worden dezelfde code style conventies gebruikt. Het idee is om zoveel mogelijk gebruik te maken van de [felixge - node style guide](https://github.com/felixge/node-style-guide).
De code wordt volledig in het Engels ontwikkelt.