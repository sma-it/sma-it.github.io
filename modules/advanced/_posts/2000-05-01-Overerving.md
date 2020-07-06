---
title: Overerving
---

<div class="header1" id="top" markdown = "1"># Overerving
</div>

<div class="header2" markdown = "1">## Wat is overerving?
</div>

Een krachtig aspect van object georiënteerd programmeren is __overerving__. Overerving laat toe een aantal gemeenschappelijke zaken (properties en functies) in een `basisklasse` te zetten. Van deze `basisklasse` kunnen dan `afgeleide klassen` gemaakt worden. Deze `afgeleide klassen` bevatten dankzij de overerving, naast hun eigen properties en functies, ook alle properties en functies van de `basisklasse`.

<div class="header2" markdown = "1">## Voorbeeld
</div>
We verklaren het principe van overerving aan de hand van een voorbeeld:

### Situatieschets
Veronderstel dat je volgende gegevens wil bijhouden over dieren: 'aantal poten', 'kan het dier vliegen' en de 'levensverwachting'. Voor honden willen we ook het 'ras' bijhouden en voor vogels de 'kleurencombinatie' van de veren.

We willen het 'aantal poten', het 'kunnen vliegen' en de 'levensverwachting' op het scherm kunnen tonen. Ook het geluid dat de hond (Bark! Bark!) en de vogel (Tsjilp! Tsjilp!) maken, willen we op het scherm tonen.

### Opsplitsing in basisklasse en afgeleide klassen
- __Hoe bepalen we wat tot de basisklasse behoort?__

  Dit doen we door de gemeenschappelijke delen (properties en functies) af te zonderen. Uit de situatieschets kunnen we afleiden dat we voor elk dier de volgende properties willen bijhouden:
  - aantal poten
  - kan het vliegen
  - de levensverwachting 
  
  Tevens willen we deze drie properties voor alle dieren naar string-formaat kunnen omzetten zodat we ze via Console.WriteLine() op het scherm kunnen tonen.
  
  Deze drie properties en de functie om de drie properties naar string-formaat te kunnen omzetten zijn de __gemeenschappelijke delen__ voor zowel honden als volgels.
  Deze __gemeenschappelijke delen__ zonderen we af en zetten we ineen aparte `basisklasse`. Deze `basisklasse` geven we een algemene naam, bijvoorbeeld __Animal__.

- __Wat zit er in de afgeleide klassen?__

    Nu de gemeenschappelijke delen afgezonderd zijn, kijken we wat er nog ontbreekt om al de gevraagde informatie en functionaliteit te kunnen implementeren in het programma. De volgende zaken ontbreken nog:
    - het ras van de hond
    - de kleurencombinatie van de vogel
    - het tonen van het geluid van de hond (Bark! Bark!)
    - het tonen van het geluid van de vogel (Tsjilp! Tsjilp!)

    Dit zijn de gegevens die we in de `afgeleide klassen` zullen moeten opnemen om het gevraagde uit de situatieschets volledig kunnen uit te werken. Concreet houdt dit het volgende in:
    - de afgeleide klasse Dog zal een eigen property 'Breed' hebben en een functie Talk() die 'Bark! Bark' op het scherm toont.
    - de afgeleide klasse Bird zal een eigen property 'Color' hebben en een functie Talk() die 'Tsjilp! Tsjilp!' op het scherm toont.

    Naast deze eigen properties en een eigen functie Talk() beschikken de afgeleide klassen ook over alle properties en functies uit de basisklasse.

### Uitwerking

De syntax om een klasse af te leiden van een andere klasse is:

```csharp
class Dog : Animal   // Na het dubbelpunt wordt de basisklasse vermeld.
{                      // Dit zorgt ervoor dat Dog een afgeleide klasse van Animal is.
    // Hier wordt de class Dog uitgewerkt.
}
```

Hieronder het volledig uitgewerkte voorbeeld.


