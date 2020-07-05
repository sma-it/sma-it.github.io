---
title: Ken Je Editor
---
<div class="header1" markdown = "1"># Ken je editor
</div>

In dit hoofdstuk overlopen we enkele belangrijke functies van Visual Studio. Daarnaast leer je ook hoe je je taken en testen voor dit vak maakt.

<div class="header2" markdown = "1">## Views
</div>
Views zijn windows binnen een programma. Eenvoudige programma's tonen dikwijls maar een view op elk moment. Maar Visual Studio bevat heel wat __Views__, en je kan er verschillende tegelijk tonen. Een view kan in het midden van je scherm staan, links, rechts of onderaan. En elke view kan je verplaatsen, sluiten en opnieuw openen. Vele views heb je alleen nodig voor heel specifieke doeleinden die op dit moment nog niet relevant zijn. Maar er zijn ook views die je nu al kan gebruiken.

Een overzicht van mogelijke Views vind je in het menu ``View``. Onderaan de lijst met beschikbare views vind je ook nog een uitklapmenu ``Other Windows`` met nog meer mogelijkheden.

### De Solution Explorer
Wanneer je een project opent, dan toont Visual Studio de Solution Explorer. Een __Solution__ is een verzameling van code, afbeeldingen enzovoort die je samen wil gebruiken. Voorlopig zullen we slechts een project per Solution nodig hebben, maar dat wordt later meer.

De Solution explorer toont de bestanden die bij je code horen op een gestructureerde manier.

![SolutionExplorer](/img/basics/ken_je_editor/solution_explorer.png)

Hierboven zie je een de solution explorer met een oefening uit deze cursus. Je ziet de naam ``oefening`` van de solution en het bijhorende project. ``oefening`` is de standaard naam voor alle oefeningen in deze cursus. Helemaal onderaan zie je de bestanden ``Program.cs`` en ``Test.cs``. Die hebben we reeds voorzien bij elke oefening. Bij eenvoudige oefeningen zal je code moeten toevoegen aan ``Program.cs``. Een meer complexe oefening zoals deze heeft een folder ``Oefeningen`` met extra ``.cs`` bestanden. In zo'n geval zal je daar je code moeten schrijven. 

In geen geval zal je ooit code moeten aanpassen in het bestand ``Test.cs`` of in de map ``Utils``. De code die daar staat dient om te controleren of je programma werkt zoals het hoort. Zou je die aanpassen dan lijkt het wel of je programma in orde is, maar krijg je gewoon geen meldingen meer over een of meerdere problemen.

De bestanden van een project staan ook ergens op de harddisk van je computer. Je kan ze eenvoudig terugvinden door rechts te klikken op een project en dan de optie ``Open Folder in File Explorer`` te kiezen.

![FileExplorer](/img/basics/ken_je_editor/file_explorer.gif)

### De Code Editor

In de Code Editor doe je het meeste werk. Je kan elk ``.cs`` bestand in je solution openen via een double-click. De vele mogelijkheden van de Code Editor komen later nog aan bod. Handig om weten is wel dat je de bestanden in de code editor kan herschikken. Dit is dikwijls nodig omdat je code die je eerder schreef wil zien terwijl je nieuwe code schrijft. Visual Studio laat je toe om meerdere bestanden naast mekaar te tonen. De animatie hieronder toont dit.

![EditorMove](/img/basics/ken_je_editor/code_editor_move.gif)

### Error List

Om van je code een programma te maken gebruik je de ``Start`` knop, of je drukt op F5. Heb je geen fouten gemaakt, dan start je programma. Staan er fouten in je code, dan toont Visual Studio de view ``Error List``. Hier zie je een overzicht van de fouten in je code. 

<div class="note protip">
<p>Los steeds de eerste foutmelding eerst op. Dikwijls genereert een enkele fout meer dan een melding.</p>
</div>

