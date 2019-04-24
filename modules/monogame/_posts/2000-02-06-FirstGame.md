---
title: Your First Game
---

Met alles wat we nu kennen zijn we zo ongeveer klaar om een kleine game te maken. Er komen nog een paar kleine nieuwigheden aan te pas, en die worden in dit hoofdstuk uitgelegd. Het spel is eenvoudig: je vangt zoveel mogelijk koeien op het scherm. Wanneer er meer dan 5 koeien vrij rondlopen, dan is het spel gedaan. Voor elke gevangen koe krijg je een punt.

Om te beginnen met dit hoofstuk open je dezelfde oefening als voorheen via github. Maar deze keer kies je voor de branch `EndGame`. Een aantal classes zijn al voorzien in deze oefening. De support classes (Camera, Enums, Font en Texture) zijn gelijk aan die van de voorgaande oefeningen, dus die kan je gewoon gebruiken.

# Al Klaar

## GameState
De class `Game1` is nu een stuk ingekort. Alle game logic is verdwenen. Dat zit zo: bij een echte game heb je nogal wat variabelen nodig om alles te doen werken. De player, enemies, een score etc. Maar in `Game1` staat ook al een hoop code om de game te initialiseren. We maken nu een onderscheid tussen:

- Code die nodig is om de game te starten. Dit gaat over algemene zaken die in elke game nodig zijn, zoals de `SpriteBatch`, `ContentManager` enzovoort. Dat soort code laten we in `Game1` staan.
- Code die eigen is aan deze game, zoals de player, enemies, score enzovoort. Die verplaatsen naar een nieuw class `GameState`.

Naast de zaken die verdwenen zijn, komt er een beetje nieuwe code bij: het `GameState` waar we de nieuwe code in onderbrengen roepen we aan vanuit de class `Game1`. Kijk even de code na. Je vindt er de declaratie van een object `gameState`, de constructie van dat object, een aanroep van de `Update` functie en een aanroep van de `Draw` functie.

### Oefening
- Waar in de code vind je deze aanroepen?
- Verklaar voor elk van deze aanroepen waarom ze staan waar ze staan.

## GameTime
De class `Cow` is bijna gelijk aan de vorige oefening. Maar we gebruiken nu in de `Update` functie nu een argument `GameTime`. Dit is nieuw. `GameTime` bestaat uit twee delen:
- TotalGameTime: dit is een object dat je laat weten hoeveel tijd er voorbij ging sinds het starten van je game.
- ElapsedGameTime: dit object laat je weten hoeveel tijd er voorbij ging sinds de vorige update. Aangenomen dat je ongeveer 60 frames per seconde haalt, zal de `ElapsedGameTime` gemiddeld 16.6 seconden zijn.

Die `ElapsedGameTime` zullen we vaak gebruiken. Daarmee kunnen we er voor zorgen dat je game altijd even snel werkt. Stel je even het volgende voor. In een game moet een object bij elke update naar rechts opschuiven. Je zou dat zo kunnen oplossen:

```csharp
position += 0.1;
```
Bij 60FPS zal je positie na 1 seconde verhoogd zijn met 6. Het probleem onstaat echter wanneer je je spel op een trage computer speelt, want dan speel je misschien aan 30FPS. In dat geval zou je positie na 1 seconde slechts verhoogd zijn met 3. Als dit de positie is van een object dat je moet ontwijken, dan heeft die speler een flink voordeel!

De oplossing bestaat erin om het aantal seconden dat verstreken is sinds de vorige update, te betrekken in je berekening. Dat doen we zo:

```csharp
position += speed * (float)gameTime.ElapsedGameTime.TotalSeconds;
```

Het aantal seconden dat verstreken is bij 60FPS zal ongeveer 0.016 zijn. Maar bij 30FPS is dat 0.032 seconden. Er zijn dus minder updates per seconde, maar de verplaatsing per update wordt nu dubbel zo groot. Op die manier geven we de speler met een trage computer geen voordeel.

In deze class is de verplaatsing geen float `speed`, maar een `Vector2 direction`. Maar ook vectoren kunnen we vermenigvuldigen met floats, dus het resultaat blijft hetzelfde.
```csharp
Position += direction * (float)gameTime.ElapsedGameTime.TotalSeconds;
```

### Oefening
- Hoe zou je de snelheid van een koe aanpassen?

## Player
De class `Player` is nieuw in deze oefening. De player is echter niets meer dan een tekening op het scherm, met de mogelijkheid om die te verplaatsen via de pijltjestoetsen. Wanneer je deze class bekijkt, dan zie je dat we de texture class als basis gebruiken. We kunnen gewoon de naam van de texture meegeven, samen met de positie en de schaal. We voegen een update functie toe waarin we de positie aanpassen via de pijltjestoetsen. Ook hier gebruiken we de gameTime om de snelheid te bepalen. 

### Oefening
- bekijk de manier waarop we de snelheid van de verplaatsing berekenen. Hoeveel tijd heeft een speler nodig om de andere kant van het scherm te bereiken?
- kan je nu al zien of de speler sneller of langzamer dan de koe zal bewegen?
- De laatste vier regels van de update functie zijn ook nieuw. Leg uit waar die voor dienen.

# De GameState

De class die je in deze oefening nog moet implementeren is `GameState`. Daarin bouwen we stap voor stap de werking van de game op.

