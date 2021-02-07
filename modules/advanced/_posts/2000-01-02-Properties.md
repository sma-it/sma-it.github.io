---
title: Properties
---

<div class="header1" id="top" markdown = "1"># Properties
</div>

In het vorige hoofdstuk leerde je al dat *Properties* een belangrijk onderdeel van classes vormen. Kijk nog even naar deze class:

```csharp
public class Person {
    public string FirstName { get; set; }
    public string LastName { get; set; }
    ...
}
```
Van een object van deze class kunnen we de FirstName en de LastName in stringformaat bijhouden. We gebruiken properties dus een beetje zoals variabelen. 
Als we het voorbeeld van hierboven bekijken zien we echter een aantal verschillen met de variabelen die we tot nu toe gebruikten:

- Er staat een extra woord vooraan, namelijk `public`. Dit wordt in dit hoofdstuk besproken in het puntje Access modifiers.
- Achteraan is er een stukje tussen accolades bijgekomen. Dit bespreken in dit hoofdstuk bij het puntje Getters en Setters.

<div class="header2" markdown = "1">## Access modifiers
</div>

Een access modifier geeft aan in welke mate een property toegankelijk is. Een volledig lijst van deze access modifiers vind je onder volgende [link](https://msdn.microsoft.com/en-us/library/system.datetime(v=vs.110).aspx)

We beperken ons voorlopig tot twee modifiers die veel gebruikt worden, namelijk `public` en `private`.

- `public`: een property die `public` als modifier meekreeg is van overal toegankelijk. Dus de property kan rechtstreeks uitgelezen worden of rechtstreeks een waarde krijgen in de class zelf, maar ook van buitenaf (bv. in Main of vanuit een andere class).
- `private`: een property die `private` als modifier meekreeg is enkel toegankelijk vanuit de class waartoe hij behoort. Vanuit Main of vanuit andere classes kan deze property niet rechtstreeks aangesproken worden.

Door gebruik te maken van `public`en `private`kan je dus bepalen waar een property rechtstreeks aangesproken kan worden en waar niet.

<div class="header2" markdown = "1">## Getters en setters
</div>

Voor properties zijn er volgende combinaties van toegankelijkheid mogelijk:
- ReadWrite property: de waarde van de property kan gelezen en aangepast worden. Leestoegang geef je met `get`, schrijftoegang geef je met `set`. 
- WriteOnly property: dit type property behandelen we niet omdat het enkel in specifieke situaties gebruikt wordt.
- ReadOnly property: je kan de waarde van de property lezen. In dit geval gebruik je enkel `get`. 

De keywords `get`en `set` verwijzen naar de getters en setters die voor de property gemaakt worden. Getters en setters zijn methods met een heel specifieke functie: het uitlezen van de property (getter) of de property een waarde geven (setter). In sommige programmeertalen moet je deze getters en setters zelf schrijven. In C# worden ze automatisch gecreëerd door `get`en/of `set` aan de property toe te voegen.

<div class="note waarschuwing">
<p>In de voorbeelden,oefeningen, taken en testen zullen we steeds gebruik maken van de 'public' access modifier voor een property. De reden hiervoor is dat C# over een handige manier beschikt om via access modifiers bij de getters en setters de mogelijke toegang tot een property in te stellen.
In andere programmeertalen is deze handige manier van werken vaak niet voorzien. Je zal in de toekomst dus merken dat properties heel vaak private als access modifier krijgen en dat je de toegang moet bepalen door het al of niet voorzien van een getter en ee setter voor een property.</p>
</div>

<div class="header2" markdown = "1">## Het gebruik van ReadWrite properties
</div>
### Voorbeeld 1: ReadWrite Properties - geen access modifiers bij get en set

De class Person heeft twee ReadWrite properties en een functie Print() die deze properties op het scherm toont. Aangezien er geen access modifiers bij get en set staan worden deze verondersteld `public` te zijn en zijn de properties dus rechtstreeks toegankelijk vanuit Main.

```csharp
public class Person 
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public void Print()
    {
        Console.WriteLine("Voornaam: {0}", FirstName);
        Console.WriteLine("Achternaam: {0}", LastName);
    }
}
```

In Main kunnen we de properties als volgt aanspreken en op het scherm tonen:

```csharp
public  static void Main()
{
    var person = new Person();      // Er wordt een nieuw object van de class person gemaakt.
    person.FirstName = "Steve";     // De ReadWrite property FirstName wordt d.m.v. de setter 
                                    // geïnitialiseerd.
    person.LastName = "Jobs";       // De ReadWrite property LastName wordt d.m.v. de setter 
                                    // geïnitialiseerd.

    person.Print();                 // De Print-functie toont de properties op het scherm.

    Console.ReadKey();
}

```

### Voorbeeld 2: ReadWrite Properties - een 'private' access modifier bij set

We willen vermijden dat de property LastName gewijzigd kan worden buiten de class. We kunnen niet zomaar het keyword `set` weg laten want dan wordt deze property ReadOnly en kan hij ook binnen de class Person zelf geen waarde meer krijgen. En natuurlijk moet het nog altijd mogelijk zijn om binnen de class zelf een property een waarde te geven, bijvoorbeeld d.m.v. een functie met een gepast argument.
De manier om een property nog wel binnen zijn class zelf Writable te houden en daarbuiten ReadOnly te maken is het keyword `private` voor `set`toe te voegen.

```csharp
public class Person 
{
    public string FirstName { get; set; }
    public string LastName { get; private set; }    // LastName is nu ReadOnly voor de 
                                                    // buitenwereld.

    public void Print()
    {
        Console.WriteLine("Voornaam: {0}", FirstName);
        Console.WriteLine("Achternaam: {0}", LastName);
    }

    // We voorzien een functie ChangeLastName die public is en dus in Main opgeroepen
    // kan worden.
    // Deze functie behoort tot de class Person en heeft dus wel toegang tot de 
    // property LastName.
    // Via deze functie kunnen we LastName dus nog steeds vanuit Main een waarde geven.
    // Voor properties die we dus heel gecontroleerd willen initialiseren, kunnen we 
    // dus gebruik maken van ReadOnly access en kunnen we indien, nodig een functie 
    // voorzien die de property initialiseert.

    public void ChangeLastName(string name)
    {
        LastName = name;
    }
}
```

In Main kunnen we de properties als volgt aanspreken en op het scherm tonen:

```csharp
static void Main(string[] args)
{
    var person = new Person();      // Er wordt een nieuw object van de class person gemaakt.
    person.FirstName = "Steve";     // De ReadWrite property FirstName wordt d.m.v. de setter 
                                    // geïnitialiseerd.
    // person.LastName = "Jobs";    // Deze lijn code geeft nu een fout, LastName is immers een 
                                    // ReadOnly property geworden.

    person.ChangeLastName("Jobs");  // De functie ChangeLastName heeft toegang tot de ReadOnly
                                    // property omdat de functie deel uitmaakt van de class 
                                    //Person.

    person.Print();                 // De Print-functie toont de properties op het scherm. Dit 
                                    // geeft geen foutmelding omdat de print-functie in de
                                    // Person class zit en daarom nog wel toegang heeft tot de
                                    // property LastName.
    Console.ReadKey();
}
```

<div class="header2" markdown = "1">## Het gebruik van ReadOnly properties
</div>

Wanneer gebruik je ReadOnly properties? Er zijn verschillende scenario's denkbaar:

### Preventie
Soms is het echt niet de bedoeling om een variabele aan te passen. 
Preventie betekent dat we `set` weglaten om fouten te voorkomen. De property kan door het ontbreken van `set` niet meer gewijzigd worden.

### Utility
Je kan ook _readonly_ utilities maken die het gebruik van je class vereenvoudigen. Als voorbeeld nemen we terug even de class Person. Veronderstel dat we heel vaak de volledige naam van een persoon in ons programma nodig hebben. We kunnen dan steeds de twee properties (FirstName en LastName) gaan opvragen en ze tonen met een spatie ertussen. Maar, we kunnen hier ook een handige utility voor maken. In het onderstaande voorbeeld zie je de utility Name. De utility is ReadOnly, want er is enkel een getter voorzien (enkel het keyword `get` staat vermeld bij de utility). Maar, er is meer aan de hand. Na het keyword `get` geven we aan wat er moet uitgelezen worden als de utility Name opgevraagd wordt. In dit geval zal het opvragen van Name dus de volledige naam als resultaat geven. Handig!

```csharp
public class Person 
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Name { get => FirstName + " " + LastName; }  // De utility combineert 
                                                               // FirstName en LastName en 
                                                               // zet er een spatie tussen.
}
```

### Berekening
Je kan ook _readonly_ utilities maken voor eenvoudige berekeningen. Zo bijvoorbeeld het oppervlak van een rechthoek:

```csharp 
public class Rectangle {
    public double Width { get; set; }
    public double Height { get; set; }
    public double Area { get => Width * Height; }
    public double Perimeter
	{
        get { 
            var sum = Width + Height;
            return 2 * sum;
        }
    }
}
```
Het bovenstaande voorbeeld bevat nog een kleine nieuwigheid. Als je get property uit meer dan 1 statement bestaat, dan kan je de eerder gebruikte schrijfwijze met het pijltje niet gebruiken. In zo'n geval werk je je statements uit zoals in een normale functie. En gebruik je return om het resultaat aan te duiden. _(In dit geval hadden we de berekening natuurlijk ook makkelijk in een enkel statement kunnen doen, maar bij wijze van voorbeeld gebruiken we een wat langere schrijfwijze.)_

<div class="note protip">
<p>Een simpele manier om het onderscheid te maken tussen een property en een utility is de volgende: Als je een property verwijdert uit de class, dan verlies je data. Als je een utility verwijdert uit je class, dan behoud je nog wel alle data.
Kijk maar naar het voorbeeld hierboven. We kunnen de utility Name probleemloos verwijderen en de volledige naam van de persoon zit nog steeds in de properties FirstName en LastName. Maar, als we de property FirstName verwijderen, dan kennen we de hele naam van de persoon niet meer. We zijn dus data kwijt. Hetzelfde geldt voor de property LastName.</p>
</div>

<div class="header2" markdown = "1">## Wanneer gebruik je _geen_ utility maar een functie?
</div>
Met de bovenstaande informatie zou je heel wat functies kunnen omzetten naar utilities. Elke niet-void functie zonder argumenten zou een `get` utility kunnen worden. En elke void functie met 1 argument zou een `set` functie kunnen zijn. Toch is dat niet de bedoeling. 

### Acties
In het algemeen kan je stellen dat je van acties nooit een utility maakt. 

### Complexe berekeningen
Als je een berekening gebruikt in een utility, dan hoort dat een eenvoudige berekening te zijn. Maar wanneer is een berekening te complex? Dat is voor interpretatie vatbaar, maar je kan de volgende regels gebruiken:

- Wanneer een berekening andere variabelen in de class gaat __aanpassen__, dan hoort het geen utility te zijn.
- Wanneer een berekening __extra variabelen__ moet declareren, dan is ze te complex. Een enkel primitive type, zoals een int of float, dat kan nog. Maar instanties van classes maken, of een nieuwe array declareren, dat hoort niet thuis in een utility.
- Wanneer je in je berekening __andere functies__ van je class oproept, dan maak je ook beter een functie.


<div class="note oefening">
<p>Maak de taak over classes en properties die je op Smartschool vindt.</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>