Via een double-click op de foutmelding brengt Visual Studio je naar de bestand en de regel waar het probleem zit. Dit helpt je om snel te vinden waar het mis gaat. (Al is dat in het voorbeeld hieronder zo ook wel duidelijk.)

![ErrorList](/img/basics/ken_je_editor/error.gif)


Het is uiterst belangrijk dat je de foutmelding grondig leest en interpreteert. Vaak kan je aan de hand van de foutmelding de oplossing al achterhalen. Neem steeds het initiatief om zelf fouten in je code trachten op te lossen, zelfredzaamheid is immers een belangrijke attitude voor een informaticus. Indien het je echt niet lukt het probleem te verhelpen, kan je de leerkracht steeds om hulp vragen.

<div class="note protip">
<p>Lees en interpreteer foutmeldingen! Ze zetten je vaak op weg om de oplossing voor een probleem in je code te vinden.</p>
</div>

Nadat je je programma gestart hebt met `start` of `F5` kan het zijn dat je het volgende dialoogvenster ziet verschijnen: `There were some build errors. Would you like to continue and run the last successful build?`. De antwoordmogelijkheden zijn `Yes` en `No`. Aangezien deze boodschap duidt op fouten in je code, kies je natuurlijk voor `No`. Je kan ook kiezen voor de optie `Always choose this option` om te voorkomen dat je dit venster opnieuw ziet. 

### C# Interactive

Via ``View -> Other Windows`` vind je ook ``C# Interactive``. Dit is een console interface waarin je code kan uitproberen. C# Interactive is niet bedoeld om echt programma's in te schrijven, maar kan van pas komen wanneer je snel iets wil testen. Naast kennis van C# heb je ook enkele commando's nodig:

- ``#reset``: zorgt ervoor dat de interface alle code vergeet die je tot dan toe invoerde.
- ``#clear``: maakt het scherm leeg.

Hieronder zie je een heel korte demo. Later in de cursus zullen we C# Interactive meer gebruiken.

![Interactive](/img/basics/ken_je_editor/interactive.gif)

<div class="header2" markdown = "1">## De Code Editor
</div>

Het ingeven van code in Visual Studio is vrij vanzelfsprekend. Er zijn echter een aantal punten die het werken met de editor en het debuggen van je programma makkelijker kunnen maken.

### Indents

Een programma kan uit vele lijnen code bestaan. Het is belangrijk om deze zo leesbaar mogelijk op te bouwen. Indents spelen hierin een grote rol. Indents slaat op de tabstops die je in de code ziet. Die tabstops maken duidelijk wat bij welk onderdeel van een stukje code hoort.

In het vorige hoofdstuk zag je reeds het onderstaande ``Hello Word`` programma:

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

We hernemen dit Hello Word programma, maar nu zonder indents:

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

Je merkt dadelijk dat de tweede versie, zonder de tabs, een onduidelijker beeld geeft van wat bij welk onderdeel hoort.

<div class="note protip">
<p>Maak steeds gebruik van indents (tabs) om je code een duidelijke structuur te geven.</p>
</div>

Tijdens het werken met Visual Studio zal je merken dat de editor je code meestal vanzelf juist schikt. Op het moment dat de editor dat niet meer doet, zit je meestal al met fouten in je code. Je lost dan best eerst je fouten op, voor je verder werkt. 

Toch zal je door aan je code te werken (toevoegen, aanpassen, verwijderen) deze automatische schikking soms teniet doen. Ook daar is een handige oplossing voor. Je kan je volledige code, of een selectie ervan, opnieuw automatisch laten schikken met de volgende shortcuts:

* CTRL-K-D: schik de gehele code
* CTRL-K-F: schik het geselecteerde deel van de code

<div class="note protip">
<p>Maak gebruik van de shortcuts om de indents van je code (of een deel ervan) opnieuw in te stellen.</p>
</div>

