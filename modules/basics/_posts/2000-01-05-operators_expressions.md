---
title: operatoren
---
<div class="header1" id="top" markdown = "1"># operatoren
</div>
<div class="header2" markdown = "1">## operatoren
</div>

Operatoren zijn de bouwstenen waarmee code kan opgebouwd worden. Ze worden gebruikt om een actie uit te voeren op operanden. In C# zijn een groot aantal operatoren voorgedefinieerd. In wat volgt worden veelgebruikte operatoren besproken.

### Wiskundige operatoren

Onderstaande tabel geeft een overzicht van enkele veelgebruikte wiskundige operatoren:

| Operator  | Bewerking         |
| --------- |-------------      |
| +         | som               |
| -         | verschil          | 
| *         | vermenigvuldiging |
| /         | deling            |
| %         | rest na deling    |
{:.tableBorder}


De meeste wiskundige operatoren ken je reeds vanuit de wiskunde. 

De operator die de rest na gehele deling als resultaat (`%`) geeft, vraagt een extra woordje uitleg. Het onderstaande voorbeeld toont hoe deze operator gebruikt wordt. Opmerking: deze operator werkt met gehele getallen (integers).

```csharp
int x, y;
x = 16;
y = x % 3; // y is nu gelijk aan 1;
```

De berekening van deze waarde gaat als volgt:

3 gaat 5 maal volledig in 16

3 x 5 = 15

16 - 15 = 1 -> De rest na gehele deling van 16 door 3 is 1


### Volgorde van bewerkingen

De volgorde van de bewerkingen in een berekening is gelijk aan de voorrang die in wiskunde gebruikt wordt. D.m.v. ronde haakjes kan je een andere volgorde van bewerkingen opgeven.

Deze volgorde is:
- haakjes
- vermenigvuldigen, delen en rest (*, /, %)
- optellen en aftrekken (+, -)

Voorbeeld:

(a + b) * (c + d) is verschillend van a + b * c + d

### Increment en decrement operatoren

| Operator  | Bewerking         | Hoe gebruiken? | Volledige schrijfwijze |
| --------- |-------------      | -------------- | ---------------------- |
| ++        | verhoog met 1     | i++;           | i = i + 1;             |
| -\-       | verminder met 1   | i-\-;           | i = i - 1;             |
{:.tableBorder}


Onderstaande voorbeelden tonen aan hoe deze operatoren gebruikt worden:

`++`  Verhoogt de waarde van de operand waarop hij toegepast wordt met 1.

```csharp
x = 10;
x++; // x is nu gelijk aan 11.
```

`--`  Verlaagt de waarde van de operand waarop hij toegepast wordt met 1.

```csharp
x = 10;
x--; // x is nu gelijk aan 9.
```

### Toekenningsoperator

In onderstaande statements

```csharp
x = 10;
a = b * 10;
```

is het gelijkheidsteken (`=`) de toekenningsoperator.

Verder bestaan er toekenningsoperatoren die eigenlijk verkorte schrijfwijzen van een bewerking zijn. Onderstaande tabel geeft een overzicht. Het getal 2 dat in de voorbeelden gebruikt wordt, kan vervangen worden door een willekeurig getal of een variabele.

| Operator  | Hoe gebruiken?| Volledige schrijfwijze  |
| --------- |---------------|------------------------ |
| +=        | a += 2;       | a = a + 2;              |
| -=        | a -= 2;       | a = a - 2;              |
| *=        | a *= 2;       | a = a * 2;              |
| /=        | a /= 2;       | a = a / 2;              |
| %=        | a %= 2;       | a = a % 2;              |
{:.tableBorder}


### Vergelijkingsoperatoren

Onderstaande tabel geeft een overzicht van de vergelijkingsoperatoren. Een vergelijkingsoperator zal steeds `true` of `false` als resultaat geven.

| Operator   | Betekenis         |
| ---------  |-------------      |
| ==         | is gelijk aan               |
| !=         | is niet gelijk aan          | 
| >          | is groter dan               |
| <          | is kleiner dan              |
| >=         | is groter dan of gelijk aan |
| <=         | is kleiner dan of gelijk aan|
{:.tableBorder}


<div class="note waarschuwing">
<p>Een vaak gemaakte fout is het verwisselen van de toekenningsoperator (=) en de vergelijkingsoperator (==).
Zorg ervoor dat je in vergelijkingen steeds de vergelijkingsoperator gebruikt.</p>
</div>

