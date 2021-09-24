## Databaser i molnet.

### Vad gör våran applikation?
Vi har skapat en rätt minimal applikation som kan läsa data och lägga till data till en cosmos databas.
Vi har fått många problem och prövat flera olika allternativ så vi har låtit det vara minimalt.

Ett exempel på när vi använder POST i postman:

![image](/images/PostBody.PNG)

I bodyn fylls det som vanligt i den data som behövs, i detta fall band och artist.
Man kan också göra ett get request som ger all data i databasen som syns nedan.

![image](/images/BodyResult.PNG)

## Beskriv koden

POST metod:

![image](/images/kodexempel.PNG)

GET metoden:

![image](/images/kodexempelGET.PNG)

BandModel klassen:

![image](/images/BandModel.PNG)

Vi har en klass som heter BandModel för att kunna lägga till object att spara till databasen.
Den har ett autogenererat id och bandnamn samt artistnamn.

## Databasen

Databasen gjordes i azure portal genom att skapa ett konto för cosmosDB och skapa ny databas. 
Därifrån väljer man bara namn och containernamn samt patitionkey om man så vill.

## Uppdatering / Ändring av databas

Inte funderat på det ännu, har inte riktig hunnit med det.

## Vad kostar det att driva ?

![image](/images/pris.PNG)
