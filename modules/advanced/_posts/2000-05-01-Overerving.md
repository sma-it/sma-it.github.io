---
title: Overerving
---

# Wat is overerving?

Een krachtig aspect van object georiënteerd programmeren is __overerving__. Overerving laat toe een aantal gemeenschappelijke zaken (properties en functies) in een `basisklasse` te zetten. Van deze `basisklasse` kunnen dan `afgeleide klassen` gemaakt worden. Deze `afgeleide klassen` bevatten dankzij de overerving, naast hun eigen properties en functies, ook alle properties en functies van de `basisklasse`.

# Voorbeeld
We verklaren het principe van overerving aan de hand van een voorbeeld:

## Sitatieschets
Veronderstel dat je volgende gegevens wil bijhouden over dieren: 'aantal poten', 'kan het dier vliegen' en de 'levensverwachting'. Voor honden willen we ook het 'ras' bijhouden en voor vogels de 'kleurencombinatie' van de veren.

We willen het 'aantal poten', het 'kunnen vliegen' en de 'levensverwachting' op het scherm kunnen tonen. Ook het geluid dat de hond (Bark! Bark!) en de vogel (Tsjilp! Tsjilp!) maken, willen we op het scherm tonen.

## Opsplitsing in basisklasse en afgeleide klassen
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

De syntax om een klasse af te leiden van een andere klasse is:

```
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

        public string AsText() // Override van de default ToSTring() functie voorzien in C#
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
        //afhangt van het ras (breed).
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
<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-inheritance-1">oefening-inheritance-1</a> en maak de oefeningen.</p>
</div>

