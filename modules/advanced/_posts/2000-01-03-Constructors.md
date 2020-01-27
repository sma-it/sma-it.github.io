---
title: Constructors
---

# Inleiding

In het hoofdstuk over classes, in het voorbeeld van de class Point, werd er op volgende manier een nieuw object van de class Point gemaakt:

```csharp
    Point point1 = new Point();
```

Als we dit even goed analyseren, dan merken we op dat deze instructie eindigt met een functieaanroep, namelijk `Point()`.
Als we de class Point, die in het voorbeeld uitgewerkt is, overlopen vinden we echter nergens een functie met de naam Point. Aangezien Point een naam is die we zelf kozen voor de class, kan deze functie ook geen ingebouwde functie van C# zijn.

Wat is het dan wel? 

De functie `Point()` is de __default constructor__ van de class Point. Je leest hieronder wat een __default constructor__ en een (non-default) __constructor__ is.


## Wat is een constructor?
Een constructor is een speciale functie die enkel uitgevoerd wordt __op het moment dat je een object van je class maakt__. Deze functie heeft __de naam van de class__ en heeft __geen resultaat__ (dus geen returntype, zelfs geen void). Bovendien moet de constructor __public__ zijn.

We kunnen twee soorten constructors onderscheiden:

### De default constructor
Wanneer de compiler je code compileert, en je schreef zelf geen constructor (zie verder), dan voegt de compiler op de achtergrond zelf een toe. Dit noemen we de _default constructor_. Deze constructor heeft geen argumenten doet niets bijzonders, maar is nodig om een object te kunnen maken van een class.

De algemene syntax van een default constructor ziet er als volgt uit:
```csharp
public NameOfClass() {}
```

Toegepast op de class Point wordt dit:
```csharp
public Point() {}
```

Je kan dus een class maken zonder een constructor te voorzien. Toch kan een constructor handig zijn. We kunnen deze functie immers gebruiken om een object bij het maken al te initialiseren. Om dit te doen schrijf je een (non-default) constructor. Vanaf nu gebruiken we voor deze non-default constructor gewoon de naam constructor en laten we de non-default weg.

### Een constructor
Indien we bij het maken van een nieuw object van de class Point de properties X en Y reeds willen initialiseren, kunnen we hiervoor een constructor schrijven. Deze constructor plaatsen we in de class Point en ziet er als volgt uit: 

```csharp
class Point
{
    //Properties
    public float X { get; set; }
    public float Y { get; set; }

    
    // De constructor
    public Point(int X, int Y) {
        this.X = X; //Merk op: gebruik van this bij identieke namen voor
        this.Y = Y; //argumenten en variabelen.
    }

    ....
}
```

Nu kan je op de volgende manier een nieuw object van de class Point maken:

```csharp
Point punt = new Point(10, 20);
```

De property punt.X krijgt hier de waarde 10 en de property punt.Y krijgt de waarde 20.

Opmerking: het keyword `this`:
Omdat er in het voorbeeld dezelfde namen gebruikt zijn voor de argumenten als voor de properties van de class, is het noodzakelijk om d.m.v. het keyword `this` onderscheid te maken tussen beide. Als er voor een naam `this` geplaatst wordt, gekoppeld door een punt, dan wordt er op die manier aangeduid dat dit de property van de class is. Op die manier is het voor de constructor duidelijk dat de class-variabele moet geïnitialiseerd worden op het argument (en niet omgekeerd).

## Combinatie van default constructors en eigen constructor
Van zodra je een eigen constructor in de class plaatst, zal de default constructor niet meer werken.
Toegepast op het voorbeeld van de class Point kunnen we zeggen dat, van zodra we de constructor toevoegen aan onze class, het niet meer zal lukken om op onderstaande manier een niet-geïnitialiseerd object te maken. Omdat we een constructor met 2 argumenten gemaakt hebben en de default constructor zonder argumenten hierdoor vervalt, is het dus niet meer mogelijk dit niet-geïnitialiseerde object te maken.

```csharp
Point point1 = new Point();
```

Oplossing: indien het toch nodig zou zijn om een niet-geïnitialiseerd object van de class te maken, voegen we de default constructor als extra constructor aan de class toe.

```csharp
public class Point {
    Public int X;
    Public int Y;

    // Default constructor
    public Point() {}

    // Eigen constructor met argumenten
    public Point(int X, int Y) {
        this.X = X;
        this.Y = Y;
    }
}
```

Op die manier kan je beide constructors gebruiken:

```csharp
Point point1 = new Point(); // default constructor
Point point2 = new Point(3, 30); // Eigen constructor
```

## Andere vormen van constructors

### Een constructor met slechts 1 argument

De onderstaande constructor maakt een nieuw object van de class Point, hierbij wordt X geïnitialiseerd op het argument, Y krijgt steeds de waarde 0.

```csharp
public Point(int X) {
        this.X = X;
        this.Y = 0;
    }
```

### Een constructor met default argumenten

De onderstaande constructor initialiseert X en Y op de argumenten indien er hiervoor waarden meegegeven worden. Indien de waarden niet meegegeven worden, initialiseert de constructor beide properties op 0.

```csharp
public Point(int X=0, int Y=0) {
        this.X = X;
        this.Y = Y;
    }
```
Met bovenstaande constructor is het mogelijk om objecten op de volgende manier te maken:

```csharp
Point point1 = new Point(); // X en Y krijgen beide de waarde 0
Point point2 = new Point(3, 30); // X krijgt de waarde 3, Y krijgt de waarde 30
Point point3 = new Point(3); // X krijgt de waarde 3, Y krijgt de waarde 0
```

Opgepast! 
Bovenstaande constructor is eveneens een __default constructor__ omdat hij zonder argumenten kan opgeroepen worden. Naast deze constructor nog een 'gewone' default constructor in de class voorzien, geeft een foutmelding. Er bestaan dan immers 2 functies met dezelfde naam en die beiden zonder argumenten opgeroepen kunnen worden. Zoals je gezien hebt bij functie overloading, is dit niet toegelaten.

De onderstaande code is dus __fout__!

```csharp
public class Point
{
...
// Default constructor
public Point() {}

// Nog een constructor die als default gebruikt kan worden -> dubbelzinnigheid -> fout!!!
public Point(int X=0, int Y=0) {
        this.X = X;
        this.Y = Y;
    }
...
```


## Properties verplicht initialiseren bij het maken van een nieuw object.
Indien we geen default constructor in een class voorzien, kunnen objecten enkel gemaakt worden door een eigen constructor met argumenten. Deze manier van werken maakt het mogelijk om te verplichten dat alle, of een aantal, properties van het object geïnitialiseerd worden bij het maken van het object.

Voorbeeld:
Hieronder vinden we de class Person. Deze class bevat 2 properties: FirstName en LastName. Er werd gekozen om deze properties ReadOnly te maken via bijbehorende private variabelen. 
Door enkel een eigen (niet-default) constructor met argumenten te voorzien, kan er enkel een nieuw object gemaakt worden als er zowel voor FirstName en LastName een waarde opgegeven wordt. Merk op dat de constructor de private variabelen initialiseert en niet de ReadOnly properties.

```csharp
public class Person {
    private string firstName;
    public string FirstName => firstName;

    private string lastName;
    public string LastName => lastName;

    public Person(string firstName, string lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```

<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-constructors-1" target="_blank">oefening-constructors-1</a> en maak de oefeningenreeks</p>
</div>