## Vad är serverless?

På namnet så låter det kanske som man kör program utan att använda sig av en server, men så är inte fallet. Med “Serverless” är hur en server hanteras samt implementeras och är något som hanteras av molnbaserade leverantörer. Servern/servrarna hanteras alltså istället av en leverantör och inte från företaget som utvecklar sin app. På detta viset, så slipper företaget som hyr servern att underhålla, utveckla, uppdatera och hantera vanliga infrastrukturuppgifter.

Serverless arkitekturen håller aldrig berkäkningsresurser i instabila minnen, utan beräkningsresurserna tar plats i små partier. Låt säga att i fall man inte använder en applikation, så kommer inga resurser att tilldelas till servern. Med detta så betalar man för det man använder och det blir kostnadseffektivt för företaget.

## Fördelar med serverless

### Kostnadseffektivt
Som jag var inne på tidigare, så blir det billigare för ett företag att använda sig av serverless. Man betalar för det man använder och slipper då onödiga kostnader som att betala för appar som man inte använder längre. Molntjänstleverantören tar bara betalt utav dig för minnet som används och tiden som koden körs och inte för appar som är inaktiva.

### Snabbare appdistribution

Utvecklarna behöver inte köra backend konfigurationen eller ladda upp kod till servern för att distribuera en ny version av appen. Man har också flexibiliteten att distrubuera ny kod direkt efter varandra eftersom det inte är någon sluten arkitektur. Utöver ovanstående, så kan man även uppdatera, lägga till nya funktioner och fixa fel i appen väldigt snabbt.

### Produktivet

Eftersom utvecklarna själva inte behöver fixa serverhanteringen, så sparar man tid och blir mer effektiva.

### Skalbarheten

“Serverless” system erbjuder en hög grad av skalbarhet, eftersom man kan skala upp eller ned baserat på applikationens behov för stunden. Leverantören sköter den automatiska skalningen vilket gör att utvecklarna kan fokusera på annat. Utvecklare i mindre team kan köra sin kod självständigt utan att behöva stöd eller infrastruktur.

## Nackdelar

### Säkerhet

När man använder sig av “Serverless computing” så har man inte själv kontrollen från leverantören som man använder. Det medför att det är riskabelt när hela företagets backend med känslig information är sparade på en sådan server.

### Prestanda

Ibland kan kod som körs mindre få en viss fördröjning än kod som körs kontinuerligt på mjukvaru containrar, dedikerade servrar och virtuella maskiner. Det tar tid för servern att starta om och skapar då ännu mer fördröjning på applikationen att starta / svara.

### Testa och felsöka

Man behöver veta hur sin kod presterar när man har distrubuerat den och för det så behöver man testa koden, vilket är svårt i en “serverless” miljö. Eftersom utvecklarna också inte har kontroll över varje backend process, samt att applikationer är uppdelade i mindre funktioner så blir felsökningen även problematisk.

## Vad är FaaS?
Faas står för “Function as a Service” vilket är en molntjänst där utvecklare kan bygga, köra och hantera applikationspaket som funktioner utan att behöva underhålla deras egna infrastruktur.
Faas är en händelsestyrd modellteknik som kör “stateless” containers och dessa funktioner hanterar server-side logik och “state” genom användningen av tjänster från en Faas leverantör.

## Faas och serverless

Faas är ett sätt att implementera “serverless computing” då utvecklare kan skriva business logiken som sedan körs i Linux containers och hanteras av en plattform. Vanligtvis så körs molnbaserade tjänster av en molnbaserad plattform men denna modell utvecklas hela tiden så att man kan köra denna modellen även lokalt och med hybriddistrubution.
En funktion är en del av en mjukvara som kör business logiken på ett operativsystem. Applikationer kan bli kombinerade av många olika funktioner. Att använda Faas-modellen är ett sätt att bygga en app med arkitekturen från “Serverless”.
FaaS ger utvecklare en abstraktion av att köra webbapplikationer som ger svar från händelse, utan att man behöver hantera servern. Som ett exempel så kan man ladda upp en fil som utlöser kod som sedan konverterar filen till många olika format.

## Vår kalkylator
Här är koden för vår kalkylator:
![image](/images/kalkylator_1.PNG)

![image](/images/kalkylator_2.PNG)
de första raderna på bilden ovan gör att vi kan skriva in ett namn för requestet och sedan kalkylera ett uttryck. Man kan ta bort name parametern, men vi valde ha kvar den bara för att skicka ett litet meddelande.

num = första numret som man fyller i
op = Vilken operator man kör, exempelvis * / + eller -
num2 = Det är andra numret som ska beräknas.
Val av namn på variablerna är inte optimala, men vi valde att inte lägga större fokus på det.

Vi har gjort en switch-sats för att man skall kunna välja vilken operator som ska beräkna de två talen. Först och främst, så skapade vi ju variablen op som en sträng. Initu switch-satsen så konverterar vi de strängarna som ska räkna ut summan och gör om num och num2 till datatypen int.

Sedan skickar vi resultatet till strängen responsemessage och där har vi enkelt valt att bara skriva ut “Hello , = . Detta ser ni även på bilderna ovan.

Här är switch-satsen:

![image](/images/kalkylator_4.PNG)

För att skapa denna HTTP trigger, så har vi först gått in och skapat en ny resurs inne i Azure portalen.

![image](/images/kalkylator_6.PNG)

Efter ha skapat resursen och funktions appen, så går man in på funktionsappen och får upp följande meny:

![image](/images/kalkylator_7.PNG)

Här klickar man på funktioner och sedan skapa. Då kommer det upp en lista med mallar på vilken trigger man vill skapa. I detta fallet skulle vi skapa en HTTP trigger, som då utlöses vid ett GET/POST request.

![image](/images/kalkylator_8.PNG)

## Hur har vi testat applikationen / Säkerhet?

Vi har bara skrivit in olika uträkningar och kollat om de stämmer så inga direkta test. säkerhet har vi inte heller tänkt över nått särskillt för.

