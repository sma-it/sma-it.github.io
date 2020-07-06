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
}

void Func() {
    var person = new Person();
    person.FirstName = "Barack";
    person.LastName = "Obama";
    Console.WriteLine(
        "Deze persoon heet " 
        + person.FirstName + " " 
        + person.LastName);
}
```
We gebruiken properties een beetje zoals variabelen. Het zijn de publiek toegankelijke variabelen van een class. Maar een gewone variabele zou je intuïtief zo schrijven:

```csharp
public class Person {
    public string FirstName;
    public string LastName;
}
```
Bovenstaand voorbeeld zal zelfs gewoon werken. In andere programmeertalen is dit soms zelfs de gangbare manier van werken. In C# niet. Alhoewel de code niet echt fout is, zal Visual Studio je voorstellen om dat aan te passen. 

<div class="note waarschuwing">
<p>In de oefeningen, taken en testen die je in deze les maakt stellen we niets voor, we rekenen het gewoon als fout aan!</p>
</div>

Deze manier van werken leidt vaak tot fouten. Daarom is het beter direct aan te duiden dat wat je van plan bent met de variabele. En dan zijn er drie opties:

- Je kan er naar schrijven en de waarde uitlezen _(readwrite)_
- Je kan er enkel naar schrijven _(writeonly)_
- Je kan enkel de waarde uitlezen _(readonly)_

De gewenste functionaliteit kunnen we aangeven met een combinatie van `set` en `get`. En op dat moment worden het _properties_.

<div class="header2" markdown = "1">## De Mogelijkheden
</div>
### ReadWrite Properties
Meestal zal je de waarde van een property willen lezen en kunnen aanpassen. Leestoegang geef je met `get`, schrijftoegang geef je met `set`. Er bestaat dan ook een shortcut voor dit soort properties, zoals uitgelegd in het vorige hoofdstuk. Het voorbeeld bovenaan dit hoofdstuk is een voorbeeld met _ReadWrite_ properties.

### WriteOnly properties
_WriteOnly_ properties laten we voorlopig even met rust, want die zal je voorlopig niet veel nodig hebben.

### ReadOnly Properties
Soms is het niet de bedoeling dat je kan schrijven naar een property, maar enkel dat je de waarde kan lezen. Dan gebruik je enkel `get`. Maar dat gaat niet vanzelf. Stel je voor dat je een class hebt die een verbinding met het internet maakt. Je hebt een functie `Connect()`, maar hoe kan je nu op elk moment te weten komen of je nu wel of niet verbonden bent? Door een property te gebruiken!

In het onderstaande voorbeeld zie je hoe dat zou kunnen werken:

```csharp
public class Connection {
    // De property Connected geeft aan of we verbonden zijn of niet 
    // (true=verbonden; false=niet verbonden).
    public bool Connected { get; set; }

    //De property Connected wordt geïnitialiseerd d.m.v. de onderstaande 
    //functie Connect().
    public void Connect() {
        if(TryToConnectToTheInternet() == true) {  //TryToConnectToTheInternet() is 
            Connected = true;                   //een fictieve functie die nagaat 
        } else {                                //of de connectie met het internet lukt.
            Connected = false;                  //De functie geeft true als resultaat indien de 
                                                //connectie lukt.
                                                //Afhankelijk hiervan wordt de property  
                                                //Connected geïnitialiseerd op true of false.
        }
    }
}

public static void Program() {
    var conn = new Connection(); //Er wordt een instantie van de class Connection gemaakt.
    conn.Connect();              //De functie Connect() wordt toegepast op deze instantie.
                                 //De property Connected van het object conn wordt hierdoor 
                                 //geïnitialiseerd.
    if(conn.Connected) {         //Indien de property Connected van het object conn true is, zal 
        // download my file      //de download starten.
    }
}
```
Maar wat als iemand die class verkeerd gebruikt, en het op deze manier probeert?
```csharp
public static void Program() {
    var conn = new Connection();
    conn.Connected = true; // Hoera! We zijn verbonden.
}
```
De property `Connected` had de bedoeling ons te vertellen of we verbonden waren. Maar nu hebben we de waarde zelf op `true` gezet. Zo lijkt het wel of we een verbinding hebben, maar dat is natuurlijk niet zo.

Deze fout kunnen we voorkomen door `set` weg te laten bij de declaratie van de property:

```csharp
public bool Connected { get; }
```

Maar dit schept een nieuw probleem. Als de waarde niet aangepast kan worden, hoe kan class zelf dat dan doen? Deze code zal niet meer werken:

```csharp
if(TryToConnectToTheInternet() == true) {
    Connected = true; // connected is readonly!!!
} else {
    Connected = false; // connected is readonly!!!
}
```

De oplossing bestaat erin een extra variabele te gebruiken. Die mag niet zichtbaar zijn wanneer je de class gebruikt, maar kan intern wel aangepast worden. De `Connected` property zal dan via zijn `get` functie de waarde van die interne variabele doorgeven.

```csharp
public class Connection {
    private bool connected = false; // de interne variabele.
    public bool Connected { get => connected; } //de property Connected haalt zijn waarde uit
                                                //de interne variabele connected.

