---
title: Enumeraties
---
<div class="header1" id="top" markdown = "1"># Enumeraties
</div>

<div class="header2" markdown = "1">## Wat is een enumeratie?
</div>
Een enumeratie is een opsomming. In een aantal programmeertalen kan je een enumeratie als datatype gebruiken. Variabelen van dit datatype kunnen dan slechts de waarden aannemen die in de enumeratie opgegeven zijn.

Voorbeeld:

In onderstaand voorbeeld zie je een enumeratie met de naam Color die een aantal kleuren bevat. Vaak zullen de enumeraties die in een project gebruikt worden in een aparte codefile binnen het project geplaatst worden.

```csharp
public enum Color
{
    green,
    blue,
    red,
    yellow,
    orange,
    pink
}
```

Eens de enumeratie binnen het project bestaat kunnen we ze als datatype bij variabelen gebruiken, zoals in onderstaande Main-functie gebeurt. Een variable met de naam c1 krijgt als datatype `Color`. Merk op hoe de initialisatie van deze variabele gebeurt: een waarde uit de enumeratie wordt aangesproken door gebruik te maken van de naam van de enumeratie d.m.v. een punt gekoppeld aan een waarde van de enumeratie. In onderstaand voorbeeld wordt c1 dus geïnitialiseerd op de waarde green.

```csharp
static void Main(string[] args)
{
    Color c1 = Color.green; // Let op de syntax van initialisatie:
                            // naamEnumeratie.waardeUitEnumeratie

            
    Console.WriteLine("The first color is {0}.", c1);
}
```

Let op! Als we een enumeratie als datatype voor een variabele gebruiken, dan kan deze variabele enkel nog waarden uit de enumeratie krijgen. Het volgende kan dus niet meer:

```csharp
static void Main(string[] args)
{
    Color c1 = Color.green; 
    Color c2 = "cyan";      // FOUT! Een variabele met 
                            // een enumeratie als type
                            // kan enkel waarden uit de
                            // enumeratie krijgen.

    Console.WriteLine("The first color is {0}.", c1);
    Console.WriteLine("The second color is {0}.", c2);

        }
```

<div class="header2" markdown = "1">## Waarom zouden we enumeraties gebruiken?
</div>
Om het nut van enumeraties aan te tonen, volgen hieronder enkele voorbeelden van problemen die zich kunnen voordoen en hoe ze opgelost worden door het gebruik van een enumeratie.

**<u>Voorbeeld 1</u>**

In het onderstaande voorbeeld staat een class `Day` waarmee je een dag in een maand kan onthouden, samen met welke dag in de week dat is. (bv. de 21ste dag van de maand en de 4de dag van de week)

We vinden in deze class volgende zaken terug:
* Properties:
    - DayInWeek: deze property houdt bij de hoeveelste dag van de week het is. Hierbij wordt de afspraak gemaakt dat maandag de waarde 0 krijgt, dinsdag de waarde 1, enz.
    - DayInMonth: deze property houdt bij over de hoeveelste dag in de maand het gaat.

* Utility:
    - IsWeekend: deze utility geeft true als het object een dag in het weekend bevat, m.a.w. als het om een zaterdag of zondag gaat. We kunnen dit testen a.h.v. de property DayInWeek. Omdat we de afspraak hadden dat maandag de waarde 0 krijgt, zal zaterdag dus 5 zijn en zondag 6. We initialiseren de utility IsWeekend dus op dayInWeek >=5.

* Een constructor die een Day-object op de meegegeven argumenten initialiseert.

* Functie:
    - WeekdayToString(): aan de hand van de property DayInWeek wordt door de functie WeekdayToString() de numerieke waarde DayInWeek omgezet naar de bijhordende dag in stringformaat. Deze kan dan achteraf op het scherm getoond worden. 
    Voorbeeld:
        Als DayInWeek de waarde 2 heeft, dan zal de functie WeekdayToString() het woord "woensdag" als resultaat returnen.

```csharp
public class Day {

    public int DayInWeek { get; private set;}
    public int DayInMonth { get; private set; }

    //De utility IsWeekend test of de dag in het weekend valt.
    public bool IsWeekend { get => dayInWeek >= 5; }
    
    //Constructor
    public Day(int inMonth, int inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }
   
    //De functie WeekDayToString() zet de integer dayInWeek om naar de bijhorende
    //dag in stringformaat.
    public string WeekdayToString() {
        if(dayInWeek == 0) return "Monday";
        if(dayInWeek == 1) return "Tuesday";
        //... en zo verder tot Sunday.
    }
} 

public void Main() {
    var day1 = new Day(21, 0); // maandag de 21ste
    var day2 = new Day(5, 6); // zondag de 5de
    var day3 = new Day(13, 4); // vrijdag de 13de
}
```

 **Wat is het probleem met deze manier van werken?**

 Deze werkwijze lijkt logisch, maar het kan snel fout lopen. Je gaat er bij deze werkwijze van uit dat iedereen zich aan de afspraak houdt en als eerste dag maandag zal kiezen en dan een 0 ingeeft voor DayInWeek. Je kan je daar makkelijk in vergissen, en bijvoorbeeld 1 ingeven voor maandag omdat je even vergeet dat programmeurs vanaf 0 beginnen tellen. Of je kan de week misschien op zondag laten beginnen i.p.v. op maandag en dan zal je 0 ingeven voor zondag. Of misschien is er iemand gewoon niet op de hoogte van de afspraak en is het bijgevolg niet gekend dat maandag de waarde 0 moet krijgen. **Het is dus duidelijk dat deze werkwijze snel tot foutieve ingave kan leiden en dat dit dus geen goede oplossing is.**

