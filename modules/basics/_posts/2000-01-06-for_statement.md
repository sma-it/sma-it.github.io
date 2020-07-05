---
title: Het for Statement
---
<div class="header1" id="top" markdown = "1"># Het for Statement
</div>
<div class="header2" markdown = "1">## Gebruik van het for statement
</div>

Het `for` statement wordt gebruikt om een instructieblok meerdere keren uit te voeren.

Een programmeerstructuur die een stuk code meerdere keren uitvoert, noemt met een lus (loop). Daarom wordt er vaak de naam for-lus of for-loop gebruikt. Een andere naam voor de for-lus is 'iteratie'.

<div class="header2" markdown = "1">## De syntax van het for statement
</div>

De algemene syntax van een for-lus ziet er als volgt uit:

```csharp
for (initialisatie; voorwaarde; stap)
{
    te herhalen instructieblok
}
```

Bespreking:

* De betekenis van de parameters tussen de ronde haakjes bij for:
  - Initialisatie: de teller wordt op een beginwaarde geïnitialiseerd.
  - Voorwaarde: zolang aan deze voorwaarde voldaan is, wordt de for-lus uitgevoerd.
  - Stap: de teller wordt met deze stap gewijzigd.
* Net zoals bij het `if-else` statement plaatsen we ook bij het `for` statement accolades rond het bijbehorende instructieblok. Indien dit instructieblok slechts uit één instructie bestaat, zijn de accolades optioneel. We maken echter de afspraak ze altijd te plaatsen.

<div class="header2" markdown = "1">## Voorbeelden
</div>

### Voorbeeld 1: For-lus toont de getallen 0 tot en met 9 op het scherm.

```csharp
for (int i = 0; i < 10; i++)
{
    Console.Write("{0} ", i);
}
Console.WriteLine("\nFirst instruction after the for loop");

/* Output
0 1 2 3 4 5 6 7 8 9
First instruction after the for loop
*/
```
Bespreking:
De parameters tussen haakjes zijn:
* Initialisatie: int i = 0
* Voorwaarde: i < 10
* Stap: i++
    * Belangrijk: voluit geschreven is dit i = i + 1.
    * We kunnen het verloop van de for-lus dus als volgt beschrijven: de teller i wordt geïnitialiseerd op 0 en gaat in stappen van 1 omhoog. Als i de waarde 10 bereikt stopt de for-lus en wordt het instructieblok niet meer uitgevoerd.
Het instructieblok toont de waarde van de teller i, bijgevolg verschijnen de getallen 0 tot en met 9 op het scherm.
Het getal 10 verschijnt niet omdat het instructieblok niet uitgevoerd wordt van zodra de teller i de waarde 10 bereikt heeft.
Als de for-lus afgelopen is, vervolgt het programma met de code die na de lus komt. In dit voorbeeld is dit de tekst '\nFirst instruction after the for loop". 

Opmerkingen: 
* Bij de instructie Console.WriteLine wordt gebruik gemaakt van `\n`. Dit genereert een enter in de uitvoer. De zin "First instruction after the for loop" verschijnt dus op een nieuwe regel.
* Verklaring syntax Console.Write("{0} ", i): De inhoud van de variabele i wordt op de plaats van {0} ingevuld. 
Er kunnen meerdere parameters gebruikt worden, de nummering is oplopend {0}, {1}, {2}, ... Voor elke parameter moet een variabele voorzien worden.

Opmerking

### Voorbeeld 2: For-lus met char teller

```csharp
for (char c = 'a'; c <= 'z'; c++)
{
    Console.Write("{0} ", c);
}
Console.WriteLine("\nFirst instruction after the for loop");

/* Output
a b c ... x y z
First instruction after the for loop
*/
```
Bespreking:
* De teller van een for-lus moet niet noodzakelijk van het type int zijn (al zal dit vaak wel het geval zijn). In het voorbeeld wordt een char-teller gebruikt om het alfabet op het scherm te tonen.
* Als teller van een for-lus wordt vaak een variabele met de naam i gebruikt. Zoals je in het voorbeeld kan zien, is de naam van de teller vrij te kiezen.
* Zoals je in het voorbeeld ziet, kan er in C# met char-variabelen geteld worden. Telkens de char-variabele met 1 verhoogt schuift hij een waarde op in de ASCII-tabel. Aangezien het alfabet in opeenvolgende posities in de ASCII-tabel zit, wordt op deze manier het volledige alfabet doorlopen.
* Ook tellers van het type float en double zijn mogelijk.