```csharp
// De basisklasse Animal
class Animal
{
    public int Legs { get; set; }
    public bool CanFly { get; set; }
    public float LifeExpectancy { get; set; }

    public string AsText() 
    {
        string fly = "cannot";
        if (CanFly)
        {
            fly = "can";
        }
        return "This animal has " + Legs + " legs and " + fly + " fly.";
    }

}

// De klasse Dog is een afgeleide klasse van Animal.
class Dog : Animal
{
    // De klasse Dog erft de properties van de klasse Animal, 
    // maar heeft ook een eigen property, nl. Breed.
    public string Breed { get; set; }

    // Constructor: merk op dat de properties van de basisklasse ook geïnitialiseerd worden
    // via deze constructor. Omdat een hond standaard 4 poten heeft en niet kan vliegen
    // moeten we hiervoor geen argumenten voorzien, maar geven we de waarden 
    // in de constructor vast in. Voor LifeExpectancy doen we dit niet aangezien dit vaak 
    // afhangt van het ras (breed).
    public Dog(int lifeExpectancy, string breed)
    {
        Legs = 4;
        CanFly = false;
        LifeExpectancy = lifeExpectancy;
        Breed = breed;
    }

    // De klasse Dog erft de functies van de klasse Animal, 
    // maar heeft ook een eigen functie Talk().
    public string Talk()
    {
        return "Bark! Bark!";
    }
}

// De klasse Bird is een afgeleide klasse van Animal.
class Bird : Animal
{
    // De klasse Bird erft de properties van de klasse Animal, 
    // maar heeft ook een eigen property, nl. Color.
    public string Color { get; set; }

    // Constructor: merk op dat de properties van de basisklasse ook geïnitialiseerd worden
    // via deze constructor. Omdat een vogel standaard 2 poten heeft en kan vliegen
    // moeten we hiervoor geen argumenten voorzien, maar geven we de waarden in de 
    // constructor vast in. Voor LifeExpectancy doen we dit niet omdat we veronderstellen 
    // dat dit afhangt van de kleur (Color). Een opvallende kleur = makkelijker gevangen 
    // worden door een roofvogel.
    public Bird(int lifeExpectancy, string color)
    {
        Legs = 2;
        CanFly = true;
        LifeExpectancy = lifeExpectancy;
        Color = color;
    }

    // De klasse Bird erft de functies van de klasse Animal, 
    // maar heeft ook een eigen functie Talk().
    public string Talk()
    {
        return "Tsjilp! Tsjilp!";
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Van elke klasse wordt een object gemaakt.
        // Indien de constructor van de klasse argumenten vereist worden
        // deze meegegeven.
        // Merk op dat er in de klasse Animal geen constructor staat, hier
        // wordt dus de door C# voorziene default constructor gebruikt.
        Animal dier = new Animal();
        Dog hond = new Dog(14, "herdershond");
        Bird vogel = new Bird(3, "Rood/groen");

        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object dier van de klasse Animal:");
        Console.WriteLine("-----------------------------------------------");
        // Het object dier wordt op het scherm getoond a.h.v.
        // de functie AsText() uit de klasse Animal waartoe het dier behoort.
        Console.WriteLine(dier.AsText());

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object hond van de klasse Dog:");
        Console.WriteLine("-----------------------------------------------");
        // Het object hond wordt op het scherm getoond a.h.v.
        // de functie AsText() uit de basisklasse Animal.
        Console.WriteLine(hond.AsText());

        // De functie Talk() uit de klasse Dog wordt op het
        // object hond toegepast.
        Console.WriteLine(hond.Talk());

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object vogel van de klasse Bird:");
        Console.WriteLine("-----------------------------------------------");
        // Het object vogel wordt op het scherm getoond a.h.v.
        // de functie AsText() uit de basisklasse Animal.
        Console.WriteLine(vogel.AsText());

        // De functie Talk() uit de klasse Bird wordt op het
        // object vogel toegepast.
        Console.WriteLine(vogel.Talk());

        Console.ReadKey();
    }
}
```

De uitvoer van dit programma is:

```
-----------------------------------------------
Info over het object dier van de klasse Animal:
-----------------------------------------------
This animal has 0 legs and cannot fly.

-----------------------------------------------
Info over het object hond van de klasse Dog:
-----------------------------------------------
This animal has 4 legs and cannot fly.
Bark! Bark!

-----------------------------------------------
Info over het object vogel van de klasse Bird:
-----------------------------------------------
This animal has 2 legs and can fly.
Tsjilp! Tsjilp!
```

<div class="note protip">
<p>Indien je een project uitwerkt, is het bepalen van de classes die je nodig hebt, een belangrijke eerste stap. Gebruik hierbij overerving waar mogelijk.</p>
</div>

<div class="header2" markdown = "1">## Gebruik van constructors bij overerving
</div>

