---
title: Interfaces
---

<div class="header1" id="top" markdown = "1"># Interfaces
</div>

<div class="header2" markdown = "1">## Waarom een interface?
</div>

Dikwijls wil je elementen in een verzameling plaatsen, zoals een `List`. Dat maakt het bijvoorbeeld veel eenvoudiger om een bepaalde functie uit te voeren voor alle elementen in die verzameling. Maar een `List` kan geen objecten van verschillende classen bevatten. Als je bijvoorbeeld cirkels en rechthoeken wil gebruiken, dan zal je daar 2 verschillende verzamelingen voor moeten maken.

Tenzij je Interfaces gebruikt! Door een interface te gebruiken kunnen de elementen van de verschillende classes via deze interface aangesproken worden. De interface geef aan welke functies en properties hiervoor in de classes moeten voorzien zijn. Via de functies en properties die in de interface staan, kunnen dan de elementen van de verschillende classes en hun respectievelijke functies en properties aangesproken worden. 

Enkele zaken om te onthouden:

- Het is de gewoonte om elke interface naam met een hoofdletter `I` te beginnen. Zo zie je achteraf duidelijk dat het een interface is.
- Interfaces kunnen functies en properties bevatten. Ze zijn automatisch `public`, dus dat moet je niet toevoegen.
- Interfaces bevatten enkel declaraties. Je werkt de functies van de interface dus nooit uit, dit doe je in de classes die je via de interface wil aanspreken.

<div class="header2" markdown = "1">## Het principe van werken met een interface
</div>

Voorbeeld: We maken volgende interface voor een vlak. Van het vlak voorzien we in de interface de omtrek (Perimeter) en de oppervlakte (Area).

Een nieuwe interface maak je door in de Solution Explorer rechts op je project te klikken en via 'Add -> New item' voor 'Interface' te kiezen. Je geeft in dit venster de interface de gewenste naam. In ons voorbeeld wordt dit `ISurface`.

Deze nieuwe interface werken we als volgt uit:

```csharp
public interface ISurface {
    float Perimeter { get; }
    float Area();
    string AsText();
}
```

De bovenstaande interface bevat een property `Perimeter()`, een functie `Area()` en een functie `AsText()`. 
Indien we via deze interface gebruik willen maken van verschillende classes dan moeten in deze classes de property Perimeter, de functie Area() en de functie AsText() uitgewerkt zijn.

Veronderstel dat we de volgende twee classes via deze interface willen aanspreken: `Rectangle` en `Circle`. Zowel in de class Rectangle als in de class Circle moet er een property `Perimeter`, een functie `Area()` en een functie `AsText()` zijn.

We maken dan een List van het type ISurface (de naam van de interface) en vullen die met Rectangle objecten en Circle objecten. Deze list kunnen we nu doorlopen en op het actieve element telkens bijvoorbeeld de functie Area() toepassen. De interface zal zelf bepalen tot welke class het actieve element behoort en zal automatisch de functie Area() uit die class oproepen. Voor een Circle object zal dat dus de Area() functie uit de class Circle zijn, voor een Rectangle object wordt dit de Area() functie uit de Rectangle class.

__Besluit: Door zowel in de interface, als in de classes waaraan de interface toegevoegd werd, functionaliteiten (properties, functies) met dezelfde naam toe te voegen, kunnen we via deze interface objecten van deze verschillende classes via een List als één geheel aanspreken. Dit is het voordeel van werken met interfaces.__

<div class="header2" markdown = "1">## Een Interface aan een Class toevoegen
</div>

Eens je een interface hebt, kan je een class declareren die de interface implementeert. Dat doe je door ze toe te voegen aan een class definitie:

```csharp
public class Rectangle : ISurface {

}
```
Visual Studio zal dadelijk opmerken dat je de interface nog niet uitgewerkt hebt in deze class en onderlijnt de interface met een rode, squiggly lijn. Je kan ervoor kiezen om Visual Studio de basis voor de interface zelf te laten implementeren. Hover met de muis over de rood onderlijnde naam van de interface, klik op het gele lampje dat verschijnt en kies uit het menu dat nu verschijnt 'Implement interface'. Je class ziet er nu zo uit:

```csharp
public class Rectangle : ISurface
{
    public float Perimeter => throw new NotImplementedException(); 

    public float Area()
    {
        throw new NotImplementedException(); 
    }

    public string AsText()
    {
        throw new NotImplementedException(); 
    }
}
```

