---
title: Wat is MonoGame?
---

# Libraries

Tot nu toe schreven we programma's die tekst tonen in een console. Dat is goed om de basics onder de knie te krijgen, maar uiteindelijk is dat meestal niet het soort programma dat je wil maken. C# is een programmeertaal die voor zowat alles bruikbaar is. Je kan er gewone Windows desktop programma's mee maken, maar ook mobile apps, interactieve websites en games. Ook bestaat er het Mono project, dat je toelaat om C# code zo te compileren dat je programma ook op linux (en macOS) kan werken.

Al die toepassingen hebben extra code nodig. Tot hiertoe schreef je voortdurend text in een console window. Je gebruikte daarvoor functies zoals

```csharp
Console.Write("Enter your name: ");
var input = Console.ReadLine();
```

Nu bestaat een console eigenlijk uit niets anders dan pixels op een scherm. Die pixels vormen letters, er is een scrollbar morgelijk en je kan zelfs tekst invoeren (en dat zijn ook weer gewoon pixels). Om deze functionaliteiten van de console (bv. invoer van het toetsenbord lezen) te kunnen gebruiken, moet je zelf geen code schrijven, die werd reeds voorzien binnen C#. Via het `Console` object kan je gewoon tekst toevoegen en lezen, zonder dat je moet weten wat er op de achtergrond gebeurt.

De `Console` is aanwezig in de C# core (basis) library. Dat betekent dat je de console in elk programma kan gebruiken. Wanneer je een ander soort programma wil schrijven, zoals een Windows desktop app, dan zal je meer nodig hebben dan een console. Je wil windows, buttons, labels, sliders en meer gebruiken. Maar die zitten niet in de core library! Je zal de library die je wil gebruiken moeten toevoegen aan je programma. Afhankelijk van de library die je wil gebruiken bestaan daar verschillende mogelijkheden voor.

_Later in deze cursus volgt een overzicht van al die mogelijkheden. Nu hebben we het enkel over MonoGame._

# Monogame

Als we een computer kopen, dan willen we daar vroeg of laat een spel op spelen. Dat weten ze bij Microsoft ook. Maar omwille van alle interactiviteit is het ontwikkelen van games behoorlijk complex. En als je code dan slechts werkt voor een enkel soort computer, dan wordt het moeilijk om uit de kosten te komen. Daarom ontwikkelde Microsoft het Xna Framework. Met Xna kan je games maken die werken op Windows, Windows Phone en Xbox.

Ondertussen is Windows Phone zo ongeveer dood en begraven. Dus blijven er nog twee platformen over. Wat eigenlijk niet zo veel is. Maar gelukkig is er MonoGame. Het Mono project is een open source project dat de belangrijkste C# libraries beschikbaar maakt voor Linux en MacOS. MonoGame is daar een onderdeel van. Code die je schrijft voor Xna werkt dankzij MonoGame ook op Linux. Maar MonoGame gaat nog een stap verder. Je kan zonder veel moeite je game ook laten werken op Playstation, Switch en Android.

Natuurlijk zijn er nog andere Frameworks, naast MonoGame. Vooral 3D game engines zoals Unity en Unreal zijn tegenwoordig heel populair. Toch zijn die niet zo efficient als je een 2D game wil maken, omwille van alle 3D functionaliteit die aanwezig is zonder dat je er gebruik van maakt.

Ook zijn er nog 2D game engines die MonoGame gebruiken maar er tools rond bouwen die het eenvoudiger maken om samen te werken met graphic designers.

We kiezen in deze cursus voor MonoGame omdat de library eenvoudig te installeren is en werkt op low budget computers. Samenwerken met andere graphics designers is voorlopig nog niet aan de orde. De voordelen van meer geavanceerde engines zijn dus beperkt. Bovendien geeft MonoGame je een extra voordeel: zowat elke game engine gebruikt dezelfde basisprincipes, maar dikwijls werken die op de achtergrond zonder dat je er iets van merkt. MonoGame laat je rechtstreeks met deze basics werken. Dat geeft je een goed inzicht in de eigenlijke werking van een game. Mocht je je later specializeren in game development, dan komt deze kennis je zeker van pas. Welke game engine je dan ook nodig hebt, je weet al hoe die eigenlijk werkt.

Maar ook als game development uiteindelijk niet je ding blijkt, dan nog zal je veel leren door het gebruik van MonoGame. Bijvoorbeeld hoe je omgaat met libraries, online oplossingen zoekt voor algemene problemen en je programma structureert in classes die alles overzichtelijk houden.

