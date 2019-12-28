---
title: Constructors
---

# Constructors

Wanneer je een object maakt van een class, dan wil je meestal zeker zijn van de waarden waar je mee werkt. In het volgende voorbeeld is dat niet zo duidelijk.

De class RangedNumber uit het voorbeeld bevat een public integer Number die d.m.v. de functie `set` binnen de grenzen minimum en maximum gehouden wordt. Deze grenzen worden in de class voorzien d.m.v. twee private integer variabelen minimum en maximum.
De class levert dus een object af met een property Number die binnen bepaalde grenzen blijft.

```csharp
public class RangedNumber {
    private int minimum;
    private int maximum;

    private int number;
    public int Number {
        get => number;
        set {
            if (value > maximum) number = maximum;
            else if (value < minimum) number = minimum;
            else number = value;
        }
    }
}
```

Wat zijn de waarden van `minimum` en `maximum`? Wel, de default waarde van een `int` is altijd 0. Voor het minimum is dat geen probleem, maar dat het maximum ook nul is, dat is minder geslaagd aangezien de property Number dan steeds 0 zal zijn. 
Gelukkig kunnen we de waarden aanpassen:

```csharp
public class RangedNumber {
    private int minimum = 0;
    private int maximum = 100;

    private int number;
    public int Number {
        get => number;
        set {
            if (value > maximum) number = maximum;
            else if (value < minimum) number = minimum;
            else number = value;
        }
    }
}
```

Toch is deze class nog ver van ideaal. We kunnen de class nu enkel gebruiken met de range 0-100. Het zou beter zijn dat de range instelbaar is. Dat kan door van `minimum` en `maximum` properties te maken. Maar dat zou betekenen dat de range op elk moment aanpasbaar is. Dat is misschien geen goed idee, want iedereen maakt fouten:

```csharp
public class RangedNumber {
    public int Minimum;   // Minimum en Maximum zijn nu properties.
    public int Maximum;

    private int number;
    public int Number {
        get => number;
        set {
            if (value > Maximum) number = Maximum;
            else if (value < Minimum) number = Minimum;
            else number = value;
        }
    }
}

// Ergens in het programma wordt de waarde voor de properties Minimum en Maximum ingesteld
var Ranged10_20 = new RangedNumber();
Ranged10_20.Minimum = 10;
Ranged10_20.Maximum = 20;

// Ergens anders in het programma
Ranged10_20.Maximum = 100; // Ik lette niet op en wilde Number aanpassen
                           // -> Maximum is per ongeluk gewijzigd.
```

Na lang zoeken zal je de fout wel vinden, maar zou het niet veel beter zijn als het niet mogelijk was om deze fout te maken? En wat als je zou vergeten om de range in te stellen? Dan zijn minimum en maximum beiden nul, een situatie die we willen voorkomen.

## Wat is een constructor?
Een constructor is een speciale functie die enkel uitgevoerd wordt op het moment dat je een object van je class maakt. Deze functie heeft __de naam van de class__ en heeft __geen resultaat__. Het aantal argumenten kan je wel zelf kiezen. Bovendien moet de constructor __public__ zijn. De class `RangedNumber` zou wel een constructor kunnen gebruiken:

```csharp
public class RangedNumber {
    // We werken terug met private variabelen voor minimum en maximum i.p.v. properties
    private int minimum;
    private int maximum;

    // De constructor
    public RangedNumber(int minimum, int maximum) {
        this.minimum = minimum; //Merk op: gebruik van this bij identieke namen voor
        this.maximum = maximum; //argumenten en variabelen.
    }

    private int number;
    public int Number {
        get => number;
        set {
            if (value > maximum) number = maximum;
            else if (value < minimum) number = minimum;
            else number = value;
        }
    }
}
```

Nu kan je zo een object maken:

```csharp
var Ranged10_20 = new RangedNumber(10, 20);
```
De range van het object is achteraf niet meer aanpasbaar. Dat voorkomt in dit geval fouten. Bovendien vraagt het minder typewerk en kan je niet vergeten de range te initialiseren. 

Omdat er in het voorbeeld dezelfde namen gebruikt zijn voor de argumenten als voor de private variabelen van de class, is het noodzakelijk om d.m.v. het keyword `this` onderscheid te maken tussen beide. Als er voor een naam `this` geplaatst wordt, gekoppeld door een punt, dan wordt er op die manier aangeduid dat dit de variabele van de class is. Op die manier is het voor de constructor duidelijk dat de class-variabele moet geïnitialiseerd worden op het argument (en niet omgekeerd).

Dat is dadelijk de belangrijkste reden voor het gebruik van constructors: je voorkomt dat er achteraf fouten gemaakt worden. In dit geval zijn er slechts twee variabelen die je moet instellen, maar wat als dat er meer worden? De kans dat je een property over het hoofd ziet wordt dan steeds groter.

## Default Constructors
Door de compiler te laten weten dat we twee integers als argument verwachten bij het declareren van een object, is het niet meer mogelijk om dit object zonder argumenten te maken. Dit werkt niet meer:

