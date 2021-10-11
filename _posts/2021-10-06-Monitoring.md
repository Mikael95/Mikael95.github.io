## Applikationen

Detta är en utveckling av den tidigare web applikationen för musik.

## Diagram
Här är ett diagram över hur azure tjänster är ihopkopplade.

![image](/images/diagram.PNG)

Man kan också se olika requests som gjorts och responstider med application map i sin application insight.

![image](/images/requests.PNG)

## Koden

Till att börja med så har jag lagt till lagt till nugetpaketet [Microsoft.ApplicationInsights.AspNetCore.](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore)
sedan behövs kodraden "services.AddApplicationInsightsTelemetry();" i Startup.cs i ConfigureServices metoden.

![image](/images/configureservice.PNG)

Jag har sedan lagt till min instumentationkey och loggningsinställningar i min appsettings fil.

![image](/images/appsettings.PNG)

InstrumentationKey hittas i din azure portal i application insights resursen under overview.

![image](/images/key.PNG)

Jag har sedan lagt till raden "@inject Microsoft.ApplicationInsights.AspNetCore.JavaScriptSnippet JavaScriptSnippet" i _ViewImports.cshtml
och @Html.Raw(JavaScriptSnippet.FullScript) i _Layout.cshtml inom <head> för att injecera nödvändiga scripts.

Här är en bild över diagnostiken när applikationen används.
  
![image](/images/live-diagnostics.PNG)
  
## Querys
  
Den första queryn visar hur lång tid våra requests tar.
  
![image](/images/query1.PNG)
  
Den andra visar vart vår trafik kommer ifrån, 100% från Sverige antar jag men det står dock inte av okänd anledning.
  
![image](/images/pie.PNG)
  
## Säkerhet
  
Det kan hjälpa mycket för säkerheten med loggning då man skan se allt som gärs i applikationen.
Till exempel om de försökst komma åt information med fel nycklar många gånger så tyder det kanske på att en obehörig
försöker hämta den informationen som tex bruteforce.
Det kan ju också bli användbart för företag med känslig data att kunna logga va de anställda gör i denna applikationen
och om det är vad de borde göra.
  
## Källor
  
- [Application Insights for ASP.NET Core applications](https://docs.microsoft.com/en-us/azure/azure-monitor/app/asp-net-core)
- [What is Application Insights?](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview)

