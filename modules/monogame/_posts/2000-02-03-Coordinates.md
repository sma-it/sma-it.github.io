---
title: Coordinates
---


# Coordinate System

In het vorige deel leerde je textures op het scherm zetten. Maar je kon ook zien dat er een probleem is: de positie van de textures wijzigt niet met de grootte van je window. Ook zou de y-as beter omgekeerd werken en kunnen we objecten beter schalen met de positie in het centrum. Dat komt allemaal omdat we de default _pixel space_ gebruiken.

Die _pixel space_ is de meest primitieve manier om met coordinaten om te gaan. Omdat niet elk coordinaten systeem het meest geschikt is voor eender welke game, gebruikt monogame de _pixel space_. Het is aan jou om daar op verder te bouwen. In dit voorbeeld stellen we vier eisen:
- De y-as moet omgekeerd werken.
- De coordinaten mogen niet afhankelijk zijn van het aantal pixels.
- Het midden van het scherm wordt het nulpunt.
- De hoogte van het scherm schalen we tussen -1 en 1. De breedte is dan afhankelijk van de hoogte.

Dat laatste punt zorgt er voor dat we de Textures nu met veel kleinere afmetingen moeten maken.  We zullen dus eerst het laden van de textures aanpassen:

```csharp
Textures.Add(new Support.Texture("balloon", new Vector2(0, 0), new Vector2(0.3f, 0.3f)));
Textures.Add(new Support.Texture("balloon", new Vector2(-0.5f, -0.5f), new Vector2(0.3f, 0.3f)));
Textures.Add(new Support.Texture("balloon", new Vector2(0.7f, 0.7f), new Vector2(0.1f, 0.1f)));
Textures.Add(new Support.Texture("balloon", new Vector2(-0.5f, 0.5f), new Vector2(0.4f, 0.2f)));
```

## Camera class

Dan maken we in de `Support` folder een class `Camera`. Omdat we altijd slechts 1 camera willen, wordt dit een static class. De class heeft twee variabelen nodig:
- sScale wordt de schaal. Die hebben we nodig om Coordinaten tussen -1 en 1 om te zetten naar pixel coordinaten.
- sOffset hebben we nodig omdat het nulpunt niet langer linksboven ligt. We moeten alle schermcoordinaten verplaatsen naar het eigenlijke nulpunt.

```csharp
static public class Camera
{
    static private float sScale;
    static private Point sOffset;
}
```

De eerste functie die we toevoegen zet een `Vector2` grootte om naar een `Point` pixel coordinaat. Deze functie gebruiken we niet voor posities, maar om de grootte _(size)_ van een `Rectangle` te converteren. De offset hebben we daarom niet nodig. 

```csharp
static private Point ConvertToSize(Vector2 value)
{
    Point point = new Point();
    point.X = (int)(value.X * sScale);
    point.Y = (int)(value.Y * sScale);
    return point;
}
```

Daarnaast hebben we ook een functie nodig om een echte schermpositie te berekenen. Hier heb je wel een offset nodig. Ook moeten we hier de `Y` waarde omkeren omdat we die van beneden naar boven willen.

```csharp
static private Point ConvertToPosition(Vector2 value)
{
    Point point = new Point();
    point.X = (int)(value.X * sScale);
    point.Y = (int)(-value.Y * sScale);
    return sOffset + point;
}
```

Dan volgt de publieke functie die we buiten de class zullen aanroepen `ScreenRectangle`. Die zet een positie en een schaling om naar een rechthoek in _pixel space_. Om de positie samen te laten vallen met het midden van de rechthoek in plaats van de linkerbovenhoek, trekken we de helft van de schaal af van de positie.

```csharp
static public Rectangle ScreenRectangle(Vector2 position, Vector2 size)
{
    Point p = ConvertToPosition(position);
    Point s = ConvertToSize(size);

    return new Rectangle(p - new Point(s.X / 2, s.Y / 2), s);
}
```

Tot slot schrijven we een `Setup` functie. Telkens als we de resolutie van het window wijzigen _(of overschakelen naar fullscreen)_ moeten we de offset en de schaal berekenen.

```csharp
static public void Setup()
{
    sOffset.X = Game1.sGraphics.PreferredBackBufferWidth / 2;
    sOffset.Y = Game1.sGraphics.PreferredBackBufferHeight / 2;
    sScale = sOffset.Y;
}
```

De bovenstaande functie moet je dan in de class `Game1` uitvoeren. Dit doe je op het eind de `Initialize` functie:

```csharp
protected override void Initialize()
{
    base.Initialize();
    Support.Camera.Setup();
}
```

## Texture
We begonnen met de `Textures` andere coordinaten te geven. De laatste stap bestaat er nu in om die coordinaten om te zetten naar de _pixel space_. Dat doen we pas op het laatste moment, net voordat we de rechthoek tekenen. De `Draw` functie van de  `Texture` class kan je zo aanpassen:

```csharp
public void Draw()
{
    Rectangle destRect = Camera.ScreenRectangle(position, size);
    Game1.sSpriteBatch.Draw(image, destRect, Color.White);
}
```

## Oefeningen
1. Voeg een object helemaal boven in het midden van het scherm toe.
2. Voeg een object helemaal beneden, rechts in het scherm toe. _(Blijf dit even oefenen totdat je intuitief weet wat voor waarden je nodig hebt voor verschillende posities.)_
3. Voeg code toe om je Camera een zoomfunctie te geven. Je moet daarvoor een zoom delta doorgeven aan de `Camera` class. Een beetje zoals de functies in `Texture` waarmee je de positie en de schaal kan aanpassen. Ook zal je in `Game1` twee toetsen moeten gebruiken om de zoom groter en kleiner te maken.
4. Voeg ook code toe om de camera te bewegen.
5. Zorg er voor dat je via de `N` toets telkens een extra Texture toevoegt aan je game. Elke texture moet een Random positie en schaal hebben.