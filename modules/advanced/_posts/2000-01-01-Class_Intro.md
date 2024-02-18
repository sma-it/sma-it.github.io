---
title: Classes
---
<div class="header1" id="top" markdown = "1"># Classes
</div>

Een `class` is een verzameling van data en functies die conceptueel bij mekaar horen. In de vorige hoofdstukken maakte je al kennis met classes in C#. `Console` is bijvoorbeeld een class, maar ook `String` en `DateTime` zijn classes. En zelfs de `Main` functie in een programma maakt deel uit van een class.

Neem bijvoorbeeld de class `DateTime`. Deze class heeft properties, zoals `Day`, `Minute`, `Year`, `DayOfWeek`, enzovoort. En daarnaast voorziet de class functies, zoals `AddDays()`, `CompareTo()` en `ToLocalTime()`. Als we zeggen dat deze functies en properties conceptueel bij mekaar horen, dan bedoelen we dat ze allemaal met het concept *tijd* te maken hebben. Die samenhang is heel belangrijk om een programma of een software library overzichtelijk te houden: als iets niet duidelijk verwant is, dan plaatsen we het niet in dezelfde class.

<div class="header2" markdown = "1">## Een class maken
</div>

Bij het maken van een class zal je twee zaken aan de class toevoegen: properties en functies.

### Properties toevoegen aan een class

Tot hiertoe gebruikte je af en toe bestaande classes. Nu leer je hoe je zelf nieuwe classes maakt. Wanneer een programma groter wordt, dan is het bijna onmogelijk om het overzicht te bewaren zonder je eigen code in classes te plaatsen. Wanneer je bijvoorbeeld gegevens over personen moet verwerken in je programma, dan zou het logisch zijn dat je een class maakt waarin je gegevens over die persoon kan opslaan. De definitie van een class kan bijna overal, maar moet wel binnen een namespace zitten:

```csharp
namespace MijnProgramma 
{
    public class Persoon
    {
        // hier komt de inhoud van je class
    }
}
```
<div class="note protip">
<p>Je kan een class samen met andere data (bv. andere classes) in een bestand zetten. En bij oefeningen in deze cursus vragen we je dikwijls om dat te doen omdat dat eenvoudiger is om te verbeteren. Maar wanneer je aan een echt programma werkt dan zal je bijna altijd een bestand maken voor elke class, waarbij de bestandsnaam en de class naam dezelfde zijn.</p>
</div>

Met een lege class ben je natuurlijk niet veel. Als voorbeeld gaan we enkele properties toevoegen. Dit zijn de eigenschappen van een persoon die we willen onthouden. We starten met naam, voornaam en leeftijd. _(De namespace laten we vanaf nu achterwege om de voorbeelden kort te houden.)_

```csharp
public class Person 
{
    // Properties
    public string Name { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }
}
```

Een property bestaat dus uit de volgende onderdelen:
* **public:** Hiermee geef je aan dat de property publiek is. Deze instelling heeft te maken met hoe een property een waarde kan krijgen en geraadpleegd kan worden. Je leert hierover meer in het volgende hoofdstuk. 
* **type:** Het type van de property, zoals int, float of string. Maar je zal later zien dat dit ook een andere class kan zijn.
* **naam:** De naam van de property zal je later gebruiken om de waarde op te vragen, net zoals je dat bij een gewone variabele doet.
* **{ get; set; }** Hier komen we in het volgende hoofdstuk over properties op terug. De vermelding van `get` EN `set` zorgt er voor dat je de waarde van de property kan opvragen EN wijzigen.

<div class="note protip">
<p>Visual Studio voorziet een handige shortcut voor het maken van properties. Typ `prop` en druk vervolgens twee maal op _tab_. De nodige code wordt automatisch aangevuld, en het woord `int` is geselecteerd. Typ nu het type en druk opnieuw twee maal op _tab_. Nu is de naam geselecteerd. Typ de naam en druk twee maal op enter. De cursor staat nu op de volgende regel, klaar voor de volgende property.</p>
</div>

### Functies in een class

Een class kan naast properties ook functies bevatten. Deze functies kunnen gebruikt worden om acties op de objecten van de class uit te voeren. Als voorbeeld maken we een functie Print() die alle properties van een object van de class Person op het scherm toont.