### Intellisense
Er zijn nog andere manieren waarop de editor je helpt. Zo is er ``Intellisense``: de editor bekijkt constant wat je doet en probeert je te helpen. Wanneer je bijvoorbeeld iets op het scherm wil schrijven, dan zal de editor al na het typen van de eerste letters voorstellen om ``Cons`` te vervolledigen tot ``Console``. Druk je op dat moment op de ``tab`` toets, dan moet je verder niets meer typen.

Typ je daarna een punt, dan zal Intellisense je tonen welke opties ``Console`` je geeft. Misschien weet je niet meer precies hoe je iets op het scherm zet? Typ gewoon ``write`` en Intellisense toont je enkel de opties waar die lettercombinatie in voorkomt. Je kan dan via de pijltjestoetsen de correcte functie kiezen, en die toevoegen via ``tab``.

Ook bij het ingeven van argumenten zal Intellisense je helpen door te tonen wat voor argumenten je kan gebruiken. _(In het geval van Writeline is dat minder duidelijk omdat er hier erg veel mogelijkheden zijn.)_

![Intellisense](/img/basics/ken_je_editor/intellisense.gif)

<div class="note protip">
<p>Op het moment dat Intellisense je niet meer helpt, zitten er al fouten in je code. Denk dan niet dat je die later wel oplost: zonder Intellisense maak je ongetwijfeld nog meer fouten en moet je achteraf al die fouten tegelijk oplossen. Haal steeds direct de fouten uit je code voor je verder werkt.</p>
</div>

### Squiggly & Dotted Lines
En de editor helpt je nog meer! Code die niet helemaal OK is, wordt aangeduid met ``Squiggly Lines`` _(gegolfde lijnen, maar het klinkt leuker in het Engels)_.

Er zijn drie soorten lijnen, met elk een eigen betekenis:

- rode golfjes: Dit is een fout. Deze code moet je aanpassen voor je je programma kan uitvoeren. In het onderstaande voorbeeld werd ``writeline`` zonder hoofdletter geschreven.
- groene golfjes: Dit is een waarschuwing. Je code zal wel werken, maar het kan beter. Het is ook mogelijk dat de code wel werkt, maar niet zoals je verwacht. In het voorbeeld wordt ``value`` gedeclareerd, maar nooit gebruikt. De declaratie is dus overbodig.
- grijze puntjes: Dit is een stijlfout. Zo begint de functienaam hieronder met een kleine letter. Dat is niet fout, maar er is een algemene consensus om public functies te laten beginnen met een hoofdletter. Zo kan je later altijd eenvoudig zien dat het om een publieke functie gaat.

Het blijft ook niet bij het aanduiden van de fouten. De editor geeft je ook suggesties om de fout op te lossen. Daar mag je wel niet blind op vertrouwen. Dikwijls zijn er verschillende suggesties, of is het voorstel van de editor niet correct in jouw situatie. Je moet dus nog altijd zelf weten wat er moet gebeuren, zodat je de correcte suggestie kan kiezen.

![Correcties](/img/basics/ken_je_editor/correcties.gif)


### Commentaar

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

Voorzie je code van voldoende commentaar. Zo kan een functie die je schrijft vandaag nog overduidelijk voor je zijn. Als je je code een tijd later opnieuw bekijkt, is het vaak al heel wat minder evident om terug te vinden wat elke stukje code ook weer deed.

Ook voor collega's waarmee je samenwerkt aan een project of die later aanpassingen aan je code moeten aanbrengen, is commentaar handig om te begrijpen wat elk onderdeel van je programma doet.

<div class="note protip">
<p>Voorzie je code van commentaar. Je maakt het jezelf en je collega's makkelijker door dit te doen.</p>
</div>

<div class="header2" markdown = "1">## Breakpoints
</div>

Soms werkt je code, maar geeft die niet het gewenste resultaat. Je kan zeker goed naar je code kijken om te zien wat er scheelt, maar ook hier kan de code editor je helpen: Je kan ``breakpoints`` toevoegen aan je code om het programma te pauseren waar je wil, door te dubbelklikken in de marge. Dat laat je toe de waarde van elke variabele te controleren.