Je ziet dat de foutmelding i.v.m. het niet uitgewerkt zijn van de interface nu weg is, maar je code zal wel een fout geven wanneer je ze uitvoert. Zoals je ziet staat er momenteel nog 'throw new NotImplementedException()' bij de property en de functie. Het is de bedoeling dat je de niet geïmplementeerde delen nu eerst zelf nog verder uitwerkt en je deze 'throw new NotImplementedException()' dus vervangt door je eigen code. 

De class `Rectangle` zou er uiteindelijk zo kunnen uitzien:

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

    public string AsText()
    {
        return "This is a rectangle with an area of " + Area();
    }
}
```

Om de voordelen van interfaces uit te leggen, implementeren we deze interface nu ook voor de `Circle` class:

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

    public string AsText()
    {
        return "This is a circle with an area of " + Area();
    }
}
```

Ook `Circle` heeft nu een functie `Area()` en een property `Perimeter`. 

Opmerking: Buiten de zaken die in de interface zitten heeft Circle ook een eigen constructor en een property `Radius`. De class Rectangle heeft nog de extra properties width en height en ook een eigen constructor. Een interface is tevreden wanneer je de gevraagde functies uit de interface implementeert. Wat er verder nog in de class staat, dat maakt voor de interface niet uit. Extra properties, een constructor, extra functies, ... zijn dus mogelijk naast de items die deel uitmaken van de interface.

<div class="header2" markdown = "1">## Objecten maken die interface elementen bevatten
</div>

We kunnen deze classes nu gebruiken door er objecten van te maken. Dat gaat hetzelfde dan bij een gewone class die geen interface elementen bevat.

```csharp
Circle c = new Circle(3);

Rectangle r = new Rectangle(4, 5);
```

<div class="header2" markdown = "1">## Objecten via de interface aan een List toevoegen
</div>

Maar hoe steek je ze nu in een list? Een list met cirkels kan immers geen rechthoeken bevatten en omgekeerd. Wel, we kunnen nu een list maken met objecten die de interface `ISurface` implementeren. Aangezien zowel `Circle` als `Rectangle` de interface `ISurface` implementeren kan je ze zonder problemen toevoegen aan de `List<ISurface>`. 

Let wel op: alhoewel de list aangeeft elementen van het type `ISurface` op te slaan, kan je van de interface zelf geen object maken. Dit werkt dus niet:

```csharp
Surfaces.Add(new ISurface()); // Dit lukt niet! ISurface is geen class!
```

Op de list kunnen we nu de functionaliteiten die in de interface voorzien zijn toepassen. In onderstaand voorbeeld wordt het volgende uitgevoerd:
- Er wordt een list die ISurface objecten kan bevatten gedeclareerd.
- Er worden twee elementen aan de list toegevoegd: een `Circle` en een `Rectangle`. (Opm. dit mogen er natuurlijk meerdere zijn.)
- De functie `AsText()` wordt op de list toegepast. Bij het doorlopen van de lijst zal telkens nagegaan worden van welk type het object surface is en zal de AsText() functie uit die respectievelijke class uitgevoerd worden.
- De oppervlaktes (area) van alle objecten uit de list worden opgeteld en op het scherm getoond.

Het bovenstaande uitgewerkt in de Main functie van Program.cs ziet er als volgt uit:

```csharp
static void Main(string[] args)
{
    var Surfaces = new List<ISurface>(); //Declaratie van een List van ISurface elementen.

    Surfaces.Add(new Circle(3)); //Een Circle object toevoegen aan de List.
    Surfaces.Add(new Rectangle(4, 5)); //Een Rectangle object toevoegen aan de List.

    foreach(ISurface surface in Surfaces)
    {
        Console.WriteLine(surface.AsText());
    }

    float area = 0;
    foreach (var surface in Surfaces)
    {
        area += surface.Area();
    }
    Console.WriteLine("The total area is: " + area);
        
    Console.ReadLine();
}
```

Het uitvoeren van deze code toont volgend resultaat op het scherm:

```
This is a circle with an area of 28,27433
This is a rectangle with an area of 20
The total area is: 48,27433
```

# Een management class voor een interface

Om op een handige manier met een interface te werken kan je hiervoor een aparte management class voorzien. In deze class voorzie je de nodige functionaliteiten om snel met de list van objecten van het interface type te werken.

Indien we dit toepassen op het voorbeeld van de interface ISurface, dan kan deze class er als volgt uitzien (we geven de class als naam Surfaces):