```csharp
public class Person
{
    // Properties
    public string Name { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }

    // De functie Print()
    public void Print()
    {
        Console.WriteLine("Name: {0} {1}", FirstName, Name);
        Console.WriteLine("Age: {0}", Age);
    }
}
```
<div class="note waarschuwing">
<p>Later zal je leren dat GUI (GUI=Graphical User Interface) functies, zoals deze Print()-functie, niet bij de class zelf horen. De GUI en de rest van je programma moeten steeds gescheiden worden. Maar omdat we nu enkel met de console werken, en om de oefeningen eenvoudig te houden, maken we hier voorlopig een uitzondering.</p>
</div>


<div class="header2" markdown = "1">## Een class gebruiken
</div>

Eens je de code voor de class geschreven hebt, kan je deze gebruiken. Je kan objecten van de class maken en hierop de functies van de class toepassen.

### Een object van een class maken

Wanneer je een class maakt, dan vertel je de compiler hoe een object eruit ziet. Je maakt eigenlijk een definitie, of een blueprint. Maar om de class te gebruiken zal je een _instance_, of een `object`, moeten maken van de class. Je kent dit principe al, want ook `DateTime` verwacht dat je een object maakt:

```csharp
DateTime date = new DateTime();
```

Van de class `Person` maken we op dezelfde manier een object:

```csharp
Person persoon = new Person();  //Hierin is Person het gegevenstype (de class) en persoon de 
                                //naam van het object dat gemaakt wordt.
```

Je kan op allerlei plaatsen in je programma op deze manier objecten maken: in andere classes en in de functie Main().

### Een object initialiseren

Eens we een object hebben, kunnen we de properties van dat object aanpassen. Hieronder vind je een voorbeeld van een functie Main die gebruik maakt van de class Person die in de voorbeelden hierboven uitgewerkt werd.
In de Main-functie gebeurt het volgende:
* Er worden twee objecten van de class Person gemaakt. Deze objecten hebben de namen person1 en person2.
* Beide objecten worden afzonderlijk geïnitialiseerd. Dit gebeurt door van elk object elke property apart een waarde te geven. De properties van een object kan je aanspreken met de syntax `objectNaam.propertyNaam`. We merken hierbij dadelijk op dat je in volgende voorbeelden zal zien dat je deze manier van initialiseren zal vervangen door een initialisatie d.m.v. een functie.
* Beide objecten worden op het scherm getoond door op elk object de functie Print() toe te passen. Let op de syntax, je past een functie als volgt op een object toe: `objectNaam.FunctieNaam()`.

```csharp
public class Program
{
    static void Main(string[] args)
    {
        //Maken van de objecten person1 en person2
        Person person1 = new Person();
        Person person2 = new Person();

        //Initialisatie object person1
        person1.FirstName = "Steve";
        person1.Name = "Jobs";
        person1.Age = 56;

        //Initialisatie object person2
        person2.FirstName = "Bill";
        person2.Name = "Gates";
        person2.Age = 68;

        //De objecten person1 en person2 op het scherm tonen d.m.v. 
        //de functie Print() van de class Person
        person1.Print();
        person2.Print();

        Console.ReadKey();
    }
}

```

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-classes-1" target="_blank">oefening-classes-1</a> via github en maak oefening 1a en 1b.</p>
</div>


<div class="header2" markdown = "1">## Een tweede voorbeeld: class Point
</div>

Je leert natuurlijk pas goed met classes werken wanneer je er vaak mee in aanraking komt. Het vorige voorbeeld was zeer concreet: je weet wat een persoon is en je kan er je wel wat eigenschappen bij voorstellen. Maar zo eenvoudig is het niet altijd. Dikwijls representeert een class iets wat meer abstract is. Zo bevat C# classes die een internetverbinding voorstellen, een databaseverbinding, enzovoort.

In dit deel zie je een uitgewerkt voorbeeld van een class voor het werken met posities in 2D. De class heeft enkele properties, maar vooral veel functies die het werken met posities eenvoudiger maken. Geef zeker aandacht aan de verschillende manieren waarop functies met argumenten en resultaten kunnen werken.

