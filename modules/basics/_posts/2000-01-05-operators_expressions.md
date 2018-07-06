---
title: Operators, Expressies en Statements
---

## Operators

Operatoren zijn de bouwstenen waarmee code kan opgebouwd worden. Ze worden gebruikt om een actie uit te voeren op operanden. In C# zijn een groot aantal operatoren voorgedefiniëerd. In wat volgt worden veelgebruikte operatoren besproken.

### Toekenningsoperator

In het statement

    x=10;

is het gelijkheidsteken (=) de toekenningsoperator.

### Wiskundige operatoren en volgorde van bewerkingen


#### Wiskundige operatoren

Onderstaande tabel geeft een overzicht van enkele veelgebruikte wiskundige operatoren:

![wiskundige operatoren](/img/operators_expressies_statements/wiskundige_operatoren.png)

De meeste wiskundige operatoren ken je reeds vanuit de wiskunde. Enkele operatoren vragen echter een extra woordje uitleg.

`++`  Verhoogt de waarde van de operand waarop hij toegepast wordt met 1.

```csharp
x=10;
x++; // x is nu gelijk aan 11.
```

`--`  Verlaagt de waarde van de operand waarop hij toegepast wordt met 1.

```csharp
x=10;
x--; // x is nu gelijk aan 9.
```

`%` Geeft de rest na een gehele deling als resultaat.

```csharp
int x, y;
x=16;
y=x%3; // y is nu gelijk aan 1;
```

De berekening van deze waarde gaat als volgt:

3 gaat 5 maal volledig in 16

3 x 5 = 15

16 - 15 = 1 -> De rest na deling van 16 door 3 is 1


#### Volgorde van bewerkingen

De volgorde van de bewerkingen in een berekening is gelijk aan de voorrang die in wiskunde gebruikt wordt. D.m.v. ronde haakjes kan je een andere volgorde van bewerkingen opgeven.

Voorbeeld:

(a + b) x (c + d) is verschillend van a + b x c + d


### Vergelijkingsoperatoren

Onderstaande tabel geeft een overzicht van de vergelijkinsoperatoren:

![vergelijkingsoperatoren](/img/operators_expressies_statements/vergelijkingsoperatoren.png)

<div class="note waarschuwing">
<p>Een vaak gemaakte fout is het verwisselen van de toekenningsoperator (=) en de vergelijkingsoperator (==).
Zorg ervoor dat je in vergelijkingen steeds de vergelijkingsoperator gebruikt.</p>
</div>

### Logische operatoren

Onderstaande tabel geeft een overzicht van de logische operatoren:

![logische operatoren](/img/operators_expressies_statements/logische_operatoren.png)

| Operator&nbsp;&nbsp;| Betekenis   |
| --------------- |-------------    |
| ==        | is gelijk aan         |
| !=        | is niet gelijk aan    |
| <         | is kleiner dan        |
| >         | is groter dan         |
| <=        | is kleiner of gelijk aan |
| >=        | is groter of gelijk aan  |


## Expressies

Een expressie is opgebouwd uit operatoren en operanden.

Voorbeelden:

```csharp
int a;              //Operatoren int en ; /operand: a

Console.ReadLine(); //Operator: ReadLine() / operand: Console

(a>b)               //Operator: > / operanden a en b
```

Het laatste voorbeeld (a>b) is een speciaal type expressie, namelijk een Booleaanse expressie. Een Booleaanse expressie heeft steeds `true`of `false`als resultaat. In een conditionele statement (zie volgend punt) gebruiken we een of meerdere Booleaanse expressies om de conditie (voorwaarde) samen te stellen. Afhankelijk van het resultaat van deze Booleaanse expressie(s) zal het programma een bepaald verloop kennen.

## Statements

Een statement is een volledige instructie, meestal afgesloten met een puntkomma. Een statement is opgebouwd uit één of meerdere expressies.

Voorbeelden:

```csharp

//Statement 1

int x;

//Statement 2

int a=10;

//Statement 3

naam=Console.ReadLine();

//Statement 4: de volledige if-else structuur vormt 1 conditionele statement,
//bestaande uit verschillende instructies

if(int a==10)
{
    Console.WriteLine("Het ingegeven getal is 10.");
}
else
{
    Console.WriteLine("Het ingegeven getal is verschillende van 10);
}
```

<div class="note waarschuwing">
<p>Bouw je programma steeds op uit volledige statemens.</p>
</div>

<div class="note oefening">
<p>Verwijzing naar oefeningen. (Opsplitsen in onderdelen? Implementatie van if-else?</p>
</div>