    public void Connect() {
        if(TryToConnectToTheInternet() == true) {
            connected = true; //de interne variabele wordt geïnitialiseerd.
        } else {
            connected = false;
        }
    }
}

public static void Program() {
    var conn = new Connection();
    conn.Connect();
    if(conn.Connected) {
        // download my file
    }
}
```

Op deze manier werkt de code zoals het hoort. Let zeker hier op:
- De extra variabele `connected` is _private_. Je leert hier later meer over, maar het betekent dat je geen toegang hebt tot deze variabele wanneer je een object maakt van je class.
- We geven die interne variabele `connected` dadelijk een waarde. We starten immers zonder een verbinding.
- De property `Connected` verwijst nu naar de interne variabele wanneer we ze opvragen. De `set` optie laten we gewoon weg.
- We kunnen bijna dezelfde naam gebruiken. Het is de gewoonte dat je in dit geval de interne variabele met een kleine letter schrijft, en de property met een hoofdletter. Dat houdt je code overzichtelijk.
- Binnen de class, bijvoorbeeld in de functie `Connect()` kan je de interne variabele gebruiken.
- In het programma (dit is buiten de class) zelf is enkel de property `Connected` bruikbaar.



<div class="header2" markdown = "1">## Wanneer gebruik je _ReadOnly_?
</div>
Er zijn verschillende scenario's denkbaar.

### Preventie
Soms is het echt niet de bedoeling om een variabele van buitenaf aan te passen. Dat zagen we al in het vorige voorbeeld: door `Connected` te wijzigen wist je niet meer of je nu wel of niet een verbinding had. Het is best mogelijk dat je programma crasht omdat je iets wil downloaden terwijl je eigenlijk geen verbinding hebt.

**Preventie** betekent dat we `set` weglaten om fouten te voorkomen.

### Utility
Je kan ook _readonly_ utilities maken die het gebruik van je class vereenvoudigen. Als voorbeeld terug even de class `Person`:

```csharp
public class Person {
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Name { get => FirstName + " " + LastName; }
}
```

Het kan handig zijn dat je de hele naam in 1 keer kan opvragen, in plaats van zelf altijd de twee namen te moeten samenvoegen tot een string. Maar wat zouden we met een `set` property die de volledige naam bevat in dit geval moeten doen? De naam opsplitsen en verdelen over `FirstName` en `LastName`, zodat we ook deze twee gegevens hebben? Dat gaat vroeg of laat fout, bijvoorbeeld als iemands voornaam uit twee delen bestaat. Het is veel veiliger om het instellen afzonderlijk te doen.

**Utility** betekent dat we een get property toevoegen om iets eenvoudiger te maken. Maar omdat het eigenlijk niet om een afzonderlijke variabele gaat, is een bijhorende `set` niet van toepassing.

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
Het bovenstaande voorbeeld bevat nog een kleine nieuwigheid. Als je get property uit meer dan 1 statement bestaat, dan kan je de eerder gebruikte schrijfwijze met het pijltje niet gebruiken. In zo'n geval werk je je statements uit zoals in een normale functie. En gebruik je return om het resultaat aan te duiden. _(In dit geval hadden we de berekening natuurlijk ook makkelijk in een enkel statement kunnen doen.)_

Wat als je hier een `set` property zou toevoegen? Afgezien van het feit dat je hier geen echte variabele hebt waarin je het oppervlak zou kunnen opslaan, zou dat betekenen dat de breedte en hoogte niet meer kloppen. Dat zou dus een HEEL slecht idee zijn.

**Berekening** betekent dat je een get property gebruikt voor een eenvoudige berekening. Ook hier zou een `set` property aan toevoegen compleet onzinnig zijn, want er is geen variabele verbonden met deze property.

<div class="header2" markdown = "1">## Wanneer gebruik je _geen_ property?
</div>
Met de bovenstaande informatie zou je heel wat functies kunnen omzetten naar properties. Elke niet-void functie zonder argumenten zou een `get` property kunnen worden. En elke void functie met 1 argument zou een `set` functie kunnen zijn. Toch is dat niet de bedoeling. 

### Acties
Het woord _property_ betekent _eigenschap_. In het algemeen kan je stellen dat je van acties nooit een property maakt. Daarom wordt `ConnectToTheInternet` een functie, terwijl `Connected` een property is. Al is er natuurlijk altijd ruimte voor interpretatie. Zo hadden we in de class `Rectangle` hierboven in plaats van de property `Area` ook een functie  `CalculateArea()` kunnen toevoegen. Dat is ook helemaal niet fout, maar gebruik dan ook een duidelijke naam die naar een actie verwijst. Dan is het voor de gebruiker van je functie of property ook duidelijk of er haakjes na de naam verwacht worden of niet.

### Complexe berekeningen
Als je een berekening gebruikt in een property, dan hoort dat een eenvoudige berekening te zijn. Maar wanneer is een berekening te complex? Dat is voor interpretatie vatbaar, maar je kan de volgende regels gebruiken:

- Wanneer een berekening andere variabelen in de class gaat __aanpassen__, dan hoort het geen property te zijn.
- Wanneer een berekening __extra variabelen__ moet declareren, dan is ze te complex. Een enkel primitive type, zoals een int of float, dat kan nog. Maar instanties van classes maken, of een nieuwe array declareren, dat hoort niet thuis in een property.
- Wanneer je in je berekening __andere functies__ van je class oproept, dan maak je beter een functie.

Het meest pragmatische argument op dit vlak is misschien wel de debugger. Wanneer je tijdens het debuggen over een property hovert met je muis, dan krijg je zijn waarde te zien. Maar dat gaat mis wanneer de berekening achter een property te complex is. Dan kan Visual Studio heel traag worden, of kan zelfs je debug sessie in sommige gevallen crashen. Niet doen dus.

<div class="header2" markdown = "1">## Schrijfwijzen
</div>
Je hebt ondertussen wel gemerkt dat je properties op verschillende manieren kan noteren. Een enkele correcte manier bestaat dikwijls niet, als is de meeste eenvoudige notatie wel afhankelijk van de situatie.

### Meest Eenvoudig
```csharp
public int MyProperty { get; set; }
```
Dit gebruik je wanneer een property _readwrite_ is, en er geen extra berekening nodig is.

### Set of Get
```csharp
private int myProperty;
public int MyProperty { get => myProperty; }