Ook kan je op dat moment de code regel voor regel verder uitvoeren via de shortcut ``F10``. 

Hieronder verwacht ik als resultaat van een deling 25, maar het programma toont enkel 20 op het scherm. Via een breakpoint leer ik dat het mis gaat bij de deling. _(Later leer je waarom.)_

![Breakpoints](/img/basics/ken_je_editor/breakpoint.gif)

<div class="header2" markdown = "1">## Een Project Downloaden via Github
</div>

Github is een website waar softwareontwikkelaars samen aan code kunnen werken. Een belangrijke functie van Github is dat iedereen die code ook kan downloaden. Elke oefenreeks in deze cursus is een Github project. Wanneer je een oefening wil maken, dan volg je een link in de cursus naar het bijhorende Github project. [Dit](https://github.com/sma-it/oefening-datatypes-1) is bijvoorbeeld een link naar de oefenreeks bij het volgende hoofdstuk.

Op de project pagina heb je rechts een groene knop ``Clone or download``. Via die knop kan je een link kopieren waarmee je je project in Visual Studio kan openen. _Het is mogelijk dat er ook een optie zichtbaar is ``Open in Visual Studio``, maar die is niet altijd aanwezig._

![Github](/img/basics/ken_je_editor/github.gif)

Nu de link in het geheugen van je computer zit, open je the ``Team Explorer`` in visual studio. Meestal vind je die in een side-panel, achter de Solution Explorer. Vind je hem niet, dan kan je de Team Explorer steeds openen via het ``View`` menu. In dit menu kies je de optie ``Clone``. Je plakt de github locatie in het eerste veld. Eventueel kan je ook aangeven waar je dit project wil bewaren. _(In de klas kan je niet aan je C-Schijf, dus je kiest een locatie op de D-schrijf.)_

![Clone](/img/basics/ken_je_editor/clone.gif)

Nu je een lokale kopie van de oefenreeks hebt, kan je de ``solution``, met daarin het project met oefeningen, openen in Visual Studio. Dit doe je door het nieuw toegevoegde project te dubbelklikken en vervolgens te dubbelklikken op de solution. Daarna kan je overschakelen naar de Solution Explorer.

![Open](/img/basics/ken_je_editor/open_solution.gif)

<div class="header2" markdown = "1">## Je werk opslaan
</div>

Telkens je je project probeert uit te voeren, of het nu fouten bevat of niet, zal Visual Studio je wijzigingen opslaan. Zolang je dus regelmatig test, zal je je werk dus niet verliezen. Maar wat als je je werk mee naar huis wil nemen, bijvoorbeeld door het hele project te mailen naar jezelf of door het op te slaan op een USB stick?

Het eerste dat je moet weten is dat broncode op zich niet veel plaats in beslag neemt. Het gecompileerde programma doet dat echter wel. Als je dus zonder meer je project overzet naar een USB-stick of naar het internet, dan kan dat wel eens heel lang duren. Maar dat gecompileerde programma heb je eigenlijk niet nodig. Je kan dat op elk moment terug genereren vanuit je code. Het eerste wat je daarom doet wanneer je je project wil meenemen, is een ``Clean`` uitvoeren. 

Dat kan eenvoudig via het right-click menu dat verschijnt wanneer je op de solution klikt.

![Clean](/img/basics/ken_je_editor/clean.gif)

Daarna kan je de projectlocatie openen in de file explorer. Ook dat kan eenvoudig via de solution explorer. Je verwijdert dan nog best de folder ``packages``. Ook die kan erg groot zijn, en visual studio maakt die folder opnieuw aan wanneer die ontbreekt. Van de overige inhoud kan je dan een zipfile maken.

![Zip](/img/basics/ken_je_editor/zip.gif)

_Bij een klein project, zoals deze oefenreeksen, kan je ook enkel de ``.cs`` bestanden selecteren en bewaren. Je kan dan achteraf het project opnieuw downloaden via Github en de ``.cs`` bestanden vervangen._