### Logische operatoren

Onderstaande tabel geeft een overzicht van de logische operatoren. Een logische operator gebruik je om voorwaarden samen te voegen (&& en \|\|) of om te keren (!). Het resultaat van het geheel zal steeds `true` of `false` zijn.  

| Operator  | Betekenis   |
| ----------|-------------|
| &&        | AND - de gehele voorwaarde is true indien beide termen van de operator true zijn            |
| \|\|        | OR - de gehele voorwaarde is true indien minstens één van de termen van de operator true is |
| !         | NOT - keert de waarde van de booleaanse vergelijking om                                     |
{:.tableBorder}


De onderstaande waarheidstabellen wanneer een operator `true` als resultaat geeft en wanneer `false`. Je vindt bij elke operator eveneens een concreet voorbeeld van de toepassing ervan.

`&&` De AND-operator geeft `true` als resultaat als aan beide voorwaarden voldaan is. Indien aan één of aan beide voorwaarden niet voldaan is, geeft deze operator `false` als resultaat.

Waarheidstabel: voorwaarde1 && voorwaarde2

| voorwaarde1 | voorwaarde2  | voorwaarde1 && voorwaarde2 |
| ----------- |------------- | -------------------------- |
| false       | false        | false                      |
| true        | false        | false                      |
| false       | true         | false                      |
| true        | true         | true                       |
{:.tableBorder}


Voorbeeld:

```csharp
int x; 

if (x >= 1 && x <= 100) // De vergelijking test of x tussen 1 en 100 ligt, grenzen 
                        // inbegrepen.
{

}
```

De operator levert volgende waarheidstabellen op voor verschillende waarden van x:

| Waarde x  | x >= 1  | x <= 100| (x >= 1 && x <= 100) |
| --------- |---------|-----|------------------|
| -3        | false | true  | false            |
| 49        | true  | true  | true             |
| 110       | true  | false | false            |
{:.tableBorder}


`||` De OR-operator geeft `true` als resultaat als aan minstens één van beide voorwaarden voldaan is. Enkel indien aan geen van beide voorwaarden voldaan is, geeft deze operator `false` als resultaat.

Waarheidstabel: voorwaarde1 \|\| voorwaarde2

| voorwaarde1 | voorwaarde2  | voorwaarde1 \|\| voorwaarde2 |
| ----------- |------------- | -------------------------- |
| false       | false        | false                      |
| true        | false        | true                       |
| false       | true         | true                       |
| true        | true         | true                       |
{:.tableBorder}


Voorbeeld:

```csharp
int x; 

if (x < 1 || x > 100) // De vergelijking test of x niet tussen 1 en 100 
                      // ligt, grenzen inbegrepen.
{

}
```

De operator levert volgende waarheidstabellen op voor verschillende waarden van x:

| Waarde x  | x < 1   | x > 100 | (x < 1 \|\| x > 100) |
| --------- |---------------|------------------|
| -3        | true  | false | true             |
| 49        | false | false | false            |
| 110       | false | true  | true             |
{:.tableBorder}


`!` De NOT-operator inverteert het resultaat van een booleaanse vergelijking. 
- De operator geeft `true` als het resultaat als de booleaanse vergelijking `false` is. 
- Indien het resultaat van de booleaanse vergelijking `true` is, geeft deze operator `false` als resultaat.

Waarheidstabel: !(voorwaarde)

| voorwaarde  | !(voorwaarde)| 
| ----------- |------------- |
| false       | true         | 
| true        | false        | 
{:.tableBorder}


Voorbeeld:

```csharp
int x; 

if (!( x==100 || x==1000 )) // De vergelijking geeft true als 
                            // x verschillend is van zowel 100 als 1000.
{

}
```

De operator levert volgende waarheidstabellen op voor verschillende waarden van x:

| Waarde x  | x == 100 | x == 1000 | (x == 100 \|\| x == 1000) | !(x == 100 \|\| x == 1000) |
| --------- |------- |-------- | --------------------- | ---------------------- |
| 50        | false  | false   | false                 | true                   |        
| 100       | true   | false   | true                  | false                  |
| 1000      | false  | true    | true                  | false                  |
{:.tableBorder}


<div class="toTop"><a href="#top">Omhoog</a></div>



