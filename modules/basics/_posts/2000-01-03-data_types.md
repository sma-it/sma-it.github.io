---
title: Data Types en Variabelen
published: true
---


## Data types

Je programma kan gebruik maken van verschillende soorten gegevens. Zo kan je berekeningen maken met getallen, namen gebruiken, enz.

C# maakt gebruik van data types, of gegevenstypes, om met deze verschillende soorten gegevens te werken. Hieronder vind je een overzicht van de gegevenstypes die in de cursus gebruikt zullen worden.

![tabel_datatypes](/img/data_types/tabel_datatypes.png)


## Wat is een variabele?

Tijdens het uitvoeren van een programma zal het vaak nodig zijn om gegevens bij te houden in het geheugen van de computer. Enkele voorbeelden hiervan zijn invoer van de gebruiker of het resultaat van een berekening.

Om op een handige manier een geheugenplaats aan te kunnen spreken, maken we gebruik van een variabele. Door middel van de variabele kunnen we gegevens plaatsen in de geheugenplaats en de inhoud ervan terug oproepen. De inhoud van de variabele kan tijdens het programma gewijzigd worden.

Naast een naam, krijgt een variabele ook een data type. Dit gegevenstype bepaalt welk type informatie er in de variabele opgeslagen kan worden en welke bewerkingen er met de variabele kunnen gebeuren. Tevens bepaalt het gekozen gegevenstype hoeveel ruimte er in het geheugen voorzien zal worden om de data op te slaan.

## Declaratie van een variabele

Onder declaratie van een variabele verstaan we maken van de variabele. Dit houdt in dat er een naam en een data type aan de variabele toegekend worden.

Kies telkens een betekenisvolle naam voor je variabele en gebruik het correcte data type.

Enkele voorbeelden van declaraties:
```csharp
namespace MijnProgramma
 {
   class Program
   {
     static void Main(string[] args)
     {
       int x;               // Inhoud: een geheel getal
       string name;         // Inhoud: een tekenreeks
       float price;         // Inhoud: een kommagetal
       double averageSpeed; // Inhoud: een kommagetal
       char teken;          // Inhoud: 1 karakter

       Console.ReadKey();
     }
   }
 }
 ```

## Initialisatie van een variabele

Het initialiseren van een variabele houdt in dat je de variabele een waarde geeft. Dit kan op verschillende manieren gebeuren:

### De variabele gelijk stellen aan een waarde

```csharp
namespace MijnProgramma
 {
   class Program
   {
     static void Main(string[] args)
     {
       // Declaratie  
       int minimum;           
       string name;     
       float price; 
       double averageSpeed;
       char teken;

       // Initialisatie
       x=7;
       name="voorbeeld";  // Tekst plaats je tussen dubbele aanhalingstekens
       price=2.99F;       // Gebruik een punt bij het kommagetal. 
                          // Bij een float variabele laat je het getal volgen door de letter F
       averageSpeed=52.36;
       teken='C';         //Het karakter plaats je tussen enkele aanhalingstekens

       Console.ReadKey();
     }
   }
 }
 ```

### De variabele gelijk stellen aan invoer van de gebruiker

```csharp
namespace MijnProgramma
 {
   class Program
   {
     static void Main(string[] args)
     {
       // Declaratie  
      string name;
      int getal;              
       
       // Initialisatie
       Console.WriteLine("Geef je naam: ");
       name=Console.ReadLine(); // z wordt geïnitialiseerd op de invoer van het toetsenbord

       Console.WriteLine("Geef een getal: ");
       getal = Convert.ToInt32(Console.ReadLine()); // Let op de omzetting naar int
     
       Console.ReadKey();
     }
   }
 }
 ```

Gegevens die ingevoerd worden via het toetsenbord hebben steeds het gegevenstype string. Om deze invoer in variabelen met een ander gegevenstype te plaatsen is er een omzetting (conversie) nodig. In het bovenstaande voorbeeld wordt de omzetting van string naar int gedaan d.m.v. ```Convert.ToInt32()```.

Voor de andere data types bestaan er eveneens methods om deze conversie te doen: ```Convert.ToFloat()```, ```Convert.ToDouble()```, ```Convert.ToBoolean()```, ```Convert.ToChar()```


### De variabele gelijk stellen aan het resultaat van een bewerking

```csharp
namespace MijnProgramma
 {
   class Program
   {
     static void Main(string[] args)
     {
       // Declaratie  
       int x, y, z;   // Variabelen met hetzelfde data type kan je op 1 lijn declareren                 
       
       // Initialisatie
       x=7;
       y=10;
       z=x+y; // De variabele z wordt initialiseert op het resultaat van de bewerking

       Console.ReadKey();
     }
   }
 }
 ```

<div class="note waarschuwing">
<p>Een variabele moet steeds geïnitialiseerd zijn voordat hij gebruikt wordt. Een niet-geïnitialiseerde variabele gebruiken (in bijvoorbeeld een bewerking of uitvoer) kan tot onverwachte en foutieve resultaten leiden.</p>
</div>

## Automatische conversie tussen data types

In bepaalde gevallen zal C# zelf de conversie tussen gegevenstypes doen. De numerieke gegevenstypes hebben onderstaande hiërarchie:

* double (hoogste)
* float
* int (laagste)

Conversie van een lager gegevenstype naar een hoger gebeurt automatisch. Probeer je een variabele van een lager gegevenstype gelijk te stellen aan een hoger data type dan krijg je een foutmelding.

Enkele voorbeelden:

* Conversie van double naar int

```csharp
using System;

namespace Voorbeeld3
{
    class Program
    {
        static void Main(string[] args)
        {
            int x;  
            double y;

            x = 10;
            y = x;
            Console.ReadKey();
        }
    }
}
```

Aangezien dit een conversie van een lager naar een hoger gegevenstype is, lukt dit probleemloos.

* Conversie van int naar double (met foutmelding!)

```csharp
using System;

namespace Voorbeeld3
{
    class Program
    {
        static void Main(string[] args)
        {
            int x;  
            double y;

            y = 10.99;
            x = y;
            Console.ReadKey();
        }
    }
}
```

In bovenstaand voorbeeld wordt er geprobeerd om de inhoud van een variabele met hoger gegevenstype te plaatsen in een variabele van een lager data type. Dit geeft onderstaande foutmelding:

![foutmelding_conversie](/img/data_types/foutmelding_conversie.png)

## Een variabele op het scherm tonen

Inhoud volgt....

<div class="note oefening">
<p>1 Wat is een geschikt data type voor het opslaan van volgende gegevens: een leeftijd in jaren, de eenheidsprijs van een product, het aantal deelnemers aan een event, de naam van een bedrijf</p>

<p>2 Schrijf een programma dat de naam van de gebruiker vraagt en deze naam op het scherm toont.</p>

<p>3 Gebruik oefening 2 als basis en vraag nu een getal i.p.v. een naam. Het getal kan een geheel of een kommagetal zijn. Toon het getal op het scherm.</p>
</div>


