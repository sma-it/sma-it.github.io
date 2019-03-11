---
title: Wat is MonoGame?
---

#Libraries

Tot nu toe schreven we programma's die tekst tonen in een console. Dat is goed om de basics onder de knie te krijgen, maar uiteindelijk is dat meestal niet het soort programma dat je wil maken. C# is een programmeertaal die voor zowat alles bruikbaar is. Je kan er gewone windows desktop programma's mee maken, maar ook mobile apps, interactieve websites en games. Ook bestaat er het Mono project, dat je toelaat om C# code zo te compileren dat je programma ook op linux (en macOS) laat werken.

Al die toepassingen hebben extra code nodig. Tot hiertoe schreef je voortdurend text in een console window. Je gebruikte daarvoor functies zoals

```csharp
Console.Write("Enter your name: ");
var input = Console.ReadLine();
```

Nu bestaat een console eigenlijk uit niets anders dan pixels op een scherm. Die pixels vormen letters, er is een scrollbar morgelijk en je kan zelfs tekst invoeren (en dat zijn ook weer gewoon pixels). En toch hoef je je daar niets van aan te trekken. Via het `Console` object kan je gewoon tekst toevoegen en lezen, zonder dat je moet weten wat er op de achtergrond gebeurt.

De `Console` is aanwezig in de C# core (basis) library. Dat betekent dat je de console in elk programma kan gebruiken. Wanneer je een ander soort programma wil schrijven, zoals een windows desktop app, dan zal je meer nodig hebben dan een console. Je wil windows, buttons, labels, sliders en meer gebruiken. Maar die zitten niet in de core library! Je zal de library die je wil gebruiken moeten toevoegen aan je programma. Afhankelijk van de library die je wil gebruiken bestaan daar verschillende mogelijkheden voor.

_Later in deze cursus volgt een overzicht van al die mogelijkheden. Nu hebben we het enkel over MonoGame._

# Monogame

Als we een computer kopen, dan willen we daar vroeg of laat een spel op spelen. Dat weten ze bij microsoft ook. Maar omwille van alle interactiviteit is het ontwikkelen van games behoorlijk complex. En als je code dan slechts werkt voor een enkel soort computer, dan wordt het moeilijk om uit de kosten te komen. Daarom ontwikkelde Microsoft het Xna Framework. Met Xna kan je games maken die werken op Windows, Windows Phone en Xbox.

Ondertussen ins Windows Phone zo ongeveer dood en begraven. Dus blijven er nog twee platformen over. Wat eigenlijk niet zo veel is. Maar gelukkig is er MonoGame. Het Mono project is een open source project dat de belangrijkste C# libraries beschikbaar maakt voor linux en MacOS. MonoGame is daar een onderdeel van. Code die je schrijft voor Xna werkt dankzij MonoGame ook op Linux. Maar MonoGame gaat nog een stap verder. Je kan zonder veel moeite je game ook laten werken op Playstation, Switch en Android.

Natuurlijk zijn er nog andere Frameworks, naast MonoGame. Vooral 3D game engines zoals Unity en Unreal zijn tegenwoordig heel populair. Toch zijn die niet zo efficient als je een 2D game wil maken, omwille van alle 3D functionaliteit die aanwezig is zonder dat je er gebruik van maakt.

Ook zijn er nog 2D game engines die MonoGame gebruiken maar er tools rond bouwen die het eenvoudiger maken om samen te werken met graphic designers.

We kiezen in deze cursus voor MonoGame omdat de library eenvoudig te installeren is en werkt op low budget computers. Samenwerken met andere graphics designers is voorlopig nog niet aan de orde. De voordelen van meer gevanceerde engines zijn dus beperkt. Bovendien geeft MonoGame je een extra voordeel: zowat elke game engine gebruikt dezelfde basisprincipes, maar dikwijls werken die op de achtergrond zonder dat je er iets van merkt. MonoGame laat je rechtstreeks met deze basics werken. Dat geeft je een goed inzicht in de eigenlijke werking van een game. Mocht je je later specializeren in game development, dan komt deze kennis je zeker van pas. Welke game engine je dan ook nodig hebt, je weet al hoe die eigenlijk werkt.

Maar ook als game development uiteindelijk niet je ding blijkt, dan nog zal je veel leren door het gebruik van MonoGame. Bijvoorbeeld hoe je omgaat met libraries, online oplossingen zoekt voor algemene problemen en je programma structureert in classes die alles overzichtelijk houden.

_Beginnende programmeurs zijn dikwijls geneigd om te kiezen voor de meest uitgebreide game engine, met een goed ogende interface en spectaculaire demo's. Die zien er dan ook heel goed uit. Maar vergeet niet dat al die extra mogelijkheden ook extra complexiteit met zich meebrengen. Het voelt goed om de basics van je game met enkele mouse clicks te genereren. Maar dat is enkel het begin. Daarna is er nog heel veel code nodig die specifiek is voor jouw game. Dat soort code leer je beter schrijven in een eenvoudige omgeving._

# Installatie

Monogame installeren is behoorlijk eenvoudig. Je opent de website monogame.net, klikt op _getting started_, je kiest de laatste versie en download 'MonoGame for Visual Studio'. Eens je download klaar is, kan je het installatieprogramma uitvoeren. Waarschijnlijk krijg je dan een melding dat Windows dit programma niet kent. Je kiest dan voor 'advanced' en 'run anyway'.

# Je Eerste Project

## Een MonoGame app maken

## De code lezen

Wanneer je een nieuw MonoGame project maakt, dan start je met twee bestanden waarin je al C# code vindt. Het eerste bestand is `Program.cs`. Daarin wordt het eigenlijke programma gestart. De code die dat doet is deze:

