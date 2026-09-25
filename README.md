# Gissa talet

Du bygger ett litet spel där spelaren gissar ett tal mellan 1 och 20 och får veta om gissningen är för låg, för hög eller rätt. Idén är inspirerad av Project 31, *Guess the Number*, i Al Sweigarts *The Big Book of Small Python Projects*. Instruktionerna och startkoden här är skrivna för den här kursen.

Arbeta i ordning och kör programmet efter varje steg. Det är helt okej att stanna vid ett fungerande steg och fortsätta senare. Steg 1–7 bygger grundspelet. Steg 8 förbättrar hanteringen av gissningar utanför intervallet. Steg 9 är frivilligt.

## Kom igång

Om du fått projektet som en GitHub-template: välj **Use this template**, skapa ett eget **Private** repository och klona **ditt eget** repository. Öppna mappen i VS Code och använd en terminal i mappen som innehåller `guess_the_number.py`.

Kör startfilen med:

```text
python guess_the_number.py
```

På Windows kan kommandot i stället vara `py guess_the_number.py`; på vissa datorer `python3 guess_the_number.py`. Startfilen skriver ut `Guess the Number` och avslutas. Den innehåller ännu inget färdigt spel. Du behöver bara Python, inga extra paket. Om något inte fungerar, se [HJALP.md](HJALP.md).

Efter ett fungerande steg kan du spara arbetet med en `commit`. Meddelandena nedan är förslag. Om du arbetar i ditt eget GitHub-repository kan du sedan göra `push`. Skriv gärna kort i [REFLECTION.md](REFLECTION.md) medan du arbetar.

## Steg 1 – två fasta tal

**Mål:** Programmet har ett hemligt tal och en gissning, båda som variabler.

**Gör så här:** Lägg till `secret_number` med värdet `12` och `guess` med värdet `7` i `guess_the_number.py`. Skriv tillfälligt ut båda värdena med `print()` så att du ser att variablerna används. Här är talet hemligt bara i spelets idé; i första steget får det synas för att du ska kunna kontrollera koden.

**Kontroll:** Kör filen. Du ska se `12` och `7`. Ändra `guess` till `12`, kör igen och kontrollera att utskriften ändras. Återställ gärna `guess` till `7` inför nästa steg.

**Commit:** `Add fixed secret and guess`

## Steg 2 – jämför talen

**Mål:** Spelaren får ett av tre besked.

**Gör så här:** Ersätt utskriften av de två talen med en `if`/`elif`/`else`-kedja. Om `guess < secret_number`, skriv `Too low`. Om `guess > secret_number`, skriv `Too high`. Annars, skriv `Correct!`. Jämför talen direkt; en funktion behövs inte ännu.

**Kontroll:** Prova `guess` som `7`, `16` och `12`, ett värde i taget medan `secret_number` är `12`. Du ska få `Too low`, `Too high` respektive `Correct!`.

**Commit:** `Compare fixed guess with secret`

## Steg 3 – läs en gissning

**Mål:** Spelaren kan skriva ett tal i terminalen.

**Gör så här:** Ta bort den fasta tilldelningen av `guess`. Be spelaren gissa med `input()` och omvandla svaret till ett heltal med `int()`, så att jämförelserna i steg 2 fungerar. Behåll `secret_number = 12`. Skriv bara siffror när programmet frågar; hantering av text som inte är ett tal ingår inte här.

**Kontroll:** Kör programmet tre gånger och skriv `7`, `16` och `12`. Varje körning ska ge rätt besked för just det talet och sedan avslutas.

**Commit:** `Read a guess from input`

## Steg 4 – gissa tills det blir rätt

**Mål:** Ett spel fortsätter efter en för låg eller för hög gissning.

**Gör så här:** Sätt `guess = 0` före en `while`-loop. Låt loopen fortsätta så länge `guess != secret_number`. Flytta raden med `input()` och `int()` samt hela `if`/`elif`/`else`-kedjan in i loopen. Den första nollan är bara ett startvärde som gör att loopen kan börja; spelaren har ännu inte gissat. Behåll det fasta hemliga talet utanför loopen.

**Kontroll:** Starta programmet en gång. Skriv `7`, sedan `16`, sedan `12`. Du ska få två ledtrådar och därefter `Correct!`; programmet ska avslutas. Ett nytt hemligt tal ska inte skapas mellan gissningarna.

**Commit:** `Repeat guesses until correct`

## Steg 5 – räkna försök

**Mål:** Varje faktisk gissning räknas, även den rätta.

**Gör så här:** Sätt `attempts = 0` före loopen. Öka `attempts` med 1 direkt efter att spelaren har matat in och omvandlat en gissning. När gissningen är rätt, skriv också ut antalet försök. Räkna inte startvärdet `guess = 0` som en gissning.

**Kontroll:** Om du skriver `12` direkt ska antalet vara `1`. Om du skriver `7`, `16`, `12` ska antalet vara `3`.