### Voorbeeld 3: Beginwaarde teller verschillend van 0 en stapgrootte verschillend van 1

```csharp
for (int i = 10; i < 100; i += 2)
{
    Console.Write("{0} ", i);
}
Console.WriteLine("\nFirst instruction after the for loop");

/* Output
10 12 14 16 ... 96 98
First instruction after the for loop
*/
```

Bespreking:
* Vaak zal je de teller van de for-lus laten start van 0 of 1, toch is een andere beginwaarde mogelijk zoals je in het voorbeeld ziet.
* Ook voor de stapgrootte kan er afgeweken worden van de waarde 1. In het voorbeeld gaat de teller met 2 omhoog. Let goed op dat je een volledige instructie gebruikt voor de derde parameter. Voluit schrijven van `i+=2` geeft `i=i+2`. Maak niet de fout om `i+2` bij de derde paramater te plaatsen. Dit wijzigt de teller niet en de for-lus werkt niet correct.

### Voorbeeld 4: Variabele in de voorwaarde

```csharp
int max = 40;
for (int i = 0; i < max; i += 2)
{
    Console.Write("{0} ", i);
}
Console.WriteLine("\nFirst instruction after the for loop");

/* Output
0 2 4 6 ... 36 38
First instruction after the for loop
*/
```

Bespreking:
In de voorwaarde wordt er gebruik gemaakt van de variabele max. Vanzelfsprekend kan ook bij de initialisatie een variabele gebruikt worden.

### Voorbeeld 5: Break statement

```csharp
for (int i = 0; i < 10; i++)
{
    Console.Write("{0} ", i);
    if (i == 5)
    {
        Console.WriteLine("\nWe make the loop end at number 5!");
        break;
    }
}
Console.WriteLine("First instruction after the for loop");

/* Output
0 1 2 3 4 5
We make the loop end at number 5!
First instruction after the for loop
*/
```
Bespreking:
* In de for-lus zit een selectie. Bij elke lus wordt er getest of de teller de waarde 5 heeft. Indien dit niet het geval is, wordt het bijbehorende instructieblok niet uitgevoerd en loopt de lus door. Indien de teller i echter 5 is wordt het instructieblok van de selectie uitgevoerd.
* In het instructieblok van de selectie doet het volgende:
    * Er wordt een boodschap getoond: "We make de loop end at number 5!"
    * Er wordt een `break` gegeven. Het `break` statement zal de lus volledig stoppen en zorgt ervoor dat het programma naar de eerste instructie na de for-lus springt. Dus ook al heeft de teller de bovengrens nog niet bereikt, de for-lus eindigt toch.

### Voorbeeld 6: Continue statement

```csharp
for (int i = 0; i < 10; i++)
{
    if (i < 8)
    {
        continue;
    }
    Console.WriteLine(i);
}

Console.WriteLine("First instruction after the for loop.");

/*
Output:
8
9
First instruction after the for loop
*/
```

Bespreking:
* In de for-lus zit een selectie. Indien de teller kleiner is dan 8 wordt het `continue` statement uitgevoerd. Van zodra de teller i een waarde 9 of hoger krijgt, wordt het `continue` statement niet meer uitgevoerd.
* Het `continue` statement stopt de huidige iteratie van de lus. Dit betekent dat alle instructies binnen de lus die volgen op `continue` niet meer uitgevoerd worden. De lus stopt echter niet volledig, de teller wordt met de stapgrootte verhoogd en de volgende iteratie van de lus start.

<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-for-1" target="_blank">oefening-for-1</a> en maak de oefeningenreeks</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>
