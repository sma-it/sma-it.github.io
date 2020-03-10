---
title: Enumeraties
---
# Enumeraties
## Hoe het niet moet

Om je uit te leggen wat enumeraties zijn, en welke voordelen ze bieden, beginnen we met een voorbeeld dat geen enumeraties gebruikt.

In het onderstaande voorbeeld staat een class `Day` waarmee je een dag in een maand kan onthouden, samen met welke dag in de week dat is. 
De property DayInWeek houdt bij de hoeveelste dag van de week het is. Hierbij wordt de afspraak gemaakt dat maandag de waarde 0 krijgt, dinsdag de waarde 1, enz.
De property DayInMonth houdt bij over de hoeveelste dag in de maand het gaat. 
Aan de hand van de property DayInWeek wordt via de functie WeekdayToString() de numerieke waarde omgezet naar de bijhordende dag in stringformaat. Deze kan dan achteraf op het scherm getoond worden.

```csharp
public class Day {

    private int dayInWeek;
    public int DayInWeek { get => dayInWeek; }

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    // Constructor
    public Day(int inMonth, int inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    // De utility IsWeekend test of de dag in het weekend valt.
    public bool IsWeekend { get => dayInWeek >= 5; }
    
    // De functie WeekDayToString() zet de integer dayInWeek om naar de bijhorende
    // dag in stringformaat.
    public string WeekdayToString() {
        if(dayInWeek == 0) return "Monday";
        if(dayInWeek == 1) return "Tuesday";
        // ... and so on
    }
} 

public void Main() {
    var day1 = new Day(21, 0); // monday the 21st
    var day2 = new Day(5, 6); // sunday the 5th
    var day3 = new Day(13, 4); // friday the 13th
}
```

 Je gaat er bij deze werkwijze van uit dat iedereen zich aan de afspraak houdt en als eerste dag maandag zal kiezen en dan een 0 ingeeft voor DayInWeek. Je kan je daar makkelijk in vergissen, en bijvoorbeeld 1 ingeven voor maandag omdat je even vergeet dat programmeurs vanaf 0 beginnen tellen. Of je kan de week misschien op zondag laten beginnen i.p.v. op maandag en dan zal je 0 ingeven voor zondag. Of misschien is er iemand niet op de hoogte van de afspraak en is het bijgevolg niet gekend dat maandag de waarde 0 moet krijgen.
 Het is dus duidelijk dat deze werkwijze snel tot foutieve ingave kan leiden en dat dit dus geen goede oplossing is.

## Zo moet het ook niet

De reden voor deze mogelijke fouten ligt in het probleem dat mensen niet zo goed zijn met cijfers en dus vroeg of laat een fout maken. Met woorden zien we veel duidelijker wat de bedoeling is. Een mogelijke oplossing voor dit probleem ligt dus voor de hand: gebruik een string in plaats van een nummer voor de property DayInWeek:

```csharp
public class Day {

    private string dayInWeek;
    public string DayInWeek { get => dayInWeek; } //Nu string i.p.v. int.

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    // Constructor
    public Day(int inMonth, string inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    // De utility IsWeekend test of de dag in het weekend valt.
    public bool IsWeekend { get => dayInWeek.Equals("Saturday") || dayInWeek.Equals("Sunday"); }
}
```

De functie `WeekdayToString` wordt zo zelfs overbodig, want de naam van de dag is nu beschikbaar via de string DayInWeek. En om te bepalen of een dag in het weekend valt vergelijken we de string met de namen van de dagen in het weekend. Maar daar zit een nieuw probleem. Niet alleen kan een computer veel sneller met nummers werken en zal hij dus sneller kunnen controleren of een getal kleiner is dan 5 t.o.v. namen met elkaar te vergelijken. Er is ook een kans dat we typfouten maken bij de invoer van de namen van de dagen. Of we schrijven bijvoorbeeld `saturday`, zonder hoofdletter. Aangezien de functie Equals in het voorbeeld hoofdlettergevoelig werkt, zal `saturday` dus niet aanzien worden als een dag in het weekend. Fout, dus!

## Lang Leve de Enum

Ook deze oplossing is dus niet ideaal. En daarom gebruiken we __enumeraties__.

Afzonderlijk van de `class Day` declareren we een `enum WeekDay`. Die bevat een oplijsting van alle dagen in de week. De computer ziet deze lijst als een lijst van nummers, waarin `Monday` eigenlijk gelijk staat aan 0, `Tuesday` aan 1, enzovoort. We moeten dit nu zelf niet onthouden.
De enumeratie en de class Day zien er nu zo uit:

