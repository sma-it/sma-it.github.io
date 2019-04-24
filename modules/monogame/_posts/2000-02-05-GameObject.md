---
title: Game Objects
---


# Game Objects
Tot hier toe gebruikte je de `Texture` class om afbeeldingen op het scherm te tonen. Maar niet elk object in je game zal zich op dezelfde manier gedragen. Daarom is het een goed idee om deze class als basis te gebruiken voor meer geavanceerde classes, die zelf bepalen hoe een object zich moet gedragen, maar de `Texture` class gebruiken voor de 'basics' die elk object nodig heeft, zoals de `Draw()` functie.

## Boundaries
Bijna altijd zal je in een game _boundaries_ willen gebruiken. Daarmee bedoelen we de grenzen van een object, of de grenzen van een scherm. Met boundaries kunnen we controleren of twee objecten mekaar raken, of een object de rand van het scherm raakt, of we met de muis in het object klikken enzovoort.

Eerst voegen we boundaries toe aan de `Texture` class. Dat kan met twee eenvoudige properties:

```csharp
public Vector2 MinBound { get => Position - (size * 0.5f); }
public Vector2 MaxBound { get => Position + (size * 0.5f); }
```

De boundaries van het scherm voegen we toe aan de `Camera` class. Afhankelijk van je game zou je hier ook rekening kunnen houden met de camera positie en zoom, maar dat doen we nu niet.

```csharp
static public Vector2 Min { get => new Vector2(-sOffset.X / sScale, -sOffset.Y / sScale); }
static public Vector2 Max { get => new Vector2(sOffset.X / sScale, sOffset.Y / sScale); }
```

Nu we boundaries hebben, willen we kunnen weten of een texture de rand van het scherm raakt. Daarvoor maken we eerst een `enum`. Je kan deze enum in een afzonderlijk bestand plaatsen, waarin je later ook andere enumeraties toevoegt.

```csharp
public enum CollisionStatus
{
    Top,
    Bottom,
    Left,
    Right,
    Inside,
}
```

Terug in de `Camera` class ga je tenslotte een functie toevoegen die controleert of een texture de rand van het scherm raakt:

```csharp
static public CollisionStatus GetCollision(Texture texture)
{
    if (texture.MaxBound.Y > Max.Y) return CollisionStatus.Top;
    if (texture.MinBound.X < Min.X) return CollisionStatus.Left;
    if (texture.MaxBound.X > Max.X) return CollisionStatus.Right;
    if (texture.MinBound.Y < Min.Y) return CollisionStatus.Bottom;

    return CollisionStatus.Inside;
}
```

## Game Object
We kunnen best een game object maken voor elke afbeelding die zich op een bepaalde manier gedraagt. Zo zou je game objects kunnen maken voor muren, bomen, de player, enemies...

In deze oefening gaan we voor koeien die over het scherm bewegen. De class die we maken heet dan ook `Cow`. Als je zelf een ander idee hebt, kan je de naam van de class natuurlijk aanpassen. Omdat elk game object op het scherm getoond wordt, zal je `Texture` als basis class gebruiken:

```csharp
public class Cow : Support.Texture 
{
    Vector2 direction;
}
```
Deze class heeft een variabele om de richting te onthouden waarin het object beweegt. In de constructor stellen we die richting in. We geven ook de juiste waarden door aan de basis class.

```csharp
public Cow(Vector2 position, float size) : base("Cow", position, new Vector2(size))
{
    direction.X = (float)(Game1.sRandom.NextDouble()) * 0.05f - 0.025f;
    direction.Y = (float)(Game1.sRandom.NextDouble()) * 0.05f - 0.025f;
}
```
Zoals je ziet geven we elk object een random richting. De code veronderstelt dat de class `Game1` een `Random` object bevat, zoals gevraagd in een van de vorige oefeningen. Als dat niet het geval is, of indien dat object niet static en public is, dan kan je dat nu nog aanpassen.

Verder heeft de class maar 1 functie nodig: `Update()`. Daarin bereken we de nieuwe positie van het object. Dat gebeurt door de richting bij de positie te tellen. Maar eerst gaan we wel controleren of we de rand van het scherm raken. In dat geval keren we de richting om.

```csharp
public void Update()
{
    var status = Support.Camera.GetCollision(this);
    switch (status)
    {
        case Support.CollisionStatus.Bottom:
        case Support.CollisionStatus.Top:
            direction.Y *= -1;
            break;
        case Support.CollisionStatus.Left:
        case Support.CollisionStatus.Right:
            direction.X *= -1;
            break;
    }
    Position += direction;
}
```

## Cows. Plural
De `Cow` class is klaar, maar wordt nog niet gebruikt in het programma. Daarom zullen we een `List<Cow>` object toevoegen. We starten met 1 koe op het scherm, maar via de spatiebalk kunnen we er meer toevoegen. En dat gebeurt allemaal in de class `Game1`.

Eerst zorg je voor een container om al die koeien in op te slaan. Die maken we rechtstreeks in de class, net zoals de variabelen die er al staan:

```csharp
List<Cow> Cows = new List<Cow>();
```

In de functie `LoadContent()` kan je alvast een koe toevoegen bij de start van het programma:

```csharp
Cows.Add(new Cow(new Vector2(0, 0), 0.3f));
```

In de `Update()` functie dienen er twee zaken te gebeuren: 
1. Wanneer je op de spatiebalk drukt, dan moet er een nieuwe koe toegevoegd worden.
2. Elke koe moet een update krijgen, via zijn eigen update functie.

```csharp
if(Keyboard.GetState().IsKeyDown(Keys.Space))
{
    Cows.Add(new Cow(new Vector2(0, 0), 0.3f));
}
Cows.ForEach((cow) => cow.Update());
```

Tot slot teken je alle koeien op het scherm in de `Draw()` functie, net na `sSpriteBatch.Begin()`. De class `Cow` heeft zelf geen `Draw()` functie, maar gebruikt de functie die in de Texture class aanwezig is.

```csharp
Cows.ForEach(cow => cow.Draw());
```

##
- Toon de positie van de eerste koe op het scherm.
- Toon hoeveel koeien er op het scherm staan.
- Zorg er voor dat er nooit meer dan 1 koe bijkomt wanneer je op de spatiebalk drukt.
- Zorg er voor dat elke nieuwe koe start op een random positie.
- Maak nog een tweede game object: `Rat`. Rats starten ergens op het scherm en bewegen naar rechts. Wanneer ze helemaal rechts staan, dan verplaats je ze terug naar links. 
- Elke rat heeft een willekeurige grootte.
- Hoe bepaal je of koeien dan wel ratten op de voorgrond staan?
- _(Uitdaging)_ Hoe zorg je er voor dat alle koeien even snel bewegen?