```csharp
public class Surfaces
{
    // Er wordt een List voorzien voor het bijhouden van interface objecten 
    List<ISurface> list = new List<ISurface>();

    // De functie Add voegt een surface aan list toe.
    // Deze surface kan een Rectangle of een Circle zijn.
    public void Add(ISurface surface)
    {
        list.Add(surface);
    }

    // Als eerste voorbeeld voegen we een functie ShowSurfaces toe die alle 
    // oppervlaktes uit de List toont, samen met hun individuele oppervlakte.
    // We passen hiervoor de functie AsText op elk element van de List toe.
    // Omdat er via een Interface gewerkt werd, zal steeds de juist AsText functie
    // opgeroepen worden (die van Class Circle voor een circle object, die van 
    // Rectangle voor een Rectangle object).
    public void ShowSurfaces()
    {
        foreach(var surface in list)
        {
            Console.WriteLine(surface.AsText());
        }
    }

    // Als tweede voorbeeld voegen we een functie TotalArea() toe die de totale
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

Deze management class kan nu in de Main functie gebruikt worden. Dit vereenvoudigt de code die in Main staat en maakt het geheel leesbaarder.

De Main functie uit het vorige punt kunnen we nu als volgt herschrijven door gebruik te maken van de management class van de interface, merk op hoe de management class voor vereenvoudiging en betere leesbaarheid van deze Main functie zorgt. Zo moet je nu niet telkens zelf een foreach voorzien om alle elementen van de list te doorlopen, je kan gewoon de functie uit de management class toepassen waarin deze foreach reeds geïmplementeerd is.

```csharp
class Program
{
    static void Main(string[] args)
    {
        Surfaces surface = new Surfaces();

        surface.Add(new Circle(3)); //Een Circle object toevoegen aan de List.
        surface.Add(new Rectangle(4, 5)); //Een Rectangle object toevoegen aan de List.

        surface.ShowSurfaces();

        Console.WriteLine("The total area is: " + surface.TotalArea());
        
        Console.ReadLine();
    }
}
```

<div class="header2" markdown = "1">## Gebruik 'Interface as Class'
</div>

### Wat kan er niet?

Wat niet kan, is properties of functies van de class gebruiken die niet tot de interface behoren. Zo heeft de class `Circle` ook een property `Radius`. Toch kan je die niet gebruiken, want die behoort niet tot de interface.

```csharp
public float TotalRadius() {
    float radius = 0;
    foreach(var circle in list) {   // Ook al vermelden we hier circle bij var,
                                    // circle is gewoon een variabelenaam en de rectangles
                                    // zullen nog steeds mee doorlopen worden.
                                    // Door deze naamgeving filteren we dus NIET de circle
                                    // objecten uit de lijst.
        radius += circle.Radius;    // Dit zal niet werken! De rectangle elementen
                                    //bevatten immers geen property Radius.
    }
    return radius;
}
```

### Hoe los je dit op?

Toch is het soms handig als je ook de andere functies van een object kan gebruiken (die niet in de interface zitten), zelfs al _zie_ je enkel de interface. Hier ga je best niet mee overdrijven, maar als het aantal classes dat in je list zit, beperkt is, dan zou je bijvoorbeeld de volgende functie kunnen toevoegen aan de `Surfaces` management class hierboven.
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

        if(element != null) // Enkel indien element niet null is, tellen we de Radius bij 
                            //het totaal op.
        {                   // Element is niet null indien element een Circle is 
                            //(zie uitleg hierboven).
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

Aan de Main functie kunnen we nu volgende lijn toevoegen:

```csharp
 Console.WriteLine("The total of radiuses of the circle objects is: " + surface.TotalRadius());
 ```

 In de uitvoer komt er nu de laatste lijn bij:

```
This is a circle with an area of 28,27433
This is a rectangle with an area of 20
The total area is: 48,27433
The total of radiuses of the circle objects is: 3
```

<div class="header2" markdown = "1">## Interfaces Combineren
</div>

Je hoeft je ook niet te beperken tot een enkele interface. Hieronder voegen we een extra interface toe, die toelaat informatie over het object op het scherm te tonen.

```csharp
public interface IPrintable
{
    void Print();
}
```

Nu maken we een nieuwe class `Triangle` die beide interfaces implementeert (voor `Rectangle` en `Circle` implementeren we de interface in dit voorbeeld niet):

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

Je kan nu de `Surfaces` class uitbreiden met deze functie, die test of het object uit de list de IPrintable interface bevat. Indien dit niet het geval is, wordt element op null gezet zodat de Print-functie niet toegepast wordt op objecten van het type `Circle` en `Rectangle`.

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

<div class="toTop"><a href="#top">Omhoog</a></div>