private int myOtherProperty;
public int MyOtherProperty { set => myProperty = value; }
```
Deze notatie gebruik je bij _readonly_ of _writeonly_ properties, zonder extra berekeningen.

### 1 statement
```csharp
private int value;
public int PowerOfTwo { get => value * value; }
```
Dit is gelijk aan het vorige voorbeeld, maar het kan dus ook met een berekening.

```csharp
private string name;
public string Name { set => name = value.ToUpper(); }
```
Ook dit is gelijk aan het vorige voorbeeld, maar nu met een eenvoudige functie.

### Meerdere statements
```csharp
public class Square {
    public float Side { get; set; }
    public float Perimeter {
        get {
            var p = Side * 4;
            return p;
        }
        set {
            var s = value / 4;
            Side = s;
        }
    }
}
```
Dit is niet echt de meest logische manier om met een vierkant om te gaan, maar het is een voorbeeld van een _readwrite_ property met meerdere statements.

### Combinaties
```csharp
public class Square {
    public float Side { get; set; }
    public float Perimeter {
        get => Side * 4;
        set {
            var s = value / 4;
            Side = s;
        }
    }
}
```
Je kan ook combinaties maken. `Set` en `Get` moeten niet dezelfde schrijfwijze volgen.

<div class="note oefening">
<p>Open het project <a href="https://github.com/sma-it/oefening-properties-1" target="_blank">oefening-properties-1</a> en maak de oefeningen.</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>