```csharp

// Declaratie van de enumeratie
public enum Weekday {
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday,
};

// De class Day
public class Day {

    private Weekday dayInWeek;
    public Weekday DayInWeek { get => dayInWeek; }

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    // Constructor
    public Day(int inMonth, Weekday inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    // De utility IsWeekend test of de dag in het weekend valt.
    // Aangezien de computer de enumeratie als integers bekijkt, kunnen we gebruik
    // maken van de test dayInWeek >= WeekDay.Friday.
    // De computer ziet het item WeekDay.Friday als 4.
    // Aangezien alle weekdagen voor Friday in de enumeratie opgesomd zijn, hebben
    // ze allemaal een waarde kleiner dan 4 (Monday = 0, enz.). We testen dus nu niet
    // meer of de dag een zaterdag of zondag is, maar we testen dat de dag na vrijdag 
    // in de enumeratie staat.
    public bool IsWeekend { get => dayInWeek > WeekDay.Friday; }
}
```

We kunnen de enum op de volgende manier gebruiken bij het meegeven van de argumenten voor de constructor.

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // monday the 21st
    var day2 = new Day( 5, Weekday.Sunday); // sunday the 5th
    var day3 = new Day(13, Weekday.Friday); // friday the 13th
}
```

Niet alleen kunnen we ons nu niet van dag vergissen, spellingsfouten worden dadelijk opgemerkt door de compiler. Bovendien zal Visual Studio ons na het typen van `Weekday.` dadelijk tonen wat de mogelijke opties uit de enumeratie zijn (de verschillende dagen, dus). En de computer zelf zal nummers gebruiken voor deze dagen. Vandaar dat we in de utility `IsWeekend` de dag van de week met vrijdag kunnen vergelijken, zoals je in de commentaar kan terugvinden.

En er is nog een voordeel: elke enum bevat automatisch een functie `ToString()` die de tekstuele representatie van de waarde geeft. De dag van de week als string tonen gaat dus vanzelf:

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // monday the 21st
    
    // gebruik van de ToString() functie die automatisch voorzien is bij de enumeratie.
    string result = day1.DayInWeek.ToString();

    // console.WriteLine maakt deze conversie naar string zelfs automatisch, zonder
    // dat de ToString() functie toegepast wordt op DayInWeek.
    Console.WriteLine("Day " + day1.DayInMonth + " is a " + day1.DayInWeek);
}
```

## In the Loop

Je kan enums ook eenvoudig in een loop gebruiken. Uiteindelijk is een enum niet meer dan een reeks getallen met een naam. De loop variabele kan dus ook een enum zijn. 
Wat niet zo eenvoudig is, is het bepalen van de grootste waarde. Dat kan je oplossen door die expliciet in je enum te declareren.

In het onderstaande voorbeeld gebruiken we hiervoor de waarde End. Het is op die manier duidelijk welke waarde we als bovengrens voor de `for` moeten gebruiken.:

```csharp
// Declaratie enumeratie
enum Values { one, two, three, End }

// Doorlopen van de enum d.m.v. for
for (Values i = 0; i < Values.End; i++) {
  Console.WriteLine(i);
}
```

## Een random Enum waarde

Soms wil je een willekeurige enum waarde toekennen aan een variabele. Hiervoor kan je gebruik maken van de random number generator. Je gebruikt deze als volgt:
- Je start de generator ergens in je code met de instructie `var generator = new Random();`
- Daarna kan je een random nummer genereren d.m.v. de instructie `var value = random.Next(100);`
De 100 is de bovengrens die je meegeeft, het nummer dat zal gegenereerd worden ligt in dit voorbeeld tussen 0 en 100.

Je zou dus het onderstaande kunnen proberen om een random Enum waarde te verkrijgen:

```csharp
var generator = new Random(); //Initialisatie random number generator 
                              
var value = generator.Next(Values.End); // <-- Compiler geeft een fout bij het genereren
                                     //van de random waarde.
```

Ook al is een enum eigenlijk een getal, de functie Next wil echt een integer zien. Dit los je op door
de enum hier te converteren naar een integer:

```csharp
var generator = new Random();
var value = generator.Next((int)Values.End); // <-- Compiler geeft GEEN fout
```
In bovenstaand voorbeeld plaatsen we de random waarde die we genereren in value, waar we als type `var` meegeven. Soms zal het echter nodig zijn om de random enum waarde in een reeds gedeclareerde waarde van een bepaald type te plaatsen. In dat geval moet er opnieuw een conversie gebeuren naar het juiste type. (Zie onderstaand voorbeeld)

In het onderstaande voorbeeld worden objecten van de class `Circle` gemaakt. Elk object heeft een straal en een kleur. De kleur wordt via een random waarde uit de enum Color gekozen.

We voorzien in dit voorbeeld 3 bestanden:
- Enum.cs met de enum met kleuren.
- Circle.cs met de beschrijving van de class Circle.
- Program.cs met daarin de Main-functie die door Visual Studio voor elk project automatisch voorzien wordt. In deze Main-functie maken we de Circle-objecten en tonen we ze op het scherm.

