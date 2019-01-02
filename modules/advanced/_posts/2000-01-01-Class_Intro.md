---
title: Classes
---

# Classes

Een `class` is een verzameling van data en functies die conceptueel bij mekaar horen. In de vorige hoofdstukken maakte je al kennis met classes in C#. `Console` is bijvoorbeeld een class, maar ook `String` en `DateTime` zijn classes. En zelfs de `Main` functie in een programma maakt deel uit van een class.

Neem bijvoorbeeld de class `DateTime`. Deze class heeft properties, zoals `Day`, `Minute`, `Year`, `DayOfWeek`, enzovoort. En daarnaast voorziet de class of functies, zoals `AddDays()`, `CompareTo()` en `ToLocalTime()`. Als we zeggen dat deze functies en properties conceptueel bij mekaar horen, dan bedoelen we dat ze allemaal met het concept *tijd* te maken. Die samenhang is heel belangrijk om een programma of een software library overzichtelijk te houden: als iets niet duidelijk verwant is, dan plaatsen we het niet in dezelfde class.

## Een class maken

Tot hiertoe gebruikte je af en toe bestaande classes. Nu leer je hoe je zelf nieuwe classes maakt. Wanneer een programma groter wordt, dan is het bijna onmogelijk om het overzicht te bewaren zonder je eigen code in classes te plaatsen. Wanneer je bijvoorbeeld gegevens over personen moet verwerken in je programma, dan zou het logisch zijn dat je een class maakt waarin je gegevens over die persoon kan opslaan. De definitie van een class kan bijna overal, maar moet wel binnen een namespace zitten:

```csharp
namespace MijnProgramma 
{
    class Persoon
    {
        // hier komt de inhoud van je class
    }
}
```
<div class="note protip">
<p>Je kan een class samen met andere data in een bestand zetten. En bij oefeningen in deze cursus vragen we je dikwijls om dat te doen omdat dat eenvoudiger is om te verbeteren. Maar wanneer je aan een echt programma werkt dan zal je bijna altijd een bestand maken voor elke class, waarbij de bestandsnaam en de class naam dezelfde zijn.</p>
</div>

Met een lege class ben je natuurlijk niet veel. Als voorbeeld gaan we enkele properties toevoegen. Dit zijn de eigenschappen van een persoon die we willen onthouden. We starten met naam, voornaam en leeftijd. _(De namespace laten we vanaf nu achterwege om de voorbeelden kort te houden.)_

```csharp
class Person 
{
    public string Name { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }
}
```

Een property bestaat dus uit de volgende onderdelen:
* **public:** Hiermee geef je aan dat de property publiek is. Zonder _public_ zal je de waarde van een property niet kunnen raadplegen. 
* **type:** Het type van de property, zoals int, float of string. Maar je zal later zien dat dit ook een andere class kan zijn.
* **naam:** De naam van de property zal je later gebruiken om de waarde op te vragen, net zoals je dat bij een gewone variabele doet.
* **{ get; set; }** Hier komen we later op terug. Dit zorgt er voor dat je de waarde van de property kan opvragen EN wijzigen.

<div class="note protip">
<p>Visual Studio voorziet een handige shortcut voor het maken van properties. Typ `prop` en druk vervolgens twee maal op _tab_. De nodige code wordt automatisch aangevuld, en het woord `int` is geselecteerd. Typ nu het type en druk opnieuw twee maal op _tab_. Nu is de naam geselecteerd. Typ de naam en druk twee maal op enter. De cursor staat nu op de volgende regel, klaar voor de volgende property.</p>
</div>


## Een class gebruiken

Wanneer je een `class` maakt, dan vertel je de compiler hoe een object eruit ziet. Je maakt eigenlijk een definitie, of een blueprint. Maar om de class te gebruiken zal je een _instance_, of een object, moeten maken van de class. Je kent dit principe al, want ook `DateTime` verwacht dat je een object maakt:

```csharp
DateTime date = new DateTime();
```

De class `Person` gebruiken doen we op dezelfde manier. Eens we een object hebben, kunnen we de properties van dat object aanpassen:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Person person1 = new Person();
        Person person2 = new Person();

        person1.FirstName = "Bilbo";
        person1.Name = "Baggins";
        person1.Age = 111;

        person2.FirstName = "Legolas";
        person2.Name = "Greenleaf";
        person2.Age = 2387;

        Console.ReadKey();
    }
}

