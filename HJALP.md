# Hjälp när något fastnar

Börja med den kontroll som hör till ditt senaste fungerande steg. Ändra en sak, spara filen och kör igen. Du behöver inte göra alla steg under samma arbetspass.

## Programmet startar inte

- Står terminalen i mappen där `guess_the_number.py` finns? Kontrollera filnamnet: understreck i filnamnet, bindestreck i mappnamnet.
- Prova `python guess_the_number.py`, `py guess_the_number.py` eller `python3 guess_the_number.py` beroende på dator. Om inget kommando fungerar, be om hjälp att hitta Python-installationen.
- Om du använder GitHub: klona ditt eget repository som skapades från templaten. Öppna sedan den klonade mappen innan du kör filen.

## Fel vid körning

- `IndentationError`: titta på raderna efter `if`, `elif`, `else`, `while` och `def`. Rader som hör till samma block ska ha samma indrag. Använd helst fyra mellanslag per nivå.
- `NameError`: kontrollera stavningen på variabeln eller funktionen och att den får ett värde innan den används.
- `ValueError` från `int()`: skrev du ett heltal med siffror? I den här övningen behöver programmet ännu inte hantera bokstäver eller tom input.
- Programmet frågar bara en gång: kontrollera att både `input()` och jämförelsen ligger inne i `while`-loopen.
- Programmet verkar aldrig bli klart: kontrollera att en ny gissning läses in i loopen och att loopens villkor kan bli falskt.

## Resultatet känns fel

- För steg 2–5, använd `secret_number = 12` och prova ett lågt, ett högt och ett korrekt tal var för sig.
- Får du motstridiga ledtrådar under samma spel? Kontrollera var `random.randint(1, 20)` står. Det hemliga talet ska väljas en gång före loopen.
- Blir första rätta gissningen försök `0`? Titta på ordningen mellan input, ökningen av `attempts` och utskriften av resultatet.
- Räknas `0` eller `21` som försök i steg 8? Följ raden som ökar `attempts`: ska den nås för ett ogiltigt tal?
- Om femförsöksgränsen beter sig konstigt, kontrollera både loopens villkor och om `attempts` bara ökar för giltiga tal.

## Git när du använder ett eget repository

- Om en `commit` inte tar med din ändring, kontrollera att filen är sparad och se vilka filer Git visar som ändrade.
- Om `push` inte fungerar, kontrollera att du öppnat ditt eget repository och be om hjälp med åtkomst. En länk till ett privat repository ger inte automatiskt läraren åtkomst.

Skriv gärna ned felmeddelandet och vad du redan provat i [REFLECTION.md](REFLECTION.md) innan du ber om hjälp.
