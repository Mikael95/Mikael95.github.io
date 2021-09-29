## Webapplikationen

Applikationen är en utveckling av den förra musikdatabasen nu i form av en ASP .NET Core Web App.
Funktionen är samma som förut att man kan visa innehållet i databasen och att kunna lägga till nya låtar.
Man kan besöka [här](https://songlibrary.azurewebsites.net/).

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
nycklarna hittas i azure portal i din databas som visas i bilden nedan.

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

Jag gjorde ett 
