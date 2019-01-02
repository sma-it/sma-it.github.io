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