**<u>Voorbeeld 2</u>**

In voorbeeld 1 zagen we reeds dat er mogelijke foute waarden ingegeven kunnen worden omdat mensen niet zo goed zijn met cijfers en dus vroeg of laat een fout maken. Met woorden zien we veel duidelijker wat de bedoeling is. Een mogelijke oplossing voor het probleem van voorbeeld 1 ligt dus voor de hand: gebruik een string in plaats van een nummer voor de property DayInWeek. 

In onderstaand voorbeeld is dit toegepast. Omdat DayInWeek nu een string-variabele is, zal ook de utility IsWeekend anders geïnitialiseerd moeten worden. Je kan deze werkwijze terugvinden in de commentaarlijnen bij de utility zelf.

```csharp
public class Day {

    public string DayInWeek { get; private set;}  //Nu een string in plaats van een integer.
    public int DayInMonth { get; private set; }

    //De utility IsWeekend test of de dag in het weekend valt. Hierbij wordt gebruik gemaakt van 
    //de functie Equals die nagaat of een string-variabele gelijk is aan de waarde tussen 
    //de haakjes. Er wordt bij het initialiseren van IsWeekend dus getest of dayInWeek gelijk is
    //aan "Saturday" of aan "Sunday".
    public bool IsWeekend { get => dayInWeek.Equals("Saturday") || dayInWeek.Equals("Sunday"); }

    //Constructor
    public Day(int inMonth, string inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }
}
```

De functie `WeekdayToString` wordt nu zelfs overbodig, want de naam van de dag is nu beschikbaar via de string DayInWeek. 

Zoals je in het voorbeeld kan zien, bepalen we of een dag in het weekend valt door de string-variabele te vergelijken met de namen van de dagen in het weekend. **En daar zit een nieuw probleem.** 
* Enerzijds kan een computer veel sneller met nummers werken dan met strings. Hij zal dus sneller kunnen controleren of een getal groter dan of gelijk is aan 5 dan dat hij namen (strings) met elkaar kan vergelijken. Dit voorbeeld werkt dus trager dan het eerste voorbeeld waar we enkel met integers werkten.
* Daarnaast is er ook een kans dat we typfouten maken bij de invoer van de namen van de dagen. Of we schrijven bijvoorbeeld `saturday`, zonder hoofdletter. Aangezien de functie Equals in het voorbeeld hoofdlettergevoelig werkt, zal `saturday` dus niet aanzien worden als een dag in het weekend. Fout, dus!


<div class="header2" markdown = "1">## De oplossing: een enumeratie
</div>

Problemen, zoals beschreven in bovenstaande voorbeelden, kunnen we vermijden door gebruik te maken van een __enumeratie__.

Afzonderlijk van de `class Day` declareren we een `enum WeekDay`. Die bevat een oplijsting van alle dagen in de week. **De computer ziet deze lijst als een lijst van nummers, waarin `Monday` eigenlijk gelijk staat aan 0, `Tuesday` aan 1, enzovoort**. We moeten dit nu zelf niet onthouden.

Deze enumeratie ziet er als volgt uit:

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
```
We kunnen deze enumeratie nu als datatype gebruiken. In de class Day gebruiken we de enumeratie als datatype voor de property DayInWeek.

Ook voor de utility IsWeekend heeft het gebruik van de enumeratie gevolgen, zoals je in de commentaar bij de utility kan lezen.

```csharp

public class Day {

    public Weekday DayInWeek { get; private set;}  //We gebruiken hier de naam van de 
                                                   //enumeratie als gegevenstype.
    public int DayInMonth { get; private set; }


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
    // de weekdagen (maandag tot en met vrijdag) allemaal een waarde kleiner dan 4 
    // (Monday = 0, enz.). 
    // Er wordt dus getest dat de dag na vrijdag in de enumeratie 
    // staat. En, ook al gebruiken we woorden
    // in de enumeratie, de computer zal met nummers werken -> sneller!
    public bool IsWeekend { get => dayInWeek > WeekDay.Friday; }
}
```

We kunnen de enum op de volgende manier gebruiken bij het meegeven van de argumenten voor de constructor.

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // maandag de 21ste
    var day2 = new Day( 5, Weekday.Sunday); // zondag de 5de
    var day3 = new Day(13, Weekday.Friday); // vrijdag de 13de
}
```