**Commit:** `Count player guesses`

## Steg 6 – välj ett slumpmässigt tal

**Mål:** Ett nytt spel får ett hemligt tal från 1 till 20.

**Gör så här:** Lägg `import random` överst i filen. Ersätt `secret_number = 12` med `secret_number = random.randint(1, 20)`. Gör detta **en gång före gissningsloopen**, inte inne i den. Berätta för spelaren att intervallet är 1–20. Visa inte det hemliga talet i det vanliga spelet.

**Kontroll:** Spela en omgång med flera gissningar. Ledtrådarna ska avse samma hemliga tal hela omgången och `Correct!` ska avsluta spelet. Starta filen på nytt för att börja en ny omgång. Om du behöver felsöka kan du tillfälligt skriva ut `secret_number` före loopen och sedan ta bort den utskriften.

**Commit:** `Choose a secret number once per game`

## Steg 7 – dela upp arbetet i två functions

**Mål:** Jämförelsen kan användas separat från själva spelomgången.

**Gör så här:** Skapa först `compare_guess(guess, secret_number)`. Den ska bara jämföra sina två argument och använda `return` för att ge exakt en av strängarna `"low"`, `"high"` eller `"correct"`. Den ska inte fråga efter input, skriva ut något eller ändra variabler utanför funktionen. Det är vad **pure** betyder här: samma två tal ger alltid samma svar utan andra effekter.

Skapa sedan `play_game()`. Flytta in valet av `secret_number`, `guess = 0`, `attempts = 0` och gissningsloopen i den. Låt loopen anropa `compare_guess(guess, secret_number)` efter varje gissning och använd returvärdet för att välja vilken ledtråd som skrivs ut. Behåll räkningen: den rätta gissningen räknas innan spelet avslutas. Anropa `play_game()` en gång längst ned i filen. Skriv `compare_guess` före `play_game` så att namnet finns när spelet startar.

**Kontroll:** Prova gärna tillfälligt `print(compare_guess(7, 12))`, `print(compare_guess(16, 12))` och `print(compare_guess(12, 12))` innan du startar spelet. De ska ge `low`, `high`, `correct` i den ordningen. Ta sedan bort de tillfälliga utskrifterna och spela en omgång. Spelarens ledtrådar ska fortfarande vara `Too low`, `Too high` och `Correct!`, och första rätta gissningen ska ge 1 försök.

**Commit:** `Separate comparison and game flow`

## Steg 8 – godkänn bara tal i intervallet

**Mål:** Tal utanför 1–20 avvisas utan att räknas som försök.

**Gör så här:** I `play_game()`, kontrollera gissningen direkt efter `int(input(...))`. Om den är mindre än 1 eller större än 20, skriv att spelaren ska välja 1–20. Lägg ökningen av `attempts` och anropet till `compare_guess` i en `else`-gren som bara körs för giltiga tal. Loopen ska sedan fråga igen. Ändra inte `secret_number`. Du behöver inte hantera text som `hej` i detta steg.

**Kontroll:** Skriv `0`, `21` och sedan ett giltigt tal. De två första ska ge ett meddelande om intervallet, ingen låg/hög-ledtråd och ingen ökning av `attempts`. Om det giltiga talet råkar vara rätt ska antalet vara `1`. För en förutsägbar kontroll kan du tillfälligt använda `secret_number = 12`, prova `0`, `21`, `12`, och därefter återställa `random.randint(1, 20)`.

**Commit:** `Ignore guesses outside the range`

## Steg 9 – frivillig utmaning: högst fem giltiga försök

**Mål:** Omgången avslutas efter fem giltiga gissningar eller när spelaren gissar rätt.

**Gör så här:** Ändra loopens villkor så att den fortsätter bara medan gissningen är fel **och** `attempts < 5`. När loopen är slut, skilj på rätt gissning och slut på försök. Visa ett avslutande meddelande om fem giltiga försök har använts utan rätt svar. Behåll kontrollen från steg 8 före ökningen av `attempts`, så att ogiltiga tal inte tar ett försök. Ett rätt svar på det femte giltiga försöket ska fortfarande vinna.

**Kontroll:** Använd tillfälligt `secret_number = 12`. Prova `0`, `21` och fem giltiga felaktiga tal: spelet ska avslutas efter de fem giltiga. Prova sedan fyra giltiga felaktiga tal följt av `12`: spelaren ska vinna med `5` försök. Återställ slumpvalet efter kontrollen.

**Commit:** `Limit the game to five valid guesses`

## När du fastnar

Kör programmet efter en liten ändring i taget och jämför med kontrollen för det steg du arbetar med. Läs felmeddelandet från första raden som nämner din fil. [HJALP.md](HJALP.md) ger ledtrådar utan en färdig lösning. Skriv i [REFLECTION.md](REFLECTION.md) vad som fungerar och vad du vill fråga om, även om du stannar före sista steget.
