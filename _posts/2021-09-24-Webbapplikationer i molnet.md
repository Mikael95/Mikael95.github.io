## Webapplikationen

Applikationen är en utveckling av den förra musikdatabasen nu i form av en ASP .NET Core Web App.
Funktionen är samma som förut att man kan visa innehållet i databasen och att kunna lägga till nya låtar.
Man kan besöka websidan [här](https://songlibrary.azurewebsites.net/).

## Koden

Kortfattad förklaring av programmets funktion.

![image](/images/song_model.PNG)

Detta är modellen som används för att definera hur ett "song objekt" ser ut.

![image](/images/services.PNG)

Då detta inte är ett api emot azure så har jag en klass som heter CosmosDbServices för att skapa en cosmos client och hantera läsning och skrivning till databasen.
denna kod är hämtad [härifrån](https://docs.microsoft.com/sv-se/azure/cosmos-db/sql/sql-api-dotnet-application).
Den innehåller även ett interface som syns nedan.

![image](/images/services_interface.PNG)

![image](/images/appsettings.PNG)

Connectionstring och nycklar till databsen behövs även läggas till i appsettings.json som syns ovan.
nycklarna hittas i azure portal i din databas som visas i bilden nedan (Microsoft exempelbild, ej min databas).

![images](/images/cosmos_key.PNG)

I startup.cs har jag fått lägga in en metod som heter "InitalizeCosmosInstanceAsync" som gör som den heter att skapa cosmos clienten vid start.

![image](/images/startup_initializeclient.PNG)

Samt att använda dependency injection med enna metod i ConfigureServices.

![images](/images/configureservice.PNG)

I Razor Pages ser det ut så här för att hämta alla låtar async.
Inte så mycket som händer, allt hämtas med en query och läggs i en lista av model klassen för låtar (Item).

![image](/images/allsongs.PNG)

För att lägga till en ny låt skapas en ny instans av vårt song objekt (Item) och tilldelas alla variabler som ligger i cshtml filen och visas under bilden nedan.

![image](/images/addsong.PNG)
![image](/images/html_addsong.PNG)

## Hur har vi fått applikationen att köra i Azure app service?

## Brons

För brons har jag deployat den från vs code i azure extension.

![image](/images/brons_deploy.PNG)

På "molnknappen" väljer man att deoplya och har man inte gjort en app service ännu så kan man enkelt göra de därifrån i code.

## Silver

Jag gjorde först en dockerfil som syns nedan, sedan ett workflow som jag tyvärr inte kan visa då den är ändrad sedan dess i ett försök till guldnivå.
Men detta workflowet byggde en imige av appen och sparade den i github packages som andra bilden visar.

![image](/images/dockerfile.PNG)
![image](/images/package.PNG)

Jag gjorde de också manuellt med vs code som test genom att skapa en docker image med Ctrl + shift + p "build image".
I docker extenion får man då en ny image och då är de smidigt att tagga den med något namn, man kan sedan välja att pusha den till antingen Docker hub
eller Azure (För azure behövs det först göras ett container regisrty).
Man kan sedan välja att "deploya" sin image till en azure app service, för detta krävs dock ett context för azure i docker.
Har man inget kommer vs code fråga om man vill skapa ett, i bilden nedan syns de olika fälten för denna beskrivning i vs code.

![image](/images/vs-code_deploy)

## Guld

Jag har tyvärr inte fått detta steget att fungera fullt ut. Men första versionen gjorde jag om min workflow så att mi docker image pushades till mitt container registry.
Därifrån fick jag sedan skapa en app service utifrån imagen, så det blev inte helautomatiskt.
andra versionen var att i min app service under deployment center välja att göra en github action. Detta kopplades då till mitt repo och genererade ett workflow
som skulle få appen att pushas direkt till min app service. Det gav ändå inte någon direkt push till app servicen av någon anledning jag inte vet ännu.
Detta syns på bilden nedan.

![image](/images/azure_github-action.PNG)

Tredje versinen var att göra ett container registry under samma flik (deployment center) och välja en specifik image och och dess tag.
Detta gav en webhook som jag kunde lägga till i mitt repo och som var meningen att denna imagen skulle pushas till azure app servicen i samband av push till main.
Fick tyvärr inte heller detta att fungera av hittills okänd orsak, container regisrty och webhook syns i bilder nedan.

![image](/image/azure_webhook.PNG)
![image](/image/github_webhook.PNG)

Senaste försöket gjorde jag istället ett workflow som skulle pusha själva web appen utan docker image direkt till min app service med ett workflow som syns nedan.
detta har tyvärr inte heller lyckats trots att min action går igenom utan fel. Workflow syns på bild nedan.

![image](/image/latest_workflow_deploy.PNG)

## kostnad

För 400 RU/S i 750 timmar med ett pris på $0,008 per 100 RU/S i timmen blir den genosnittliga månadskostnaden $23.
Med samma prismodell fast med 40000 RU/S blir det ca $2350 i månaden.

## Referenser

[ASP .NET Core MVC app med azure cosmos DB](https://docs.microsoft.com/sv-se/azure/cosmos-db/sql/sql-api-dotnet-application)
[Deploy to azure app service](https://code.visualstudio.com/docs/containers/app-service)
[Distribuera en anpassad container till App Service med GitHub Actions](https://docs.microsoft.com/sv-se/azure/app-service/deploy-container-github-action?tabs=publish-profile)
[Kontinuerlig distribution med anpassade containrar i Azure App Service](https://docs.microsoft.com/sv-se/azure/app-service/deploy-ci-cd-custom-container?tabs=private&pivots=container-linux)
