---
title: Ken Je Editor
---

In dit hoofdstuk overlopen we enkele belangrijke functies van Visual Studio. Daarnaast leer je ook hoe je je taken en testen voor dit vak maakt.

## De Interface

Het ingeven va code in Visual Studio is vrij vanzelfsprekend. Er zijn echter een aantal punten die het werken met de editor en het debuggen van je programma makkelijker kunnen maken.

### Indentatie

Een programma kan uit vele lijnen code bestaan. Het is belangrijk om deze zo leesbaar mogelijk op te bouwen. Indentatie speelt hierin een grote rol. Indentatie slaat op de insprongen die je in de code ziet. Die insprongen maken duidelijk wat bij welk onderdeel van een stukje code hoort.

In het vorige hoofdstuk zag je reeds het onderstaande Hello Word programma:

```csharp
namespace MijnProgramma
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World!");
      Console.ReadKey();
    }
  }
}
```

We hernemen dit Hello Word programma, maar nu zonder indentatie:

```csharp
namespace MijnProgramma
{
class Program
{
static void Main(string[] args)
{
Console.WriteLine("Hello World!");
Console.ReadKey();
}
}
}
```

Je merkt dadelijk dat de tweede versie, zonder de insprongen, een onduidelijker beeld geeft van wat bij welk onderdeel hoort.

<div class="note protip">
<p>Maak steeds gebruik van indentatie om je code een duidelijke structuur te geven.</p>
</div>

Tijdens het werken met Visual Studio zal je merken dat de editor reeds zelf een zekere vorm van schikking en insprongen aanbrengt. Dit zorgt reeds voor een zekere conformiteit in de code. Toch zal je door aan je code te werken (toevoegen, aanpassen, verwijderen) deze automatische schikking soms teniet doen. Ook daar is een handige oplossing voor. Je kan je volledige code, of een selectie ervan, opnieuw automatisch laten schikken met de volgende shortcuts:

* CTRL-K-D: schik de gehele code
* CTRL-K-F: schik het geselecteerde deel van de code

<div class="note protip">
<p>Maak gebruik van de shortcuts om de indentatie van je code (of een deel ervan) opnieuw in te stellen.</p>
</div>

Commentaar voeg je als volgt in je code in:

Methode 1: de dubbele slash.

```csharp
// Een enkele commentaarlijn wordt vooraf gegaan door een dubbele slash.
namespace MijnProgramma
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World!");
      Console.ReadKey();
    }
  }
}
```

Methode 2: de slash in combinatie met de asterisk.

```csharp
namespace MijnProgramma
{
  class Program
  {
    /* Het hele blok tekst dat zich tussen het begin- en het eindcommentaarteken bevindt, 
     * wordt als commentaar beschouwd.
     * Dit is handig als je meerdere lijnen in commentaar wil zetten.
     */
      static void Main(string[] args)
      {
        Console.WriteLine("Hello World!");
        Console.ReadKey();
      }
  }
}

```

### Gebruik van commentaar

Voorzie je code van voldoende commentaar. Zo kan een functie die je schrijft vandaag nog overduidelijk voor je zijn. Als je je code een tijd later opnieuw bekijkt, is het vaak al heel wat minder evident om terug te vinden wat elke stukje code ook weer deed.

Ook voor collega's waarmee je samenwerkt aan een project of die later aanpassingen aan je code moeten aanbrengen, is commentaar handig om te begrijpen wat elk onderdeel van je programma doet.

<div class="note protip">
<p>Voorzie je code van commentaar. Je maakt het jezelf en je collega's makkelijker door dit te doen.</p>
</div>



## Een Project Downloaden via Github
