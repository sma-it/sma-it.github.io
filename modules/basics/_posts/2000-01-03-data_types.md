---
title: Data Types en Variabelen
published: true
---
<div class="header1" markdown = "1"># Data types en variabelen
</div>

<div class="header2" markdown = "1">## Wat is een data type?
</div>

Je programma kan gebruik maken van verschillende soorten gegevens. Zo kan je berekeningen maken met getallen, namen gebruiken, enz.

C# maakt gebruik van data types, of gegevenstypes, om met deze verschillende soorten gegevens te werken. Hieronder vind je een overzicht van de gegevenstypes die in de cursus gebruikt zullen worden. In de eerste kolom vind je de naam van het data type, in de tweede kolom zie je het bereik dat dit data type kan hebben, m.a.w. welke waarden er tot dit data type behoren.


| Keyword       | Bereik   |
| ------------- |-------------    |
| bool          | true / false         |
| int           | gehele getallen van -2147483648 tot 2147483647   |
| float         | kommagetallen van -3.402823e38 tot 3.402823e38        |
| double        | kommagetallen van -1.79769313486232e308 tot 1.79769313486232e308       |
| char          | één karakter |
| string        | een tekenreeks  |
{:.tableBorder}

<div class="header2" markdown = "1">## Wat is een variabele?
</div>

Tijdens het uitvoeren van een programma zal het vaak nodig zijn om gegevens bij te houden in het geheugen van de computer. Enkele voorbeelden hiervan zijn invoer van de gebruiker of het resultaat van een berekening.

Om op een handige manier een geheugenplaats aan te kunnen spreken, maken we gebruik van een variabele. Door middel van de variabele kunnen we gegevens plaatsen in de geheugenplaats en de inhoud ervan terug oproepen. De inhoud van de variabele kan tijdens het programma gewijzigd worden.

Naast een naam, krijgt een variabele ook een data type. Dit gegevenstype bepaalt welk type informatie er in de variabele opgeslagen kan worden en welke bewerkingen er met de variabele kunnen gebeuren. Tevens bepaalt het gekozen gegevenstype hoeveel ruimte er in het geheugen voorzien zal worden om de data op te slaan.

<div class="header2" markdown = "1">## Declaratie van een variabele
</div>

Onder declaratie van een variabele verstaan we het maken van de variabele. Dit houdt in dat er een naam en een data type aan de variabele toegekend worden.

Kies telkens een betekenisvolle naam voor je variabele en gebruik het correcte data type.

Niet alle karakters kunnen gebruikt worden om een naam van een variabele samen te stellen. Een geldige variabelenaam voldoet aan de volgende eisen:
* De naam kan letters, cijfers en de underscore (_) bevatten.
* De naam begint met een letter of een underscore. Een cijfer als eerste karakter is niet toegelaten.
* De naam is hoofdlettergevoelig. Bijvoorbeeld: de variabele Price is niet dezelfde als de variabele price.
* Gereserveerde woorden van C# kunnen niet gebruikt worden als naam voor een variabele. Zo kan je bijvoorbeeld geen variabele met de naam `int` maken aangezien dit woord gereserveerd is in C#.

Enkele voorbeelden van declaraties:
```csharp

int x;               // Inhoud: een geheel getal
string name;         // Inhoud: een tekenreeks
float price;         // Inhoud: een kommagetal
double averageSpeed; // Inhoud: een kommagetal
char c;              // Inhoud: 1 karakter

 ```

Variabelen van hetzelfde data type kan je op 1 lijn declareren. Zo declareert onderstaand voorbeeld 3 variabelen van het type integer:
```csharp
int x, y, z;
```

<div class="header2" markdown = "1">## Initialisatie van een variabele
</div>

Het initialiseren van een variabele houdt in dat je de variabele een waarde geeft. Dit kan op verschillende manieren gebeuren:

### De variabele gelijk stellen aan een waarde

```csharp

// Declaratie van variabelen van verschillende gegevenstypes.
int x;           
string name;     
float price; 
double averageSpeed;
char c;

// Initialisatie van de bovenstaande variabelen op een gepaste waarde.
x = 7;

name = "voorbeeld";   // Tekst plaats je tussen dubbele aanhalingstekens.

price = 2.99F;        // Gebruik een punt bij het kommagetal. Bij een float variabele laat 
                      // je het getal volgen door de letter F.

averageSpeed = 52.36; // Let op! Je geeft kommagetallen in met een punt en niet met een komma.

c = 'A';              // Het karakter plaats je tussen enkele aanhalingstekens
```

