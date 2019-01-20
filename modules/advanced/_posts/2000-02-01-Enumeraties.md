---
title: Enumeraties
---
# Enumeraties
## Hoe het niet moet

Om je uit te leggen wat enumeraties zijn, en welke voordelen ze bieden, beginnen we met een voorbeeld dat geen enumeraties gebruikt.

```csharp
public class Day {

    private int dayInWeek;
    public int DayInWeek { get => dayInWeek; }

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    public Day(int inMonth, int inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    public bool IsWeekend { get => dayInWeek < 5; }
    
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

In het bovenstaande voorbeeld staat een class `Day` waarmee je een dag in een maand kan onthouden, samen met welke dag in de week dat is. Maar je gaat er van uit dat iedereen als eerste dag maandag zal kiezen en dan een 0 ingeeft. Niet alleen kan je je daar makkelijk in vergissen, en bijvoorbeeld 1 ingeven voor maandag omdat je even vergeet dat programmeurs vanaf 0 beginnen tellen. In de VS zijn er christelijke programmeurs die vinden dat zondag de eerste dag van de week moet zijn. Die zouden de nummering dus bij zondag beginnen. _(Vreemd genoeg gaan ze voorbij aan het feit dat zondag zo dag 0 wordt, en maandag nog steeds de eerste dag is!)_

## Zo moet het ook niet

De reden voor deze mogelijke fouten ligt in het probleem dat mensen niet zo goed zijn met cijfers en dus vroeg of laat een fout maken. Met woorden zien we veel duidelijker wat de bedoeling is. De oplossing ligt dus voor de hand: gebruik een string in plaats van een nummer:

```csharp
public class Day {

    private string dayInWeek;
    public string DayInWeek { get => dayInWeek; }

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    public Day(int inMonth, string inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    public bool IsWeekend { get => dayInWeek.Equals("Saturday") || dayInWeek.Equals("Sunday"); }
}
```

de functie `WeekdayToString` wordt zo zelfs overbodig. En om te bepalen of een dag in het weekend valt vergelijken we de string met de dagen in het weekend. Maar daar zit een nieuw probleem. Niet alleen kan een computer veel sneller controleren of een getal kleiner dan 5 is, er is ook een kans dat we typfouten maken. Of we schrijven bijvoorbeeld `saturday`, zonder hoofdletter.

## Lang Leve de Enum

Ook deze oplossing is dus niet ideaal. En daarom gebruiken we enumeraties. Dan ziet deze class er zo uit.

```csharp
public enum Weekday {
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday,
};

public class Day {

    private Weekday dayInWeek;
    public Weekday DayInWeek { get => dayInWeek; }

    private int dayInMonth;
    public int DayInMonth { get => dayInMonth; }

    public Day(int inMonth, Weekday inWeek) {
        dayInMonth = inMonth;
        dayInWeek = inWeek;
    }

    public bool IsWeekend { get => dayInWeek > WeekDay.Friday; }
}
```

Afzonderlijk van de `class Day` declareren we nu een `enum WeekDay`. Die bevat een oplijsting van alle dagen in de week. De computer ziet deze lijst als een lijst van nummers, waarin `Monday` eigenlijk gelijk staat aan 0, `Tuesday` aan 1, enzovoort. Dat moeten we echter zelf niet onthouden. We kunnen de enum op de volgende manier gebruiken.

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // monday the 21st
    var day2 = new Day( 5, Weekday.Sunday); // sunday the 5th
    var day3 = new Day(13, Weekday.Friday); // friday the 13th
}
```

Niet alleen kunnen we ons nu niet van dag vergissen, spellingsfouten worden dadelijk opgemerkt door de compiler. Bovendien zal Visual Studio ons na het typen van `Weekday.` dadelijk tonen wat de mogelijke dagen zijn. En de computer zelf zal nummers gebruiken voor deze dagen. Vandaar dat we in de functie `IsWeekend` de dag van de week met vrijdag kunnen vergelijken.

En er is nog een voordeel: elke enum bevat automatisch een functie `ToString()` die de tekstuele representatie van de waarde geeft. De dag van de week als string tonen gaat dus vanzelf:

```csharp
public void Main() {
    var day1 = new Day(21, Weekday.Monday); // monday the 21st
    
    string result = day1.dayInWeek.ToString();

    // console.WriteLine maakt deze conversie zelfs automatisch
    Console.WriteLine("Day " + day1.dayInMonth + " is a " + day1.dayInWeek);
}
```

## In the Loop

Je kan enums ook eenvoudig in een loop gebruiken. Uiteindelijk is een enum niet meer dan een reeks getallen met een naam. De loop variabele kan dus ook een enum zijn. Wat niet zo eenvoudig is, is het bepalen van de grootste waarde. Dat kan je oplossen door die expliciet in je enum te declareren.:

```csharp
enum Values { one, two, tree, End }

for (Values i = 0; i < Values.End; i++) {
  Console.WriteLine(i);
}
```

## Een random Enum waarde

Soms wil je een willekeurige enum waarde toekennen aan een variabele. Je zou het volgende kunnen proberen:

```csharp
var generator = new Random();
var value = Random.Next(Values.End); // <-- Compiler geeft een fout
```

Ook al is een enum eigenlijk een getal, de functie Next wil echt een integer zien. Dit los je op door
de enum hier te converteren naar een integer:

```csharp
var generator = new Random();
var value = Random.Next((int)Values.End); // <-- Compiler geeft GEEN fout
```

## Oefeningen

In deze oefenreeks gebruiken we nog iets nieuws: Overrides.

Elke class die je maakt is afgeleid van een andere class: `Object`. Deze class heeft onder meer functie `ToString()`. Daardoor kan je
elke class die je maakt rechtstreeks gebruiken met `Console.WriteLine()`. Bijvoorbeeld zo:

```csharp
class BankAccount {
    public string Name { get; set; }
    public int Balance { get; set; }
}

var account = new BankAccount();
Console.WriteLine("Dit is een " + account);
```
Het resultaat zou de naam van de class zijn:
```
Dit is een BankAccount
```

Je kan die functie ook _overschrijven_. Je zegt dat aan de compiler "Wanneer iemand om de functie `ToString()` vraagt, gebruik dan deze
versie in plaats van de standaard versie." Je doet dat door de functie te voorzien van het keyword `override`. De functienaam, argumenten en
resultaat moeten wel gelijk zijn aan de oorspronkelijke functie. Maar de compiler helpt je daarbij. Wanneer je override typt in een class, dan
zal de compiler je de functies tonen die je kan overschrijven. Je selecteert dan de functie die je wil overschrijven. 

```csharp
class BankAccount {
    public string Name { get; set; }
    public int Balance { get; set; }

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
```
Account one has a balance of 1000 Euro
```

<div class="note oefening">
    <p>Open het project <a href="https://github.com/sma-it/oefening-enum-1">oefening-enum-1</a> en maak de oefeningenreeks</p>
</div>