_Beginnende programmeurs zijn dikwijls geneigd om te kiezen voor de meest uitgebreide game engine, met een goed ogende interface en spectaculaire demo's. Die zien er dan ook heel goed uit. Maar vergeet niet dat al die extra mogelijkheden ook extra complexiteit met zich meebrengen. Het voelt goed om de basics van je game met enkele mouse clicks te genereren. Maar dat is enkel het begin. Daarna is er nog heel veel code nodig die specifiek is voor jouw game. Dat soort code leer je beter schrijven in een eenvoudige omgeving._

# Installatie

Monogame installeren is behoorlijk eenvoudig. Je opent de website monogame.net, klikt op _Get started_, je kiest de laatste versie en downloadt 'MonoGame for Visual Studio'. Eens je download klaar is, kan je het installatieprogramma uitvoeren. Waarschijnlijk krijg je dan een melding dat Windows dit programma niet kent. Je kiest dan voor 'advanced' en 'run anyway'.

# Je Eerste Project

## Een MonoGame app maken

Nadat je Monogame geïnstalleerd hebt, kan je een een nieuw project maken. In de categorie `Visual C#` vind je nu een subcategorie `MonoGame`. Daarin staan verschillende mogelijkheden. Om het eenvoudig te houden kies je voor `MonoGame Windows Project`. Geef je project een naam en kies de locatie om het op te slaan.

## De code lezen

Wanneer je een nieuw MonoGame project maakt, dan start je met twee bestanden waarin je al C# code vindt:

- Het eerste bestand is `Program.cs`. Daarin wordt het eigenlijke programma gestart.

```csharp
static void Main()
{
  using (var game = new Game1())    // Er wordt een nieuw object van de class Game1 gemaakt.
    game.Run();                     // De Run-functie uit de class Game1 wordt op het object 
                                    // toegepast.
}                                   // De Run-functie start het eigenlijke game.
```

De code hierboven maakt een object van de de class `Game1` en voert dan de `Run()` functie van die class uit. De class `Game1` is voorzien in elk nieuw project dat je maakt, zoals je in het volgende punt kan lezen.

- Het tweede bestand is `Game1.cs`. Dit bestand is het echte vertrekpunt voor je game. Het is belangrijk dat je weet wat er in dit bestand gebeurt. Dit wordt verder in dit hoofdstuk uitgelegd.

Zowat elke game engine werkt op dezelfde manier, de volgende stappen worden bij het starten en runnen van het game doorlopen:

Stap 1: Initialiseren van het game: De `Run()` functie uit het eerst bestand (in het geval van Monogame Program.cs zoals we hierboven zagen) zal eerst de game engine initialiseren.

Stap 2: In stap 1 wordt het spel opgestart door een object van de class `Game1`te 'runnen'. In het spelverloop komen nu volgende zaken aan bod: 
- de __content__ van je game wordt geladen. Dit zijn bijvoorbeeld afbeeldingen, geluiden en andere bestanden zoals game levels en dergelijke. In de volgende hoofdstukken zal je leren hoe je content voorziet en in je game gebruikt.
- Nu komt het belangrijkste deel: de __game loop__ (het 'lopen' van het spel). Die bestaat uit twee delen: `Update` en `Draw`. Je programma zal voortdurend deze twee delen afwisselen. (Zie hieronder) In de volgende hoofdstukken zal je leren hoe je d.m.v. instructies in deze functies een game maakt.

Stap 3: Tot slot is er nog een functie om de geladen content terug vrij te geven. Die wordt uitgevoerd wanneer je het programma sluit.

Zoals hierboven vermeld zijn `Update` en `Draw` het belangrijkste deel van je game. Deze onderdelen hebben volgende functie binnen het game:
- In `Update` hoor je alle berekeningen te doen, zoals aanpassen van posities, controleren of een toets ingedrukt werd, reageren op een mouse click etc. Ook informatie die via het netwerk binnenkomt kan hier verwerkt worden. 
- In `Draw` wordt al die informatie gebruikt om objecten op het scherm te tekenen.
Door `Update` en `Draw` dus voortdurend af te wisselen tijdens de game loop wordt dus telkens a.h.v. nieuwe gegevens uit de `Update` functie, uitvoer getoond door de `Draw` functie.