### De variabele gelijk stellen aan invoer van de gebruiker

```csharp
// Declaratie
string name;
int number;              
     
// Initialisatie
Console.WriteLine("Geef je naam: ");
name = Console.ReadLine(); // name wordt geïnitialiseerd op de invoer van het toetsenbord

Console.WriteLine("Geef een getal: ");
number = Convert.ToInt32(Console.ReadLine()); // Let op de omzetting naar int
```

Gegevens die ingevoerd worden via het toetsenbord hebben steeds het gegevenstype `string`. Om deze invoer in variabelen met een ander gegevenstype te plaatsen is er een omzetting (conversie) nodig. In het bovenstaande voorbeeld wordt de omzetting van string naar int gedaan d.m.v. `Convert.ToInt32()`.

Voor de andere data types bestaan er eveneens methods om deze conversie te doen: `Convert.ToSingle()` (dit doet een conversie naar float), `Convert.ToDouble()`, `Convert.ToBoolean()`, `Convert.ToChar()`.


### De variabele gelijk stellen aan het resultaat van een bewerking

```csharp

// Declaratie  
int x, y, result;               
       
// Initialisatie
x = 7;
y = 10;
result = x + y; // result wordt geïnitialiseerd op het resultaat van de bewerking.  
```

 

<div class="note waarschuwing">
<p>Een variabele moet steeds geïnitialiseerd zijn voordat hij gebruikt wordt. Een niet-geïnitialiseerde variabele gebruiken (in bijvoorbeeld een bewerking of uitvoer) kan tot onverwachte en foutieve resultaten leiden.</p>
</div>

<div class="header2" markdown = "1">## Een variabele op het scherm tonen
</div>

D.m.v. `Console.WriteLine()` kan je zaken op het scherm laten verschijnen. Dit kan een variabele, letterlijk weer te geven tekst (= string literal) of een combinatie van beiden zijn.

Enkele voorbeelden:

```csharp
// De inhoud van de variabele y wordt getoond
Console.WriteLine(y);

// Er wordt een combinatie van een string literal en de inhoud van een variabele getoond.
Console.WriteLine("De prijs is: " + price + " euro");   
```

<div class="header2" markdown = "1">## Automatische conversie tussen data types
</div>

In bepaalde gevallen zal C# zelf de conversie tussen gegevenstypes doen. De numerieke gegevenstypes hebben onderstaande hiërarchie:

* double (hoogste)
* float
* int (laagste)

Conversie van een lager gegevenstype naar een hoger gebeurt automatisch. Probeer je een variabele van een lager gegevenstype gelijk te stellen aan een hoger data type dan krijg je een foutmelding.

Enkele voorbeelden:

* Conversie van `int` naar `double`

```csharp

int x;  
double y;

x = 10;
y = x;  // Automatische conversie van int naar double
 
```

Aangezien dit een conversie van een lager naar een hoger gegevenstype is, lukt dit probleemloos.

* Conversie van `double` naar `int` (met foutmelding!)

```csharp

int x;  
double y;

y = 10.99;
x = y;  // Automatische conversie van double naar int is niet mogelijk
 
```

In bovenstaand voorbeeld wordt er geprobeerd om de inhoud van een variabele met hoger gegevenstype te plaatsen in een variabele van een lager data type. Dit geeft een foutmelding.

Indien automatische conversie tussen data types niet lukt maar er toch een omzetting nodig is, kan je gebruik maken van de Convert methods die in vorige punt aangehaald werden. Merk hierbij op dat dit een wijziging van gegevens tot gevolg kan hebben.

Indien we de Convert method `Convert.ToInt32()` toepassen om de foutmelding bij het vorige voorbeeld te vermijden dan wordt dit:

```csharp

int x;  
double y;

y = 10.99;
x = Convert.ToInt32(y);
Console.WriteLine("De waarde van y: " + y);
Console.WriteLine("De waarde van x: " + x);
 
```
De uitvoer van dit stukje code is:

```csharp
De waarde van y: 10.99
De waarde van x: 11
```

