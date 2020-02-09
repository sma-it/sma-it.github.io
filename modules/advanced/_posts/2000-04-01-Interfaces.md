---
title: Interfaces
---

# Interfaces

Dikwijls wil je elementen in een verzameling plaatsen, zoals een `List`. Dat maakt het bijvoorbeeld veel eenvoudiger om een bepaalde functie uit te voeren voor alle elementen in die verzameling. Maar een `List` kan geen objecten van verschillende classen bevatten. Als je bijvoorbeeld cirkels en rechthoeken wil gebruiken, dan zal je daar 2 verschillende verzamelingen voor moeten maken.

Tenzij je Interfaces gebruikt! Door een interface te gebruiken kunnen de elementen van de verschillende classes via deze interface aangesproken worden. De interface geef aan welke functies en properties hiervoor in de classes moeten voorzien zijn. Via de functies en properties die in de interface staan, kunnen dan de elementen van de verschillende classes en hun respectievelijke functies en properties aangesproken worden. 

Enkele zaken om te onthouden:

- Het is de gewoonte om elke interface naam met een hoofdletter `I` te beginnen. Zo zie je achteraf duidelijk dat het een interface is.
- Interfaces kunnen functies en properties bevatten. Ze zijn automatisch `public`, dus dat moet je niet toevoegen.
- Interfaces bevatten enkel declaraties. Je werkt de functies van de interface dus nooit uit.

# Het principe van werken met een interface

Voorbeeld: We maken volgende interface voor een vlak:

```csharp
public interface ISurface {
    float Perimeter { get; }
    float Area();
}
```

De bovenstaande interface bevat twee functies, `Perimeter()` en `Area()`. 
Indien we via deze interface gebruik willen maken van verschillende classes dan moeten in deze classes de property Perimeter en de functie Area() uitgewerkt zijn.

Veronderstel dat we de volgende twee classes via deze interface willen aanspreken: Rectangle en Circle. Zowel in de class Rectangle als in de class Circle moet er een property Perimeter en een functie Area() zijn.

We maken dan een List van het type ISurface (de naam van de interface) en vullen die met Rectangle objecten en Circle objecten. Deze list kunnen we nu doorlopen en de property naam opvragen van het actieve element of er de functie Area() op toepassen. De interface zal zelf bepalen tot welke class het actieve element behoort en zal automatisch de property of functie uit die class oproepen. Voor een Circle object zal dat dus de Area() functie uit de class Circle zijn, voor een Rectangle object wordt dit de Area() functie uit de Rectangle class.

Besluit: Door zowel in de interface, als in de classes waaraan de interface toegevoegd werd functionaliteiten (properties, functies) met dezelfde naam toe te voegen, kunnen we via deze interface objecten van deze verschillende classes als één geheel aanspreken. Dit is het voordeel van werken met interfaces.

## Een Interface aan een Class toevoegen

Eens je een interface hebt, kan je een class declareren die de interface implementeert. Dat doe je door ze toe te voegen aan een class definitie:

```csharp
public class Rectangle : ISurface {

}
```
Visual Studio zal dadelijk opmerken dat je de interface niet uitgewerkt hebt, en stelt zelfs voor om de interface te implementeren. Als je daar mee akkoord gaat, dan ziet je class er zo uit:

```csharp
public class Rectangle : ISurface
{
    public float Perimeter => throw new NotImplementedException(); // Opvangen fout

    public float Area()
    {
        throw new NotImplementedException(); // Opvangen fout
    }
}
```

Je ziet dat de foutmelding weg is, maar je code zal wel een fout geven wanneer je ze uitvoert. Het is de bedoeling dat je de niet geïmplementeerde delen zelf verder uitwerkt. De class rechthoek zou er uiteindelijk zo kunnen uitzien:

```csharp
public class Rectangle : ISurface
{
    float width;
    float height;

    float perimeter;
    public float Perimeter => perimeter;

    public Rectangle(float width, float height)
    {
        this.width = width;
        this.height = height;

        perimeter = (width + height) * 2;
    }

    public float Area()
    {
        return width * height;
    }
}
```

Om de voordelen van interfaces uit te leggen, implementeren we deze interface nu ook voor een Cirkel:

```csharp
public class Circle : ISurface
{
    float radius;
    public float Radius => radius;

    float perimeter;
    public float Perimeter => perimeter;

    public Circle(float radius)
    {
        this.radius = radius;
        this.perimeter = 2 * (float)Math.PI * radius;
    }

    public float Area()
    {
        return (float)Math.PI * (float)Math.Pow(radius, 2);
    }
}
```

Ook `Circle` heeft nu een functie `Area()` en een property `Perimeter`. Merk op dat Circle ook een eigen constructor en een property `Radius` heeft. Een interface is tevreden wanneer je de gevraagde functies implementeert. Wat er verder nog in de class staat, dat maakt niet uit.

## Objecten met een Interface maken

We kunnen deze classes nu gebruiken door er objecten van te maken. Dat gaat niet anders dan bij een gewone class.

```csharp
Circle c = new Circle(3);
Console.WriteLine("My circle Area: " + c.Area());
Console.WriteLine("My circle Perimeter: " + c.Perimeter);

Rectangle r = new Rectangle(4, 5);
Console.WriteLine("My rectangle Area: " + r.Area());
Console.WriteLine("My rectangle Perimeter: " + r.Perimeter);
```

Maar hoe steek je ze nu in een list? Een list met cirkels kan immers geen rechthoeken bevatten. Wel, we kunnen nu een list maken met objecten die de interface `ISurface` implementeren. 