_Meestal zullen `Update` en `Draw` mekaar gewoon afwisselen. Maar het kan gebeuren dat je computer te traag blijkt, bijvoorbeeld omdat er andere programma's op de achtergrond plots veel werk hebben. In dat geval kan de game engine beslissen om een aantal `Draw` instructies over te slaan. Update wordt dan wel uitgevoerd, zodat de berekeningen accuraat blijven. Er zijn gewoon minder screen updates. Daarom is het belangrijk dat je het onderscheid maakt tussen deze twee functies. Ook al kan je in theorie positie updates en dergelijke ook in de `Draw` functie uitvoeren, het is een heel slecht idee om dat te doen._

## Beschrijving van de code van een nieuw, leeg programma 

Als je een nieuw project met Monogame maakt, bevat je project reeds een deel code. Het bestand `Program.cs` bespraken we hierboven al en dient om het spel te starten.

`Game1.cs` is het bestand waarin we zaken zullen toevoegen. Een beschrijving van de code die bij een nieuw, leeg project reeds in `Game1.cs` aanwezig is, vind je hieronder.

### Monogame laden

```csharp
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
```
In dit eerste deel wordt MonoGame geladen. Het lijkt alsof het niet MonoGame, maar Xna Framework is dat geladen wordt. Dat komt omdat MonoGame een volledige vervanging is van Xna Framework. Je kan dus ook Xna installeren in plaats van MonoGame en je programma compileren zonder dat je iets moet aanpassen. Maar dan werkt het wel enkel met Windows.

Opm.: Afhankelijk van wat je in je programma gebruikt, zal je hier nog extra zaken moeten laden. Zo zal bijvoorbeeld het gebruik van een `List` object in je game nog steeds vereisen dat je `using System.Collections.Generic;` laadt.

### Start van de class en declaratie van objecten i.v.m. het grafisch gedeelte + constructor met initialisatie van reeds voorziene objecten

```csharp
namespace Game1
{
    public class Game1 : Game
    {
        GraphicsDeviceManager graphics;
        SpriteBatch spriteBatch;

        // Constructor
        public Game1()
        {
            graphics = new GraphicsDeviceManager(this);
            Content.RootDirectory = "Content";
        }
```
- In het deel hierboven wordt de class `Game1` gedeclareerd. Wanneer je een nieuw project maakt, dan zal dat project steeds een class bevatten met de naam `Game1` en de class `Game` als base class (volgens het principe van overerving). 

- De class bevat alvast twee objecten die gebruikt worden voor het grafisch aspect van het game. In de volgende hoofdstukken zal je deze objecten gebruiken, maar hier vind je alvast een korte omschrijving van hun functie: 

    - Het object __graphics__ is een object van de `GraphicsDeviceManager` class. Deze class bevat properties, methods, ... i.v.m. het beheer van het graphic device. Voorbeelden hiervan zijn hoogte en breedte van het game window, indicatie van fullscreen mode, ... 

    - Het object spriteBatch is een object van de `SpriteBatch` class. Via dit object kunnen `Sprites` op het scherm getekend worden. Een `Sprite` is een 2D-element dat gebruikt wordt om een figuur op het scherm te tonen.

- Verder is er nog de constructor van je class die alvast het volgende doet:

    - De objecten graphics en spriteBatch worden geïnitialiseerd. 
    - Er wordt aangegeven in welke folder de content van het project zich bevindt. Even opfrissen: de content van een project zijn bijvoorbeeld afbeeldingen, geluiden, e.d. Dit is dus de directory waar je later je afbeeldingen, e.d. in plaatst.

### De functie Initialize()

```csharp
        protected override void Initialize()
        {
            base.Initialize();
        }
```

In de functie initialize voeg je later code toe die geïnitialiseerd moet worden. Deze functie wordt eenmalig uitgevoerd na het uitvoeren van de constructor, maar voor het starten van de game loop. Je zal hier niet-grafisch gerelateerde content laden zoals bijvoorbeeld het starten van een netwerkverbinding.

### De functie LoadContent()

```csharp
        protected override void LoadContent()
        {
            spriteBatch = new SpriteBatch(GraphicsDevice);
        }
```

`LoadContent()` is de functie waarin je de content van je game laadt. In de vorige functie ging het om het initialiseren van netwerkverbindingen of databases. Hier gaat het om het laden van afbeeldingen en geluid. De functie wordt eenmalig uitgevoerd na de Initialize functie, maar voor de game loop.

Het object spriteBatch dat bovenaan de class reeds voorzien werd, wordt hier gemaakt. Het object spriteBatch kan gebruikt worden om afbeeldingen op het scherm te tonen.

### De functie UnloadContent()