```csharp
class Point
{
    //Properties
    public float X { get; set; }
    public float Y { get; set; }

    //Functies

    //De functie Zero() initialiseert de properties X en Y beiden op 0f.
    public void Zero()
    {
        X = Y = 0f;
    }

    /* Begin Set-functies: 
    */
    // Hieronder vind je 3 functies met de naam Set. Dit type functie wordt 
    // gebruikt om één of meerdere properties van een object een waarde te geven via één of 
    // meerdere functieargumenten. 
    // In dit voorbeeld worden X en Y geïnitialiseerd a.h.v. de functieargument(en). 
    

    // De drie Set functies kunnen dezelfde naam hebben omdat de 
    // argumenten verschillend zijn. (function overloading)

    // Set functie versie 1: X en Y krijgen dezelfde waarde via het argument value.
    public void Set(float value)
    {
        X = Y = value;
    }

    // Set functie versie 2: X en Y krijgen elk een verschillende waarde. 
    // X krijgt de waarde van x en Y krijgt de waarde van y.
    public void Set(float x, float y)
    {
        X = x;
        Y = y;
    }

    // Je kan als argument ook een object van de class zelf gebruiken. Zo kan je 
    // een bestaand object kopiëren in een ander object.
    // X wordt geïnitialiseerd op de X-property van het object other dat als functieargument
    // meegegeven wordt. Y wordt geïnitialiseerd op de Y-property van dit object.
    public void Set(Point other)
    {
        X = other.X;
        Y = other.Y;
    }

    /* Einde Set-functies.
    */

    /* Hieronder vind je andere functies die tot de class behoren. Zo zijn er functies die 
     * de properties wijzigingen en functies die andere functionaliteiten hebben.
     */

    // -> Functies die de properties wijzigen.

    // Bij de properties X en Y wordt telkens dezelfde waarde geteld, 
    // nl. het functieargument value.
    public void Add(float value)
    {
        X += value;
        Y += value;
    }

    // Bij de properties X en Y worden respectievelijk functieargument x 
    // en functieargument y opgeteld.
    public void Add(float x, float y)
    {
        X += x; 
        Y += y;
    }

    // Bij de properties X en Y worden respectievelijk de X-property en de Y-property  
    // van het object dat als functieargument meegegeven wordt, opgeteld.
    public void Add(Point other)
    {
        X += other.X; 
        Y += other.Y;
    }

    // -> Functie die het gemiddelde van de X en Y-coördinaat berekent.
    public float Average()
    {
        return (X + Y) / 2F;
    }

    // -> Deze functie heeft de class Point als functieresultaat. In de 
    // functie wordt een nieuw tijdelijk punt gemaakt dat dan als functieresultaat
    // van de functie gebruikt wordt. Dit nieuwe punt heeft de omgekeerde
    // coördinaten van het punt waarop de functie toegepast wordt.
    public Point Reversed()
    {
        Point result = new Point(); // Het nieuwe tijdelijke Point-object wordt gemaakt.
        result.X = Y; 
        result.Y = X;
        return result;
    }

    // -> Deze functie berekent de afstand tussen 2 punten. De functie wordt toegepast op 
    // het ene punt en het tweede punt wordt als argument meegegeven.
    // De afstand tussen 2 punten wordt berekend met de volgende wiskunde bewerking:
    // afstand = vierkantswortel(((x2-x1)^2 + (y2-y1)^2))
    public double Distance(Point other)
    {
        return Math.Sqrt(Math.Pow((other.X - X), 2) + Math.Pow((other.Y - Y), 2));
    }
}
```
In Main kunnen we deze class bijvoorbeeld als volgt gebruiken:

```csharp
public class Program
{
    static void Main(string[] args)
    {
        //Maken van de objecten point1, point2, point3 en point4
        Point point1 = new Point();
        Point point2 = new Point();
        Point point3 = new Point();
        Point point4 = new Point();

        //Initialisatie object point1 d.m.v. Set-functie met 1 argument
        point1.Set(3);

        //Initialisatie object point2 d.m.v. Set-functie met 2 argumenten
        point2.Set(10,16);

        //Initialisatie van object point3 d.m.v. Set-functie met een Point-argument.
        //We kopiëren hier point1 in point3.
        point3.Set(point1);

        //Initialisatie van object point4 d.m.v. Set-functie die een Point-object als 
        //returnwaarde geeft.
        point4=point2.Reversed();

        Console.ReadKey();
    }
}

```
<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-classes-1" target="_blank">oefening-classes-1</a> en maak de overige oefeningen.</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>