```csharp
var Surfaces = new List<ISurface>();

Surfaces.Add(new Circle(3));
Surfaces.Add(new Rectangle(4, 5));
```

Aangezien zowel `Circle` als `Rectangle` de interface `ISurface` implementeren kan je ze zonder problemen toevoegen aan de bovenstaande `List<ISurface>`. Let wel op: alhoewel de list aangeeft elementen van het type `ISurface` op te slaan, kan je van de interface zelf geen object maken. Dit werkt dus niet:

```csharp
Surfaces.Add(new ISurface()); // ISurface is geen class!
```

Je kan ook op de volgende manier een class maken die een verzameling van surfaces beheert:

```csharp
public class Surfaces
{
    List<ISurface> list = new List<ISurface>();

    public void Add(ISurface surface)
    {
        list.Add(surface);
    }

    // Als voorbeeld voegen we een functie TotalArea() toe die de totale
    // oppervlakte van alle elementen uit de List berekent en als
    // resultaat geeft.
    public float TotalArea()
    {
        float area = 0;
        foreach(var surface in list)
        {
            area += surface.Area();
        }
        return area;
    }
}
```

Wat ook niet kan, is properties of functies van de class gebruiken die niet tot de interface behoren. Zo heeft de class `Circle` ook een property `Radius`. Toch kan je die niet gebruiken, want die behoort niet tot de interface.

```csharp
public float TotalRadius() {
    float radius = 0;
    foreach(var circle in list) {   // Ook al vermelden we hier circle bij var,
                                    // dit is gewoon een variabelenaam en de rectangles
                                    // zullen nog steeds mee doorlopen worden.
        radius += circle.Radius;    // Dit zal niet werken! De rectangle elementen
                                    //bevatten immers geen property Radius.
    }
    return radius;
}
```

## Gebruik 'Interface as Class'

Toch is het soms handig als je ook de andere functies van een object kan gebruiken (die niet in de interface zitten), zelfs al _zie_ je enkel de interface. Hier ga je best niet mee overdrijven, maar als het aantal classes dat in je list zit, beperkt is, dan zou je de volgende functie kunnen toevoegen aan de `Surfaces` class hierboven.
De functie TotalRadius() berekent de som van de stralen (Radius) van alle circle-elementen uit de List. Het ligt voor de hand dat we een voorziening moeten inbouwen die de rectangles eruit filtert. Rectangles elementen hebben immers geen Radius property.

```csharp
public float TotalRadius()
{
    float radius = 0;
    foreach(var surface in list)
    {
        var element = surface as Circle; // Met deze lijn code geven we aan dat we
                                            // de variabele surface als een Circle willen
                                            // behandelen. Indien het element een Rectangle is
                                            // zal element op null geïnitialiseerd worden.

        if(element != null) // Enkel indien element niet null is, tellen we de Radius bij het totaal op.
        {                   // Element is niet null indien element een Circle is (zie uitleg hierboven).
            radius += element.Radius;
        }
    }
    return radius;
}
```

Hierboven maken we eerst een nieuwe variabele met `surface as Circle`. We vertellen zo dat we de huidige surface als een cirkel willen behandelen. Dat lukt bij de elementen die echt cirkels zijn. Andere elementen, zoals rechthoeken, kunnen niet omgezet worden en bijgevolg wordt `element` gelijk aan `null`. Null is een bijzondere waarde om aan te geven dat een variabele naar _niets_ verwijst.

Enkel wanneer de variabele naar iets verwijst, met andere woorden wanneer een Circle achter de interface zat, dan vragen we naar de `Radius` property.

<div class="note waarschuwing">
<p>Wanneer je de controle met null overslaat en je element blijkt geen cirkel te zijn, dan crasht je programma.</p>
</div>

## Interfaces Combineren

Je hoeft je ook niet te beperken tot een enkele interface. Hieronder voegen we een extra interface toe, die toelaat informatie over het object op het scherm te tonen.

```csharp
public interface IPrintable
{
    void Print();
}
```

Nu kunnen we een nieuwe class maken die beide interfaces implementeert:

```csharp
public class Triangle : ISurface, IPrintable
{
    float side1;
    float side2;
    float bottom;

    float perimeter;
    public float Perimeter => perimeter;

    public Triangle(float side1, float side2, float bottom)
    {
        this.side1 = side1;
        this.side2 = side2;
        this.bottom = bottom;

        perimeter = side1 + side2 + bottom;
    }

    public float Area()
    {
        float p = perimeter * 0.5f;
        return (float)Math.Sqrt(p * (p - side1) * (p - side2) * (p - bottom));
    }

    public void Print()
    {
        Console.WriteLine("Triangle with perimeter " + perimeter + " and area " + Area());
    }
}
```

Je kan nu de `Surfaces` class uitbreiden met deze functie:

```csharp
public void PrintAll()
{
    foreach(var surface in list)
    {
        var element = surface as IPrintable;
        if(element != null)
        {
            element.Print();
        }
    }
}
```

Je kan deze controle trouwens ook op een andere manier uitvoeren:

```csharp
public void PrintAll()
{
    foreach(var surface in list)
    {
        if(surface is IPrintable)
        {
            (surface as IPrintable).Print();
        }
    }
}
```

Beide opties doen hetzelfde. Welke je gebruikt hangt enkel af van je persoonlijke voorkeur.

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-interface-1">oefening-interface-1</a> en maak de oefeningen.</p>
</div>