```csharp
var Ranged10_20 = new RangedNumber();
```

Nu je weet wat een constructor is, is het eigenlijk vooral vreemd dat de eerste versie van deze class _wel_ werkte. Het is nu duidelijk dat we `RangedNumber(10, 20)` kunnen gebruiken omdat we een constructor schreven met precies die naam en argumenten. Maar we hebben nooit de constructor in de vorm `RangedNumber()` geschreven die bij de eerste versie gebruikt wordt om een object te maken.

Dit is de reden: wanneer de compiler je code compileert, en je schreef geen constructor, dan voegt de compiler er zelf een toe. Dit noemen we de _default constructor_. Deze constructor heeft geen argumenten doet niets bijzonders, maar is nodig om een object te kunnen maken van een class.

Waarom doet de compiler dit? Om het jou gemakkelijk te maken. De code voor een default constructor zou er zo uit zien:

```csharp
public NameOfClass() {}
```

Dat kan de compiler dus perfect zelf verzinnen. En het bespaart je wat typewerk wanneer je geen andere constructor nodig hebt. Maar op het moment dat je zelf een constructor toevoegt, zoals in de class  `RangedNumber` hierboven, dan kan de compiler niet meer weten of je ook een object wil kunnen maken zonder die argumenten. Dus voegt de compiler geen default constructor meer toe.

Als je toch een default constructor wil, dan moet je die dus zelf toevoegen. Bijvoorbeeld zo:

```csharp
public class RangedNumber {
    private int minimum;
    private int maximum;

    // Default constructor
    public RangedNumber() {
        this.minimum = 0;
        this.maximum = 10;
    }

    // Specific constructor met argumenten
    public RangedNumber(int minimum, int maximum) {
        this.minimum = minimum;
        this.maximum = maximum;
    }

    private int number;
    public int Number {
        get => number;
        set {
            if (value > maximum) number = maximum;
            else if (value < minimum) number = minimum;
            else number = value;
        }
    }
}
```

Op die manier kan je beide constructors gebruiken:

```csharp
var n1 = new RangedNumber(); // default constructor
var n2 = new RangedNumber(3, 30); // specific constructor
```

Je kan trouwens ook meerdere eigen constructors schrijven:

```csharp
// specific constructor met enkel voor maximum een argument
public RangedNumber(int maximum) {
    this.minimum = 0;
    this.maximum = maximum;
}

// of:
// constructor met optionele argumenten (er zijn default waarden voorzien)
public RangedNumber(int maximum = 100, int minimum = 0) {
    this.minimum = minimum;
    this.maximum = maximum;
}
```

Merk op dat bij de constructor met optionele argumenten het maximum voor het minimum staat in de argumentenlijst. Bij deze constructor is het immers niet noodzakelijk om twee waarden mee te geven vanwege de default argumenten. Aangezien het onlogisch is om enkel het minimum in te willen stellen (het maximum blijft dan 0), zal het bij het oproepen van de constructor met één argument de bedoeling zijn om deze waarde in het maximum te plaatsen. Omdat de meegegeven waarden in volgorde ingevuld worden in de argumentenlijst, is het dus noodzakelijk om het maximum eerst te plaatsen. Bij het oproepen van de constructor met één waarde, wordt deze waarde in maximum geplaatst, het minimum krijgt dan de voorziene default waarde 0.
Bij die laatste versie moet je wel uitkijken. In het hoofdstuk functies heb je geleerd wat optionele argumenten zijn. In dit geval zijn alle argumenten optioneel, dus de functie is ook bruikbaar als default constructor. Je kan dus niet ook nog eens een lege constructor toevoegen. Met deze laatste constructor zou je een object kunnen declareren op verschillende manieren:

```csharp
var n1 = new RangedNumber(); // 0 - 100
var n2 = new RangedNumber(60); // 0 - 60
var n3 = new RangedNumber(20, 10); // 10 - 20, maar niet handig omdat het maximum eerst moet
var n4 = new RangedNumber(minimum: 10, maximum: 20); // beter leesbaar vanwege named parameters
```

## Voorbeeld: Person
Hier een voorbeeld met een andere class: Person. Deze class bevat onder meer de naam en de voornaam van een persoon. Daarnaast zijn er nog andere eigenschappen, maar we willen nu zeker zijn dat de persoon zeker een naam heeft. Dat kunnen we doen via een constructor:

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

Ook hier zie je voordelen van een constructor in actie. Je kan onmogelijk vergeten om de persoon een naam te geven. Ook kan je zijn naam achteraf niet meer wijzigen. _(Dat laatste zou waarschijnlijk geen goed idee zijn in een echt programma. Wat als iemand een typefout maakte bij de registratie?)_

Ook is het duidelijk dat een default constructor in dit geval geen goed idee is. Welke naam zou je kiezen? Wat je ook als default kiest, het is ongetwijfeld niet de juiste naam.

<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-constructors-1" target="_blank">oefening-constructors-1</a> en maak de oefeningenreeks</p>
</div>