In het voorbeeld dat hierboven besproken wordt, heeft de basisklasse geen eigen constructor (buiten de default constructor die door C# zelf voorzien wordt). De properties die tot de basisklasse behoren worden geïnitialiseerd in de constructor van de afgeleide klassen.

Het is echter mogelijk om in de basisklasse een niet-default constructor te voorzien en deze in de constructor van de afgeleide klassen te gebruiken. Bij het maken van een object van een afgeleide klasse zal steeds eerst de constructor van de basisklasse uitgevoerd worden, daarna de constructor van de afgeleide klasse. Op die manier wordt er een 'volledig' object van de afgeleide klasse bekomen.

We onderscheiden dus twee mogelijkheden:
- De basisklasse heeft een default constructor.
- De basisklasse heeft geen default constructor.

### De basisklasse heeft geen eigen constructor

Dit hoofdstuk startte met een voorbeeld waarbij de basisklasse geen default constructor heeft. De constructor in de afgeleide klassen ziet er als volgt uit (bv. de class dog):

```csharp
public Bird(int lifeExpectancy, string color)
{
    Legs = 2;
    CanFly = true;
    LifeExpectancy = lifeExpectancy;
    Color = color;
}
```
De properties Legs en CanFly behoren tot de basisklasse, maar worden door de constructor van de afgeleide klasse geïnitialiseerd.

### De basisklasse heeft een eigen constructor

Indien we de basisklasse Animal uit het voorbeeld wel voorzien van een constructor dan ziet het voorbeeld er als volgt uit:

```csharp
class Animal
{
    public int Legs { get; set; }
    public bool CanFly { get; set; }
    public float LifeExpectancy { get; set; }

    // Niet-default constructor in basisklasse
    public Animal(int legs, bool canFly, float lifeExpectancy)
    {
        Legs = legs;
        CanFly = canFly;
        LifeExpectancy = lifeExpectancy;
    }

    public string AsText()
    {
        string fly = "cannot";
        if (CanFly)
        {
            fly = "can";
        }
        return "This animal has " + Legs + " legs and " + fly + " fly.";
    }

}

class Dog : Animal
{
    public string Breed { get; set; }

    // Constructor: de basisklasse Animal heeft een eigen niet-default constructor. 
    // In de constructor van de afgeleide klasse Dog roepen we deze constructor 
    // op (na de dubbelpunt) d.m.v. het keyword 'base'. Let in onderstaand
    // voorbeeld goed op het gebruik van argumenten. De constructor van de afgeleide 
    // klasse Dog heeft in de argumentenlijst eveneens de argumenten van de basisklasse 
    // Animal staan. Deze worden doorgegeven aan de constructor van de basisklasse die 
    // na de dubbelpunt vermeld staat. 
    // Bij wijze van voorbeeld gebruiken we voor de properties Legs en canFly nu geen vaste
    // waarden (in tegenstelling tot het voorbeeld waarmee we begonnen in dit hoofdstuk).
    // We initialiseren deze gegevens nu ook d.m.v. argumenten. Onthou dat initialisatie op 
    // vaste waarden hier ook nog altijd kan.
    // In de body van de constructor van de afgeleide klasse Dog wordt enkel nog de property 
    // die eigen is aan de klasse zelf geïnitialiseerd. 
    public Dog(int legs, bool canFly, float lifeExpectancy, string breed) : base(legs, canFly, lifeExpectancy)
    {
        Breed = breed;
    }

    // De klasse Dog erft de functies van de klasse Animal, 
    // maar heeft ook een eigen functie Talk().
    public string Talk()
    {
        return "Bark! Bark!";
    }
}

class Bird : Animal
{
    public string Color { get; set; }

    // Constructor: zie klasse Dog voor de verklaring van deze constructor.
    public Bird(int legs, bool canFly, float lifeExpectancy, string color) : base(legs, canFly, lifeExpectancy)
    {

        Color = color;
    }

    public string Talk()
    {
        return "Tsjilp! Tsjilp!";
    }
}

class Program
{
    static void Main(string[] args)
    {
            
        // Let op de argumenten die meegegeven worden. Alle argumenten die door de
        // constructors verwacht worden, zijn voorzien in de argumentenlijst.
        Animal dier = new Animal(0, false, 0f);
        Dog hond = new Dog(4, false, 14, "herdershond");
        Bird vogel = new Bird(2, true, 3, "Rood/groen");

        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object dier van de klasse Animal:");
        Console.WriteLine("-----------------------------------------------");
            
        Console.WriteLine(dier.AsText());

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object hond van de klasse Dog:");
        Console.WriteLine("-----------------------------------------------");
           
        Console.WriteLine(hond.AsText());

        Console.WriteLine(hond.Talk());

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object vogel van de klasse Bird:");
        Console.WriteLine("-----------------------------------------------");
           
        Console.WriteLine(vogel.AsText());

        Console.WriteLine(vogel.Talk());

        Console.ReadKey();
    }
}
}
```
<div class="header2" markdown = "1">## Hergebruik van functies bij overerving
</div>

De mogelijkheid om functies uit de basisklasse te hergebruiken in de afgeleide klassen zorgt ervoor dat de code zo efficiënt mogelijk gehouden wordt.
Om dit te illustreren passen we het voorbeeld van hierboven als volgt aan:
In elke klasse wordt een functie Print() toegevoegd die de properties van de klasse op het scherm toont. In de klassen Dog en Bird zal gebruik gemaakt worden van de Print-functie van de basisklasse Animal om de properties Legs, CanFly en LifeExpectancy op het scherm te tonen. Deze werkwijze zorgt ervoor dat de Print-functies zo efficiënt mogelijk opgesteld kunnen worden. Er moet namelijk maar één set uitvoerinstructies voorzien worden voor deze drie properties, namelijk in de basisklasse Animal. De afgeleide klassen kunnen van deze set instructies gebruik maken door de Print-functie van Animal in hun eigen Print-functie te implementeren. Dit is eenvoudiger en efficiënter dan in elke Print-functie telkens opnieuw deze drie properties via Console.WriteLine() op het scherm te tonen.

Het voorbeeld ziet er als volgt uit:

```csharp
class Animal
{
    public int Legs { get; set; }
    public bool CanFly { get; set; }
    public float LifeExpectancy { get; set; }

    public Animal(int legs, bool canFly, float lifeExpectancy)
    {
        Legs = legs;
        CanFly = canFly;
        LifeExpectancy = lifeExpectancy;
    }

    // De functie AsText() is vervangen door de functie Print() die de properties 
    // van de basisklasse op het scherm toont.
    public void Print()
    {
        Console.WriteLine("Legs: " + Legs);
        Console.WriteLine("Fly: " + CanFly);
        Console.WriteLine("Life expectancy: " + LifeExpectancy);
    }

}

class Dog : Animal
{
    public string Breed { get; set; }

    public Dog(int legs, bool canFly, float lifeExpectancy, string breed) : base(legs, canFly, lifeExpectancy)
    {
        Breed = breed;
    }

    // De functie Print() wordt toegevoegd, deze toont de properties van een 
    // Dog object op het scherm. Aangezien er in de basisklasse Animal reeds 
    // een functie met deze naam bestaat, is het nodig om
    // het keyword 'new' toe te voegen aan de declaratie van de functie.
    // De Print-functie uit de basisklasse Animal wordt opgeroepen om de properties die 
    // tot de basisklasse behoren op het scherm te tonen.
    // De syntax die gebruikt wordt om een functie uit de basisklasse op te roepen is:
    // base.naamFunctie()
    // Daarna worden de properties van de afgeleide klasse via Console.WriteLine()
    // op het scherm getoond.
    // Hier wordt deze werkwijze toegepast op de Print-functie.

    public new void Print()
    {
        base.Print();
        Console.WriteLine("Breed: " + Breed);
    }

    public string Talk()
    {
        return "Bark! Bark!";
    }
}

class Bird : Animal
{
    public string Color { get; set; }

    public Bird(int legs, bool canFly, float lifeExpectancy, string color) : base(legs, canFly, lifeExpectancy)
    {
        Color = color;
    }

    // Werkwijze Print-functie: zie klasse Dog.

    public new void Print()
    {
        base.Print();
        Console.WriteLine("Color: " + Color);
    }

    public string Talk()
    {
        return "Tsjilp! Tsjilp!";
    }
}

class Program
{
    static void Main(string[] args)
    {
        Animal dier = new Animal(0, false, 0f);
        Dog hond = new Dog(4, false, 14, "herdershond");
        Bird vogel = new Bird(2, true, 3, "Rood/groen");

        // In wat volgt worden de Print-functies op de verschillende objecten uitgevoerd.
        // Daarnaast wordt via de Talk-functies van de hond en de vogel ook het geluid van
        // deze dieren getoond.
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object dier van de klasse Animal:");
        Console.WriteLine("-----------------------------------------------");

        dier.Print();

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object hond van de klasse Dog:");
        Console.WriteLine("-----------------------------------------------");

        hond.Print();
        Console.WriteLine(hond.Talk());

        Console.WriteLine();
        Console.WriteLine("-----------------------------------------------");
        Console.WriteLine("Info over het object vogel van de klasse Bird:");
        Console.WriteLine("-----------------------------------------------");

        vogel.Print();
        Console.WriteLine(vogel.Talk());

        Console.ReadKey();
    }
}
```

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-overerving-1">oefening-overerving-1</a> en maak de oefeningen.</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>