Niet alleen kunnen we ons nu niet van nummer van de de dag vergissen (zoals in voorbeeld 1), spellingsfouten worden dadelijk opgemerkt door de compiler. Bovendien zal Visual Studio ons na het typen van `Weekday.` dadelijk tonen wat de mogelijke opties uit de enumeratie zijn (de verschillende dagen, dus). En de computer zelf zal nummers gebruiken voor deze dagen. Vandaar dat we in de utility `IsWeekend` de dag van de week met vrijdag kunnen vergelijken, zoals je in de commentaar kan terugvinden.

**Het is dus duidelijk dat de enumeratie hier een groot aantal voordelen heeft.**

En er is nog een voordeel: elke enum bevat automatisch een functie `ToString()` die de tekstuele representatie van de waarde geeft. De dag van de week als string tonen gaat dus vanzelf:

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // maandag de 21ste
    
    // Mogelijkheid 1: 
    // gebruik van de ToString() functie die automatisch voorzien is bij de enumeratie.
    string result = day1.DayInWeek.ToString();

    // Mogelijkheid 2: 
    // console.WriteLine maakt deze conversie naar string zelfs automatisch, zonder
    // dat de ToString() functie toegepast wordt op DayInWeek.
    Console.WriteLine("Day " + day1.DayInMonth + " is a " + day1.DayInWeek);
}
```

<div class="header2" markdown = "1">## Enums doorlopen d.m.v. een for-lus
</div>

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

Opmerking: Een enum kan eveneens doorlopen worden met een `foreach`-lus, maar aangezien deze syntax minder eenvoudig is, beperken we ons in deze cursus tot de for-lus.

<div class="note oefening">
    <p>Maak de oefeningenreeks Enumeraties die je op Smartschool vindt.</p>
</div>

<div class="header2" markdown = "1">## Een random Enum waarde
</div>

Soms wil je een willekeurige enum waarde toekennen aan een variabele. Hiervoor kan je gebruik maken van de random number generator. Je gebruikt deze als volgt:
- Je start de generator ergens in je code met de instructie `var generator = new Random();`
- Daarna kan je een random nummer genereren d.m.v. de instructie `var value = generator.Next(100);`
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
In bovenstaand voorbeeld plaatsen we de random waarde die we genereren in de variabele value, waar we als type `var` meegeven. Soms zal het echter nodig zijn om de random enum waarde in een reeds gedeclareerde waarde van een bepaald type te plaatsen. In dat geval moet er opnieuw een conversie gebeuren naar het juiste type. (Zie onderstaand voorbeeld)

In het onderstaande voorbeeld worden objecten van de class `Circle` gemaakt. Elk object heeft een straal en een kleur. De kleur wordt via een random waarde uit de enum Color gekozen.

We voorzien in dit voorbeeld 3 bestanden:
- Enum.cs met de enum met kleuren.
- Circle.cs met de beschrijving van de class Circle.
- Program.cs met daarin de Main-functie die door Visual Studio voor elk project automatisch voorzien wordt. In deze Main-functie maken we de Circle-objecten en tonen we ze op het scherm.

Belangrijke opmerking i.v.m. het starten van de `Random` generator: het is belangrijk om dit slechts éénmalig in je programma te voorzien. De `Random` generator werkt intern als volgt: bij het opstarten bepaalt hij een lijst van random waarden a.h.v. een `seed`. Standaard is deze `seed` de systeemtijd. 
Eens de `Random` generator gestart is, kunnen we door `Next` op de generator toe te passen telkens de volgende waarde uit de interne lijst opvragen. Zo krijgen we dus random waarden. Indien we echter telkens opnieuw de generator zouden starten op heel korte tijd en dan telkens een random waarde opvragen, dan kan dit als gevolg hebben dat we steeds dezelfde waarde als resultaat krijgen. De generator zal in die korte tijd immers vaak intern steeds dezelfde lijst genereren a.h.v. de seed en uit deze lijst vragen we dan steeds de eerste waarde op. Gevolg: de kans is groot dat we steeds dezelfde waarde krijgen.
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

        public Color Color { get; private set;}
        public int Radius { get; private set; }

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

<div class="header2" markdown = "1">## Opmerking i.v.m. de oefeningen
</div>

In deze oefenreeks gebruiken we nog iets nieuws: Overrides. Je vindt de uitleg hierover in het hoofdstuk Details onder het puntje Override. Lees eerst dit onderdeel van het hoofdstuk Details voordat je de oefeningen maakt.


<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-enum-1" target="_blank">oefening-enum-1</a> en maak de oefeningenreeks</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>