```csharp
        protected override void UnloadContent()
        {
        }
```
`UnloadContent()` dient om content terug uit het geheugen te verwijderen. Als je slechts 1 game class hebt, dan is dat bijna nooit nodig. Grote games bestaan dikwijls uit verschillende stages. Zoals een intro, lobby waar je naar andere players zoekt, en de game zelf. In dat geval is het dikwijls goed dat je geheugen vrij maakt voor dat je naar de volgende stage gaat.

### De functie Update()

```csharp
        protected override void Update(GameTime gameTime)
        {
            if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed || Keyboard.GetState().IsKeyDown(Keys.Escape))
                Exit();

            base.Update(gameTime);
        }
```
De `Update` functie is de eerste functie van de game loop en zal dus afwisselend met de `Draw` functie uitgevoerd worden zolang het game loop. 

In de `Update()` functie wordt alvast gecontroleerd of de escape key ingedrukt werd (of de knop back op een gamepad). Als dat zo is dan wordt het game beëindigd d.m.v. `Exit()`. 

Je ziet dat de functie ook een argument heeft: `gameTime`. Daar gaan we later verder op in.

### De functie Draw()

```csharp
        protected override void Draw(GameTime gameTime)
        {
            GraphicsDevice.Clear(Color.Black);
            base.Draw(gameTime);
        }
    }
}
```
Tot slot is er de `Draw()` functie, die alle objecten op het scherm tekent. De eerste regel (`Clear`) maakt het scherm leeg. Daarbij moet je aangeven in welke kleur dat dat moet gebeuren. Die kleur is dus meteen de achtergrond van je nieuwe scherm. Net zoals bij Initialize en Update moet je hier op het eind van de functie ook de gelijknamige functie van de base class oproepen.

## Een eerste voorbeeld: een afbeelding tonen

MonoGame laat je afbeeldingen op het scherm tonen. In dit voorbeeld wordt getoond hoe je de afbeelding eerst toevoegt aan de `Content` van je project, hoe je ze in een `Texture2D` object laadt en hoe je dit object toont in het game window.

We werken het voorbeeld in 3 stappen uit:
- Stap1: Een afbeelding toevoegen aan de Content van je project.
- Stap 2: Uitwerken van een class Player met de nodige functionaliteiten om Texture2D objecten vlot op het scherm te kunnen tonen.
- Stap 3: Een object van de class Player gebruiken in de Game1 class.


### Stap 1: Een afbeelding toevoegen aan de Content van je project

Items die je in je game kan gebruiken, laad je in de `Content`. Dit kan je vergelijken met een 'verzameling' van afbeeldingen, geluid, fonts, ... waaruit je kan kiezen bij de opbouw van je game.

Je voegt iets toe aan de `Content` door de __MonoGame Pipeline tool__ te openen. Je opent daarvoor de folder `Content` in je project en klikt op `Content.mgcb`. Indien de Pipeline tool dan niet opent, kan je rechts klikken en `Open With MonoGame Pipeline Tool` kiezen uit het snelmenu.

Kies in de toolbar voor `Add Existing Item` en voeg een afbeelding toe. Voor het beste resultaat gebruik je afbeeldingen met een transparente achtergrond, die niet al te groot zijn. Een afbeelding voor een avatar is bijvoorbeeld zelden groter dan 512x512 pixels. Wanneer je afbeelding te groot is, dan moet je programma de afbeelding voortdurend schalen. Dat maakt je programma trager. Ook neemt een grote afbeelding veel meer geheugen in beslag.

Als je een afbeelding gekozen hebt, dan kies je voor `Copy the file to the directory`. Merk op dat je de afbeelding (met heel wat extra informatie) ziet verschijnen in het gedeelte `Content`. Je afbeelding zit nu in de `Content`. Je kan de Pipeline tool nu sluiten.

### Stap 2: Uitwerken van de Player class

In Monogame kan je via het `Texture2D` gegevenstype met afbeeldingen werken. Je maakt een object van dit type, via de `ContentManager` haal je de gewenste afbeelding uit de `Content` van je project en je laadt deze afbeelding in het `Texture2D` object.

Opmerking: De `ContentManager` class doet wat zijn naam aangeeft: het beheren van de Content van je game. Deze class is voorzien in Monogame. Om in je programma van deze `ContentManager` class gebruik te kunnen maken moet je bovenaan een extra namespace laden, namelijk `Microsoft.Xna.Framework.Content;`.

Voeg aan je project een nieuwe class `Player` toe en voorzie onderstaande code.

