---
title: Je Eerste Programma
---

<div class="header1" id="top" markdown = "1"># Je Eerste Programma
</div>

<div class="header2" markdown = "1">## Visual Studio Installeren
</div>

Wanneer je een tekst wil schrijven, dan kan je dat doen met eender welk programma waar je in kan typen. Notepad is al voldoende. Toch zal je werk wellicht vlotter gaan als je een programma gebruikt dat specifiek bedoeld is voor het schrijven van teksten, zoals OpenOffice Writer of Microsoft Word.

Ook programmeren kan simpelweg in Notepad, maar ook hier geldt dat je het jezelf een stuk makkelijker maakt met een programma dat speciaal gemaakt is voor programmeurs en voor de programmeertaal die je gebruikt. In deze cursus gebruiken we C# om te leren programmeren. Daarom gebruiken we ook een editor die zeer geschikt is voor C#: **Microsoft Visual Studio**. Omdat we software ontwikkelen, noemen we dit ook wel een **ontwikkelomgeving**.

<div class="header2" markdown = "1">## Download & Installatie 
</div>


Indien Visual Studio nog niet op je computer staat, dan moet je dit programma eerst downloaden. Ga naar de <a href="https://visualstudio.microsoft.com/vs/community/" target="_blank">Visual Studio website</a> en download de meest recente versie van Visual Studio.

Tijdens de installatie krijg je onderstaand scherm. Vergeet hierbij niet de workload aan te vinken die je zal toelaten om console programma's in C# uit te voeren. Deze workload is `.net Desktop Development`. Vink dit aan en ga verder met de installatie.

Eens gedownload moet je het installatieprogramma uitvoeren. Je kan akkoord gaan met de standaard opties bij het installeren. Kies zeker voor de community versie: de professional en enterprise versies heb je echt niet nodig, en bovendien zijn die niet gratis.

Wanneer de installatie gestart is, kan je _Workloads_ kiezen. Voorlopig heb je enkel de _.NET Desktop development_ workload nodig. Later in de cursus gebruiken we ook andere workloads, maar op dat moment is het eenvoudig om die toe te voegen.

![image](/img/basics/eerste_programma/netWorkload.JPG)

### Launch

Na het installeren kan je visual studio starten. De eerste keer zal je moeten inloggen. _(Je kan dat de eerste maand overslaan, maar daarna niet meer. Dus maak je beter dadelijk een account.)_  Inloggen moet gebeuren met een Microsoft Account. Als je al een Microsoft account hebt, dan kan je daar mee inloggen. Heb je er geen en wil je geen persoonlijk account, dan kan je je school account gebruiken: `voornaam.naam@arcadiascholen.be`.

### Problemen?

Zit je vast met de installatie. Bekijk dan <a href="https://www.youtube.com/watch?v=EF5YDkGu5Lk" target="_blank">deze video</a>. De eerste drie minuten tonen je hoe je Visual Studio installeert. _De rest van de video is niet van toepassing op deze cursus._

<div class="header2" markdown = "1">## Een Project Maken
</div>

Om code te kunnen schrijven heb je een project nodig. Afhankelijk van het soort applicatie dat je maakt, kies je een project type. In het eerste deel van deze cursus werk je uitsluitend met console projecten.

### Een nieuw console project

Kies in het menu bovenaan _'File -> New -> Project'_. Kies nu in het menu links _'Installed -> Visual C# -> Get Started -> Console App'_.

Voor dat je op OK klikt, pas je best de instellingen van je project aan:

* **Name:** MijnEersteProgramma
* **Location:** Kies een geschikte folder, zoals **C:\users\account\programmas\\**
* **Solution:** Create new solution
* **Create directory for solution:** Niet aanvinken voor een klein project zoals een oefening.
* **Create new Git repository**: Niet aanvinken

![Demo](/img/basics/eerste_programma/01.gif)

### Je programma starten

Je kan je programma starten door bovenaan **Start** te kiezen. Je nieuwe programma zal de tekst `'Hello World'` op het scherm tonen. Sluit je programma af door op de spatiebalk te duwen.

<div class="note protip">
<p>Je zal dit jaar heel vaak een programma moeten starten. Dat kan via de button <b>Start</b>, maar nog sneller via de functietoets F5.</p>
</div>

### Code Aanpassen

Een programma bestaat uit code. Op dit moment geeft die code je computer de instructie om een console te tonen met daarin een tekst. Je kan deze code ook bekijken.

* Open de Solution Explorer als die nog niet zichtbaar is via _'View -> Solution Explorer'_. 
* In de Solution explorer zie je een boomstructuur met bovenaan je _Solution_. In die Solution zie je je programma, met daarin alle bestanden die bij je programma horen. 
* Open het bestand **Program.cs**.
* Je ziet de volgende code. Welke regel zorgt er voor dat je een tekst op het scherm toont?

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

<div class="note oefening">
<p>Pas de tekst 'Hello World' aan en start het programma opnieuw.</p>
</div>

<div class="toTop"><a href="#top">Omhoog</a></div>


