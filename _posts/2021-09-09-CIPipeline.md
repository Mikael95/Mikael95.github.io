## Vad är en CI pipeline?

En CI pipeline är en rad med steg som måste göras i en viss ordning för att leverera en mjukvara.
Continuous intergration (CI) är en metod som fokuserar på att förbättra leveransen av en mjukvara 
när man använder sig av Devops eller SRE kultur.

Steg i en CI pipeline:
- Build - Applikationen kompileras.
- Test - När koden testas, gärna automatiserat.
- Release - Applikationen levereras till sitt repository.
- Deploy - Applikationen lanseras för användning.
- Validation and compiance - Applikationen valideras och testas så att den möter kravbilden.

![image](/images/CI_Pipeline.jpeg)

## Implementering av CI pipeline i eget Github repo

Jag och Kevin implementerade en action i spacepark v1 från tidigare kurs.

Vi följde dessa steg:

- Forkade projektet till eget repository
- Gjorde ett workflow, genom att skapa ny mapp som heter .gitub/workflows.
- Inuti action-filen så började vi med att lägga till att en action sker efter varje commit (on: push)
- Skapade upp en build som sedan körs på senaste ubuntu versionen.
- Ställde in vilken version av dotnet som ska köras, blev 5.0, då det är den versionen som projektet kördes på.
- Sist ställde vi för att kunna köra två olika actions på samma fil (SpacePark/sln).

![image](/images/git_action.PNG)

