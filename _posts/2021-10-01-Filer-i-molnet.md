# Hur fungerar applikationen+

Jag gjorde både en console och en webapp där console appen laddar upp bilder och webappen ska visa dom.
Dock fungerar det inte som jag vill och tänkte gå igenom det här.

Console appen ser ut som nedan.

![image](/images/console1.PNG)
![image](/images/console2.PNG)
![image](/images/console3.PNG)

När appen körs så skriver man "upload" för att ladda upp, då får man sedan skriva i vägen till den lokala bild man vill ladda upp 
och slutligen vilken container i azure.
Metoden upload är det som sköter hela processen med uppladningen, problemet är att bilderna hamnar i azure och dom syns om man klickar edit.
Men dom syns däremot inte när man går in på dess url som bilderna nedan visar.
Trodde först att det hade med contentType att göra men trots att den är hårdkodad i metoden Upload så löser det sig inte.

![image](/images/azure-edit.PNG)
![image](/images/url-error.PNG)

Jag gjorde sedan en webapp som skulle visa dessa blobbar med Razor pages utan controller som i vår övning med databaser.
Det blir såklart samma problem då det är samma blobbar som skall visas men nedan är iallafall koden för hur jag hämtar dom.

![image](/images/webapp1.PNG)
![image](/images/webapp2.PNG)
![image](/images/webapp3.PNG)
![image](/images/webapp4.PNG)
![image](/images/webapp5.PNG)

Diagram för dataflödet.

![image](/images/blob-diagram.PNG)

## Vad skulle det kosta att driva applikationen?

Om vi skulle ha en applikation med 1000 användare och varje användare lägger upp 100mb / dag och som sedan laddas ner 3 gånger varje dag så skulle kostnaden bli runt $85. 
Nedan kommer bild med uträkningen:

![image](/images/kostnad1.PNG)
![image](/images/kostnad2.PNG)

## Hur håller Azure min data säker?

- i vila: Detta beskriver data som finns i molnet som för närvarande inte används. 
  Azure Storage använder SSE (Server-Side Encryption) för att automatiskt kryptera dina data när de finns kvar i molnet.
- i förflyttning: Detta beskriver dataöverföringar via internet, till exempel mellan vår app och molnlagringen eller annan dataförflyttning. 
  För att undvika avlyssning, snokande etc måste varje begäran skickas över HTTPS, som standard nekar alla andra förfrågningar.
- Key vault: Man kan också använda key vault för att förvara sina connectionstring säkert.
  dessa borde även bytas ut då och då för att inte knäckas, det kan göras automatiskt och det finns alltid två stycken av denna anledning.
 
## Referenser

- [Setting up Azure storage emulator](https://medium.com/oneforall-undergrad-software-engineering/setting-up-the-azure-storage-emulator-environment-on-windows-5f20d07d3a04)
- [Azure storage blob service using .NET console application](https://medium.com/@rammonzito/azure-blob-storage-using-a-net-core-console-application-106a0c2e6de5)