```csharp
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Content;  // De extra namespace om met de
                                        // ContentManager class te kunnen werken.

namespace MyGame
{
    class Player
    {
        private Texture2D texture; //Texture2D object

        //Constructor
        public Player(ContentManager contentManager) //ContentManager van game class
        {                                            //wordt als argument doorgegeven.
            //texture wordt a.h.v. de contentManager geïnitialiseerd met de afbeelding.
            texture = contentManager.Load<Texture2D>("balloon");
        }

        //Functie om het Player object te tekenen
        public void Draw(SpriteBatch spriteBatch) //SpriteBatch van game class wordt
        {                                         //als argument doorgegeven.
            //Het tekenen van de texture gebeurt door de Draw functie van de SpriteBatch class.
            spriteBatch.Draw(texture, new Rectangle(new Point(200,200), new Point(100, 100)), Color.White);
        }
    }
}
```

Verklaring van de onderdelen:

__Onderdeel 1: Declaratie van het Texture2D object waarin we de afbeelding zullen laden__

```csharp
private Texture2D texture; 
```

De class `Player` heeft een property van het type `Texture2D`. Hierin komt de afbeelding die het Player object zal voorstellen in het game window.

__Onderdeel 2: De constructor__

```csharp
public Player(ContentManager contentManager)
{
    texture = contentManager.Load<Texture2D>("balloon");
}
```

Via de constructor laden we de afbeelding in het `Texture2D` object. Zoals reeds aangehaald werd in dit hoofdstuk, hebben we een `ContentManager` nodig om de beschikbare content te laden. Herinner dat we daarnet onze afbeelding via de Pipeline Tool in de content geladen hebben, we moeten deze nu terug aanspreken via de `ContentManager`. Onze class `Player` heeft geen contentManager, maar de `Game` class heeft die wel. We zorgen dus dat we die `ContentManager` kunnen doorgeven via de constructor. We doen dit door de constructor een argument van het type `ContentManager` te geven. Via dit argument heeft de constructor van de `Player` class dus wel een `ContentManager` beschikbaar.

Opm.: Om gebruik te kunnen maken van `ContentManager` voegen we bovenaan een extra namespace toe: 

`using Microsoft.Xna.Framework.Content`.

__Onderdeel 3: De functie Draw om het `Player` object te tekenen__

```csharp
public void Draw(SpriteBatch spriteBatch)
        {                                         
            spriteBatch.Draw(texture, new Rectangle(new Point(200,200), new Point(100, 100)), Color.White);
        }
```

We hebben ook een functie nodig om de player te tekenen. Dat is de Draw functie. Tekenen gebeurt via de `SpriteBatch` class, die de voorzieningen biedt om zaken op het scherm weer te geven. Aangezien `SpriteBatch` niet voorzien is in onze eigen `Player`class zullen we ook hier weer hetzelfde principe toepassen als bij de constructor en `ContentManager`. We geven de `Draw` functie van de `Player` class een functieargument van het type `SpriteBatch` en op die manier kunnen we binnen deze de `Draw` functie van de functionaliteiten van de `SpriteBatch` class gebruik maken.

De functionaliteit van de `SpriteBatch` class die we in de `Draw` functie van `Player` zullen gebruiken is de method `Draw`. Via de `Draw` method van `SpriteBatch` geven we door wat er getekend moet worden, en waar. Let erop dat je goed het verschil inziet tussen de `Draw` functie van `Player` en de method `Draw` van de `SpriteBatch` class.

Welke argumenten heeft de method `Draw` van de `SpriteBatch` class nodig (je vindt deze tussen de ronde haakjes)? 
- We geven eerst de texture property door. Aangezien deze reeds door de constructor geïnitialiseerd is op een afbeelding, wordt er op deze manier aangegeven welke afbeelding getoond moet worden. 
- Daarna volgt er een rechthoek. Deze rechthoek bepaalt waar de afbeelding geplaatst moet worden en hoe groot de afbeelding getoond moet worden. Het eerste punt dat bij de `new Rectangle` meegegeven wordt, is de linkerbovenhoek van de rechthoek, en bepaalt hoe ver die van de linkerbovenhoek van het scherm staat (aantal pixels van de linkerrand en van de bovenrand). Het tweede punt is de grootte van de rechthoek (in het voorbeeld 100 pixels op 100 pixels groot). Indien de gekozen afbeelding niet in de rechthoek past, zal deze geschaald worden zodat ze passend is (te vermijden want dit vraagt resources).
- Als laatste geven we een kleur mee. De kleur is normaal gezien wit, wat betekent dat je de afbeelding gewoon toont zoals ze is. 