## Player

We beginnen met de  `Player`. We moeten van deze class een object maken, updaten en op het scherm tonen. Dan kan zo:

```csharp
class GameState
{
    // the hero
    Player player;

    public GameState()
    {
        player = new Player(new Vector2(0.0f));
    }

    public void Update(GameTime gameTime)
    {
        player.Update(gameTime);
    }

    public void Draw(GameTime gameTime)
    {
        player.Draw();
    }
}
```

Test je game uit en controleer of de Player werkt zoals het hoort.

## Cows
Eens je getest hebt of alles werkt, kan je de koeien toevoegen. Dat doen we via een list. Ook hier moeten we de Update en Draw functies voorzien. Ook willen we elke twee seconden een nieuwe koe toevoegen. Dat doen we via een extra variable. We moeten onthouden hoeveel tijd er verstreken is sinds we voor het laatst een nieuwe koe toevoegden.

```csharp
class GameState
{
    // the hero
    Player player;

    // the cows
    List<Cow> cows = new List<Cow>();
    float timeToNewCow;

    public GameState()
    {
        player = new Player(new Vector2(0.0f));

        // cows
        cows = new List<Cow>();
        timeToNewCow = 2.0f; // twee seconden tot nieuwe koe
    }

    public void Update(GameTime gameTime)
    {
        // verminder de wachttijd met de verstreken game tijd
        timeToNewCow -= (float)gameTime.ElapsedGameTime.TotalSeconds;
        // is het tijd voor een nieuwe koe?
        if (timeToNewCow <= 0)
        {
            // voeg koe toe, op een random positie
            cows.Add(new Cow(
                new Vector2(
                    -1 + (float)Game1.sRandom.NextDouble() * 2.0f,
                    -1 + (float)Game1.sRandom.NextDouble() * 2.0f
                ),
                0.1f
            ));
            // terug twee seconden tot een nieuwe koe
            timeToNewCow = 2;
        }

        // teken alle koeien op het scherm
        cows.ForEach(cow => cow.Update(gameTime));
        player.Update(gameTime);
    }

    public void Draw(GameTime gameTime)
    {
        cows.ForEach(cow => cow.Draw());
        player.Draw();
    }
}
```

De methode om een nieuwe koe toe te voegen kom je heel vaak tegen in een game. Zorg dus dat je weet hoe dit werkt. De stappen zijn altijd dezelfde:
- voorzie een `float` variabele waarin je het instelt hoeveel tijd er moet verstrijken voor de actie _(in dit geval het toevoegen van de nieuwe koe)_
- in de update functie verminder je deze waarde met de verstreken tijd in seconden.
- wanneer de waarde kleiner of gelijk aan nul is, dan voer je de actie uit en stel je de nieuwe wachttijd in. Dit kan een vaste waarde zijn, maar ook een random getal.

Voer opnieuw de game uit om te controleren of alles werkt.

### Koeien Vangen

Het is ook de bedoeling dat je koeien kan _vangen_. Dat doen we door te controleren of de speler een koe raakt. Als dat zo is, dan verwijderen we de koe uit de lijst. We gebruiken hier een omgekeerde `for`-lus. Wanneer je objecten wil verwijderen uit een lijst, dan hoor je een loop van achter naar voor te doen. Immers, op het moment dat je een element uit een lijst verwijderd, dan klopt de rest van de lijst niet meer. Loop je van achter naar voor, dan heb je de resterende elementen al gebruikt, dus dan maakt het niet uit.

Je voegt deze code toe onder in de `Update` functie:

```csharp
for (int i = cows.Count - 1; i >= 0; i--)
{
    if (cows[i].Collides(player))
    {
        cows.RemoveAt(i);
    }
}
```

##  De Score
Om de score bij te houden heb je een variabele nodig. Daarna is het ook handig om te weten of het spel al dan niet bezig is. We voorzien twee waarden in de `GameState`. 

```csharp
// the score
int score = 0;
bool gameOver = false;
```

In de `Update` functie zullen we nu eerst controleren of het spel wel bezig is. Indien niet, dan controleren we ook of de spatiebalk ingedrukt is om dan een nieuw spel te starten. Is het spel niet bezig, dan beeindigen we de functie. Tot slot zullen we ook controleren of er meer dan 5 koeien in het spel zijn. In dat geval ben je een slechte koeienvanger en is het spel gedaan.

```csharp
if (gameOver && Keyboard.GetState().IsKeyDown(Keys.Space))
{
    score = 0;
    cows.Clear();
    gameOver = false;
}

if (gameOver) return;

if (cows.Count > 5)
{
    gameOver = true;
}
```

Om te controleren of je score effectief werkt, tonen we die ook op het scherm. Ook in de draw functie is wat we tonen anders bij een gameOver. De Draw functie ziet er uiteindelijk zo uit:

```csharp
public void Draw(GameTime gameTime)
{
    if (gameOver)
    {
        Support.Font.PrintAt(new Vector2(0f, 0f), "Game Over", Color.Red);
        Support.Font.PrintAt(new Vector2(0f, -0.1f), "Score: " + score, Color.Red);
        return;
    }

    cows.ForEach(cow => cow.Draw());
    player.Draw();

    Support.Font.PrintStatus("Score: " + score, Color.Black);
}
```