Belangrijke opmerking i.v.m. het starten van de `Random` generator: het is belangrijk om dit slechts éénmalig in je programma te voorzien. De `Random` generator werkt intern als volgt: bij het opstarten bepaalt hij een lijst van random waarden a.h.v. een `seed`. Standaard is deze `seed` de systeemtijd. Eens de `Random` generator gestart is, kunnen we door `Next` op de generator toe te passen telkens de volgende waarde uit de interne lijst opvragen. Zo krijgen we dus random waarden. Indien we echter telkens opnieuw de generator zouden starten op heel korte tijd en dan telkens een random waarde opvragen, dan kan dit als gevolg hebben dat we steeds dezelfde waarde als resultaat krijgen. De generator zal in die korte tijd immers vaak intern steeds dezelfde lijst genereren a.h.v. de seed en uit deze lijst vragen we dan steeds de eerste waarde op. Gevolg: de kans is groot dat we steeds dezelfde waarde krijgen.
Door de `Random` generator slechts eenmalig op te starten, vermijden we dit probleem en wordt via `Next` de lijst met random waarden steeds verder afgegaan. Gevolg: we krijgen nu wel verschillende resultaten.

Enum.cs

```csharp
public enum Color
{
    Red,
    Green,
    Blue,
    Orange,
    Yellow,
    Purple,
    Lime,
    End
};
```

Circle.cs

```csharp
public class Circle
    {

        private Color color;
        public Color Color { get => color; }

        private int radius;
        public int Radius { get => radius; }

        // Constructor: het argument color wordt in 
        // de Main-functie a.h.v. Random geïnitialiseerd
        // op een random waarde uit de enum Color.
        public Circle(int radius, Color color)
        {
            this.radius = radius;
            this.color = color;
        }

        public override string ToString()
        {
            return "The circle has a radius of " + radius + " and its color is " + color + ".";
        }
    }
```

Program.cs
```csharp
class Program
    {
        static void Main(string[] args)
        {
            // Eenmalig starten van de Random generator.
            var generator = new Random();

            // Declaratie variabele voor opslaan Random color.
            Color color;

            // Circle c1 wordt gemaakt.
            // Eerst krijgt de variabele color een waarde via
            // de Random generator.
            // De variabele wordt dan gebruikt als argument voor
            // de constructor.
            color = (Color)generator.Next((int)Color.End);
            Circle c1=new Circle(1,color);

            // Circle c2 wordt gemaakt.
            // De variabele color krijgt eerst een andere random
            // waarde.
            color = (Color)generator.Next((int)Color.End);
            Circle c2 = new Circle(3, color);

            // Circle c3 wordt gemaakt.
            // De variabele color krijgt eerst een andere random
            // waarde.
            color = (Color)generator.Next((int)Color.End);
            Circle c3 = new Circle(8, color);

            // Uitvoer van de drie Circle objecten.
            Console.WriteLine(c1);
            Console.WriteLine(c2);
            Console.WriteLine(c3);
            Console.ReadKey();
        }
    }
```

## Oefeningen

In deze oefenreeks gebruiken we nog iets nieuws: Overrides.

Elke class die je maakt is afgeleid van een andere class: `Object`. Deze class heeft onder meer de functie `ToString()`. Daardoor kan je
elke class die je maakt rechtstreeks gebruiken met `Console.WriteLine()`. Het resultaat van `Console.WriteLine()` is de __naam van de class__. Bijvoorbeeld zo:

```csharp
class BankAccount {
    public string Name { get; set; }
    public int Balance { get; set; }
}

var account = new BankAccount();
Console.WriteLine("Dit is een " + account);
```
Het resultaat van Console.WriteLine is in dit geval:

```csharp
Dit is een BankAccount.
```

Je kan die functie ook _overschrijven_. Je zegt dan aan de compiler __"Wanneer iemand om de functie `ToString()` vraagt, gebruik dan deze versie in plaats van de standaard versie"__. Je doet dat door de functie te voorzien van het keyword `override`. De functienaam, argumenten en resultaat moeten wel gelijk zijn aan de oorspronkelijke functie. Maar de compiler helpt je daarbij. Wanneer je override typt in een class, dan zal de compiler je de functies tonen die je kan overschrijven. Je selecteert dan de functie die je wil overschrijven.
In het voorbeeld hieronder maken we een `override` voor de functie `ToString()` __zodat niet de naam van de class gegeven wordt, maar de properties getoond worden.__

```csharp
class BankAccount {
    public string Name { get; set; }
    public int Balance { get; set; }

    // Override voor de ToSTring() functie
    public override string ToString() {
        return "Account " + Name + " has a balance of " + Balance + "Euro";
    }
}

var account = new BankAccount();
account.Name = "one";
account.Balance = 1000;
Console.WriteLine(account);
```
Het resultaat is nu:
```csharp
Account one has a balance of 1000 Euro
```

<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-enum-1" target="_blank">oefening-enum-1</a> en maak de oefeningenreeks</p>
</div>