### Stap 3: Een object van de class Player gebruiken in de Game1 class

Nu we de Player class uitgewerkt hebben, kunnen we een Player object aan het game toevoegen. We doen dit door in de `Game1` class een object te maken van de class `Player`. Die voeg je bovenaan in de class toe, bij de andere definities:

```csharp
    GraphicsDeviceManager graphics;
    SpriteBatch spriteBatch;
    Player player; // deze regel voeg je toe
```

In de functie `LoadContent()` van de class `Game1` maak je je object. Door __new Player__ wordt de constructor uit de class `Player` opgeroepen. Het Player object wordt gemaakt en door de constructor geladen met de voorziene content (in ons voorbeeld: de figuur die in de constructor vermeld staat).

```csharp
protected override void LoadContent()
{
    // Create a new SpriteBatch, which can be used to draw textures.
    spriteBatch = new SpriteBatch(GraphicsDevice);

    // TODO: use this.Content to load your game content here
    player = new Player(this.Content); //De voorziene content wordt in 
                                      //het player object geladen.
                                      //De content (balloon) is in de constructor gedefiniëerd.
}                                       
```                                     

Tot slot teken je je player in de `Draw` functie van de class `Game1`. Alle sprites dienen getekend te worden tussen `spriteBatch.Begin()` en `spriteBatch.End()`. We geven de `spriteBatch` door aan de `Draw` functie van `Player`. 

```csharp
protected override void Draw(GameTime gameTime)
{
    GraphicsDevice.Clear(Color.CornflowerBlue);

    // TODO: Add your drawing code here
    spriteBatch.Begin();
    player.Draw(spriteBatch);
    spriteBatch.End();

    base.Draw(gameTime);
}
```

## Oefeningen

__Oefening 1__

Neem even de tijd om te experimenteren met de kleur, positie en schaal van je afbeelding. Wat gebeurt er wanneer je een andere kleur kiest? Hoe groot is je scherm? Wat als je de schaal(tweede punt van de rechthoek) een negatieve waarde geeft? En wat als je enkel de x of y waarde negatief maakt?

__Oefening 2__ 

Zorg dat een Player object een extra property met de naam position heeft. Voor een positie in het game window wordt het gegevenstype Point gebruikt. Pas de constructor aan zodat deze property geïnitialiseerd wordt op een meegegeven argument.
Om het Player object op de correcte position te tekenen, is het ook nodig om de Draw functie aan te passen. We starten nu niet meer vanaf een vast punt, zoals in de cursus, maar we plaatsen de linkerbovenhoek op de position property. 
De Draw functie passen we dus als volgt aan:

```csharp
spriteBatch.Draw(texture, new Rectangle(position, new Point(100, 100)), Color.White);
```

Als dit gebeurd is, kan kan je ook de positie van de player ingeven in je game. In je game (LoadContent functie van game1.cs) kan je nu dit gebruiken:

```csharp
player = new Player(this.Content, new Point(100, 100));
```

De Player wordt niet enkel met de voorziene content (de afbeelding) geladen, maar er wordt nu ook en variabele startpositie meegegeven.

__Oefening 3__

Een game waarin niets beweegt is maar niets. Je kan de `Player` class een Update functie geven. Deze Update functie test of er een toets op het keyboard ingedrukt werd. Via `IsKeyDown(Keys.Right)` wordt er getest of het rechterpijltje ingedrukt werd. Indien dit het geval is, wordt de X-coördinaat van de position property van het Player object met 1 verhoogd. Merk op hoe deze coördinaat aangesproken wordt: `position.X`.
Opmerking: om deze status van de toetsen van het keyboard te kunnen detecteren, is het nodig om een extra namespace te includen. Voeg bovenaan bij het gedeelte `using...` de volgende lijn toe:

```csharp
using Microsoft.Xna.Framework.Input;
```

De functie Update waarin de code voor het rechtse pijltje voorzien is, ziet er als volgt uit:

```csharp
public void Update()
{
    if (Keyboard.GetState().IsKeyDown(Keys.Right)) position.X++; 
}
```
Plaats deze functie Update in de Player class en voeg aan de functie de nodige instructies toe zodat ook de andere pijltjestoetsen voorzien worden en je figuur in de vier richtingen verplaatst kan worden d.m.v. de pijltjes.
Zorg er dan voor dat deze functie uitgevoerd wordt in de `Update` functie van je game (in game1.cs).