```csharp
static void Main()
{
  using (var game = new Game1())
    game.Run();
}
```

De code hierboven maakt een object van de de class `Game1` en voert dan de `Run()` functie van die class uit. De naam `Game1` is afhankelijk van de naam van je project. Als je een project maakte met de naam `SpaceInvaders` dan zal dat ook de naam van de class zijn.

Het tweede bestand heeft de naam van je project. Bijvoorbeeld `Game1.cs` of `SpaceInvaders.cs`. Dit bestand is het echte vertrekpunt voor je game. Het is belangrijk dat je weet wat er in dit bestand gebeurt.

Zowel elke game engine werkt op dezelfde manier. De `Run()` functie uit het eerst bestand zal eerst de game engine initialiseren. Daarna wordt de content van je game geladen. Dit zijn bijvoorbeeld afbeeldingen, geluiden en andere bestanden zoals game levels en dergelijke.

Nu komt het belangrijkste deel: de game loop. Die bestaat uit twee delen: `Update` en `Draw`. Je programma zal voortdurend deze twee delen afwisselen. In `Update` hoor je alle berekeningen te doen, zoals aanpassen van posities, controlleren of een toets ingedrukt werd, reageren op een mouse click etc. Ook informatie die via het netwerk binnenkomt kan hier verwerkt worden. In `Draw` wordt al die informatie gebruikt om objecten op het scherm te tekenen.

Tot slot is er nog een functie om de geladen content terug vrij te geven. Die wordt uitgevoerd wanneer je het programma sluit.

_Meestal zullen `Update` en `Draw` mekaar gewoon afwisselen. Maar het kan gebeuren dat je computer te traag blijkt, bijvoorbeeld omdat er andere programma's op de achtergrond plots veel werk hebben. In dat geval kan de game engine beslissen om een aantal `Draw` instructies over te slaan. Update wordt dan wel uitgevoerd, zodat de berekeningen accuraat blijven. Er zijn gewoon minder screen updates. Daarom is het belangrijk dat je het onderscheid maakt tussen deze twee functies. Ook al kan je in theorie positie updates en dergelijke ook in de `Draw` functie uitvoeren, het is een heel slecht idee om dat te doen._

We overlopen hier de code die een leeg programma bevat. 

```csharp
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
```
In dit eerste deel wordt MonoGame geladen. Het lijkt alsof het niet MonoGame, maar Xna Framework is dat geladen wordt. Dat komt omdat MonoGame een volledige vervanging is van Xna Framework. Je kan dus ook Xna installeren in plaats van MonoGame en je programma compileren zonder dat je iets moet aanpassen. Maar dan werkt het wel enkel met Windows.

```csharp
namespace Game1
{
    public class Game1 : Game
    {
        GraphicsDeviceManager graphics;
        SpriteBatch spriteBatch;

        public Game1()
        {
            graphics = new GraphicsDeviceManager(this);
            Content.RootDirectory = "Content";
        }
```
In het deel hierboven wordt de class `Game1` gedeclareerd. Wanneer je een nieuw project maakt, dan zal dat project steeds een class bevatten met de naam van je project, met de class `Game` als base class. De class bevat alvast twee objecten: `GraphicsDeviceManager` en `SpriteBatch`. Daarover leer je later meer. En dan is er nog de constructor van je class. Daarin initialiseer je de objecten van de class. Je geeft er ook aan in welke folder de content van je project zicht bevindt. Dit is de directory waar je later je afbeeldingen plaatst.

```csharp
        protected override void Initialize()
        {
            base.Initialize();
        }
```

In de functie initialize voeg je later code toe die geinitialiseerd moet worden. Je zal hier bijvoorbeeld een netwerkverbinding starten.

```csharp
        protected override void LoadContent()
        {
            spriteBatch = new SpriteBatch(GraphicsDevice);
        }
```

`LoadContent()` is de functie waarin je de inhoud van je game laadt. In de vorige functie ging het om het initialiseren van netwerkverbindingen of databases. Hier gaat het om het laden van afbeeldingen en geluid.

```csharp
        protected override void UnloadContent()
        {
        }
```
`UnloadContent()` dient om content terug uit het geheugen te verwijderen. Als je slechts 1 game class hebt, dan is dat bijna nooit nodig. Grote games bestaan dikwijls uit verschillende stages. Zoals een intro, lobby waar je naar andere players zoekt, en de game zelf. In dat geval is het dikwijls goed dat je geheugen vrij maakt voor dat je naar de volgende stage gaat.

```csharp
        protected override void Update(GameTime gameTime)
        {
            if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed || Keyboard.GetState().IsKeyDown(Keys.Escape))
                Exit();

            base.Update(gameTime);
        }
```
In de `Update()` functie wordt alvast gecontroleerd of de escape key ingedrukt werd. Als dat zo is dan beeindig je de game. Je ziet dat de functie ook een argument heeft: `gameTime`. Daar gaan we later verder op in.

```csharp
        protected override void Draw(GameTime gameTime)
        {
            GraphicsDevice.Clear(Color.Black);
            base.Draw(gameTime);
        }
    }
}
```
Tot slot is er de `Draw()` functie, die alle objecten op het scherm tekent. De eerste regel (`Clear`) maakt het scherm leeg. Daarbij moet je aangeven in welke kleur dat dat moet gebeuren. Die kleur is dus metteen de achtergrond van je nieuwe scherm. Net zoals bij Initialize en Update moet je hier op het eind van de functie ook de gelijknamige functie van de base class oproepen.