```

Jammer genoeg toont dit programma niets niets op het scherm. Daarom voegen we aan de Program class een `PrintPerson` functie toe die de eigenschappen van de persoon toont. Dat kan door een object van het type `Person` als functieargument te gebruiken.

```csharp
static void PrintPerson(Person person)
{
    Console.WriteLine("Name: {0} {1}", person.FirstName, person.Name);
    Console.WriteLine("Age: {0}", person.Age);
}
```

Deze functie laat ons toe om in het programma de gegevens van de personen op het scherm te tonen:

```csharp
// Dit plaats je net voor Console.ReadKey();
PrintPerson(person1);
PrintPerson(person2);
```

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-classes-1">oefening-classes-1</a> via github en maak oefening 1.</p>
</div>

## Functies in een class

Aan het begin van dit hoofdstuk stelden we dat classes dienen om zaken samen te zetten die conceptueel bij mekaar horen. Wel, de print functie hierboven dient slechts voor een enkel ding: het tonen van een persoon op het scherm. Daarom zou het beter zijn als deze functie ook een onderdeel was van de class `Person`.

<div class="note waarschuwing">
<p>Later zal je leren dat GUI functies net niet bij een class horen. De GUI en de rest van je programma moeten steeds gescheiden worden. Maar omdat we nu enkel met de console werken, en om de oefeningen eenvoudig te houden, maken we hier voorlopig een uitzondering.</p>
</div>

Je kan niet enkel properties, maar ook functies toevoegen aan een class. Dat heeft een groot voordeel: waar de print functie hierboven het object via een argument moest binnenkrijgen, heeft een class functie automatisch toegang tot alle properties van die class. De person class kan er dan zo uitzien:

```csharp
class Person
{
    public string Name { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }

    public void Print()
    {
        Console.WriteLine("Name: {0} {1}", FirstName, Name);
        Console.WriteLine("Age: {0}", Age);
    }
}
```

In het programma kunnen we nu de gegevens van een persoon printen door de `Print()` functie van de class te gebruiken:
```csharp
person1.Print();
person2.Print();
```

<div class="note oefening">
<p>Open het project **Oefening_Classes1** en maak oefenreeks 2.</p>
</div>

## Voorbeeld: class Point

Je leert natuurlijk pas goed met classes werken wanneer je er vaak mee in aanraking komt. Het vorige voorbeeld was zeer concreet: je weet wat een persoon is en je kan er je wel wat eigenschappen bij voorstellen. Maar zo eenvoudig is het niet altijd. Dikwijls representeert een class iets wat meer abstract is. Zo bevat C# classes die een internetverbinding voorstellen, of een JSON bestand, een databaseverbinding, enzovoort.

In dit deel zie je een uitgewerkt voorbeeld van een class voor het werken met posities in 2D. De class heeft enkele properties, maar vooral veel functies die het werken met posities eenvoudiger maken. Geef zeker aandacht aan de verschillende manieren waarop functies met argumenten en resultaten kunnen werken.

```csharp
class Point
{
    public float X { get; set; }
    public float Y { get; set; }

    public void Zero()
    {
        X = Y = 0f;
    }

    // De drie Set functies kunnen dezelfde naam hebben omdat de 
    // argumenten verschillend zijn.
    public void Set(float value)
    {
        X = Y = value;
    }

    public void Set(float x, float y)
    {
        X = x;
        Y = y;
    }

    // Je kan als argument ook de class zelf gebruiken. Zo kan je 
    // een ander object van dezelfde class doorgeven. In dit geval
    // maakt de functie dus een kopie.
    public void Set(Point other)
    {
        X = other.X;
        Y = other.Y;
    }

    // Deze functies lijken sterk op de Set functies. In dit geval
    // maken we een som. Je zou eenvoudig ook andere wiskundige 
    // bewerkingen kunnen toevoegen aan deze class.
    public void Add(float value)
    {
        X += value;
        Y += value;
    }

    public void Add(float x, float y)
    {
        X += x; Y += y;
    }

    public void Add(Point other)
    {
        X += other.X; Y += other.Y;
    }

    public float Average()
    {
        return (X + Y) / 2F;
    }

    // Deze functie gebruikt de class Point als resultaat. In de 
    // functie wordt een nieuw punt gemaakt dat dan als resultaat
    // van de functie gebruikt wordt.
    public Point Reversed()
    {
        Point result = new Point();
        result.X = Y; result.Y = X;
        return result;
    }

    public double Distance(Point other)
    {
        return Math.Sqrt(
            Math.Pow((other.X - X), 2) + Math.Pow((other.Y - Y), 2)
        );
    }
}
```

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-classes-1">oefening-classes-1</a> en maak de overige oefeningen.</p>
</div>