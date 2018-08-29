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

### Interpreteren van foutmeldingen

#### Foutmeldingen tijdens het ingeven van code

Reeds tijdens het ingeven van code krijg je reeds aanduidingen van mogelijke fouten. Het deel van de code waar de mogelijke fout zich bevindt, wordt onderlijnd. Hiervoor worden kunnen twee kleuren gebruikt worden:

* Een rode, gekartelde lijn: er bevindt zich op deze plaats een fout tegen de syntax (schrijfwijze). Dit kan bijvoorbeeld een vergeten punt-komma op het einde van een instructie zijn.
* Een groene, gekartelde lijn: dit duidt op een waarschuwing. Je declareerde bijvoorbeeld een variabele (zie hoofdstuk data_types), maar je gebruikt deze nergens. Er wordt door deze variabele dus onnodige geheugenruimte ingenomen. Door deze variabele in het groen te onderlijnen word je hier attent op gemaakt.

Door de cursor op het onderlijnde stuk code te plaatsen krijg je extra informatie over de fout.

<div class="note protip">
<p>Negeer de foutmeldingen die reeds aangegeven worden bij het ingeven van je code niet! Bekijk je code kritisch en los eventuele problemen op.</p>
</div>

#### Foutmeldingen tijdens het builden

Nadat je je programma gestart hebt met `start` of `F5` kan het zijn dat je het volgende dialoogvenster ziet verschijnen: `There were some build errors. Would you like to continue and run the last successful build?`. De antwoordmogelijkheden zijn `Yes` en `No`. Aangezien deze boodschap duidt op fouten in je code, kies je natuurlijk voor `No`.

Je weet nu dat je programma fouten bevat en het is aan jou om deze op te lossen. Onderaan het venster kan je de `Error list` opvragen. Je krijg daar een overzicht en verklaring van alle gevonden fouten. Door te dubbelklikken op de fout ga je naar de lijn code die de fout veroorzaakt heeft. Het is uiterst belangrijk dat je de foutmelding grondig leest en interpreteert. Vaak kan je aan de hand van de foutmelding de oplossing al achterhalen. Neem steeds het initiatief om zelf fouten in je code trachten op te lossen, zelfredzaamheid is immers een belangrijke attitude voor een informaticus. Indien het je echt niet lukt het probleem te verhelpen, kan je de leerkracht steeds om hulp vragen.

<div class="note protip">
<p>Lees en interpreteer foutmeldingen! Ze zetten je vaak op weg om de oplossing voor een probleem in je code te vinden.</p>
</div>

### Het gebruik van onderbrekingspunten



## Een Project Downloaden via Github