Zoals je ziet heeft de method `Convert.ToInt32()` de waarde van y eerst afgerond op nul decimalen en daarna in x geplaatst. Dit is noodzakelijk omdat de integer x geen kommagetal kan bevatten. Het afronden gebeurt op een rekenkundige manier.

### Van char naar string
De conversie van een `char` naar een `string` is minder vanzelfsprekend. Dat komt omdat je een `char`, zoals 'a', ook als een cijfer in de ASCII tabel kan zien. 

Er zijn twee manieren om een `char` om te zetten naar `string`:
* Conversie d.m.v. `Convert.ToString(a)`: dit zal de `char` omzetten naar een `string`. Zie voorbeeld `string` s1 hieronder.
* De functie `.ToString()` toepassen op de variabele van het type `char`. Zie voorbeeld `string` s2 hieronder.

Let op! Wanneer je twee chars optelt, en het resultaat is groter dan 127, dan wordt het resultaat vanzelf een `integer`. De letter a heeft in de ASCII tabel de waarde 97. Als je zoals in het voorbeeld met string s3 binnen de functiehaken van ToString eerst de twee characters optelt, dan geeft dit de waarde 194. Aangezien dit groter is dan 127, zal het resultaat een integer zijn. Het is op deze integere waarde dat daarna de `Convert.ToString()` functie toegepast wordt, met als gevolg dat het resultaat een `string` met waarde "194" zal zijn, en niet zoals we zouden verwachten "aa".

```
char teken = 'a';
string s1 = Convert.ToString(teken) + Convert.ToString(teken); // s1 = "aa"
string s2 = teken.ToString() + teken.ToString(); // s2 = "aa"
string s3 = Convert.ToString(teken + teken); // s3 = "194"
```
<div class="header2" markdown = "1">## Gebruik van variabelen in functies
</div>
Later in de cursus volgt een volledig hoofdstuk over functies. Toch is het belangrijk om nu al enige notie van functies te hebben aangezien de oefeningen met functies opgebouwd zijn.
Een functie is een klein stukje programma dat opgeroepen kan worden d.m.v. een functienaam.
Hetzelfde voorbeeld maar dan toegepast in een functie:

 ```csharp
// Declaratie van de variabelen a en b in de argumentenlijst. Deze variabelen bestaan enkel binnen de functie.
// Initialisatie van a en b gebeurt bij de aanroep van de functie.
public static int calcSum(int a, int b)   
{
  int result;
  result = a + b;
  return result;
}
```

Als je een progamma start, wordt steeds de functie `Main` gestart. Vanuit `Main` kan je de functie `calcSum`als volgt aanroepen:

```csharp
static void Main(string[] args)
  {
    int x = 10;
    int y = 2;
    int res;
    // Hieronder wordt de functie calcSum aangeroepen. Het argument a krijgt de waarde van x,
    // het argument b krijgt de waarde van y. Op die manier kan er binnen de functie met de  
    // daar gekende variabelen a en b gewerkt worden die dezelfde waarde gekregen hebben 
    // als x en y (twee variabelen uit Main).
    // Je leert meer hierover in het hoofdstuk Functies.
    res = calcSum(x, y); 
    Console.WriteLine("Het resultaat van de berekening is: " + res);

    System.Console.ReadKey();
  }
```
<div class="header2" markdown = "1">## Opmerking i.v.m. het maken van oefeningen
</div>

In de stap hieronder start je met de eerste oefening. In de uitvoer van het project krijg je al een eerste indicatie dat je de oefening correct uitgewerkt hebt doordat telkens jouw bekomen resultaat vergeleken wordt met het verwachte resultaat.
Er zijn echter nog extra NUnit tests voorzien, die je code grondiger met andere en soms met meerdere waarden testen. Je kan deze tests starten via het Test Explorer venster. Indien dit venster niet openstaat, kan je het steeds terug zichtbaar zetten via het menu Test - Window - Test Explorer. Merk op dat de tests pas in het Test Explorer venster zichtbaar komen te staan nadat je je code uitgevoerd hebt.

<div class="note protip">
<p>Test steeds je oefeningen met de extra NUnit tests en zorg ervoor dat elke test correct werkt.</p>
</div>


<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-datatypes-1" target="_blank">oefening-datatypes-1</a> en maak de oefeningenreeks</p>
</div>
