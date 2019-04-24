---
title: Game Window
---

Of je nu een afbeelding gebruikt om de player te tonen, of particles om een explosie duidelijk te maken, een game heeft altijd graphics en effecten nodig. In dit hoofdstuk bekijken we een aantal bouwstenen die je nodig hebt om die afbeeldingen goed te gebruiken.

# Game Window

Het eerste waar het over moeten hebben is het game window. Er zijn twee manieren om je game te tonen. In _windowed_ mode kies je een specifieke resolutie voor je window, en zie je je game als een _window_, net zoals andere progamma's. Daarnaast is er ook de _Full-screen_ mode die je hele scherm inneemt. Hier leer je hoe je wisselt tussen deze twee modes.

1. Maak een nieuw project met de naam GameWindowSize.
2. In de Game1 class declareer je de variabelen windowWidth en windowHeight:

    ```csharp
    public class Game1 : Game {
        GraphicsDeviceManager graphics;
        SpriteBatch spriteBatch;

        int windowWidth = 1000;
        int windowHeight = 800;
    ```

3. Nu kan je deze waarden gebruiken in de constructor. Daarmee stel je de beginwaarden voor de hoogte en breedte van je game in.

    ```csharp
    graphics = new GraphicsDeviceManager(this);
    graphics.PreferredBackBufferWidth = windowWidth;
    graphics.PreferredBackBufferHeight = windowHeight;
    ```
4. Nu kan je in de update functie kijken of er een toets ingedrukt wordt en zo wisselen tussen twee modi. Denk er wel aan dat je deze wijzigingen ook moet toepassen met _ApplyChanges()_. Hierboven was dat niet nodig omdat de game nog niet gestart was.

    ```csharp
    if(Keyboard.GetState().IsKeyDown(Keys.K) && !graphics.IsFullScreen)
    {
        graphics.PreferredBackBufferWidth = 1920;
        graphics.PreferredBackBufferHeight = 1080;
        graphics.IsFullScreen = true;
        graphics.ApplyChanges();
    }

    if(Keyboard.GetState().IsKeyDown(Keys.L) && graphics.IsFullScreen)
    {
        graphics.PreferredBackBufferWidth = windowWidth;
        graphics.PreferredBackBufferHeight = windowHeight;
        graphics.IsFullScreen = false;
        graphics.ApplyChanges();
    }
    ```

## Oefeningen
1. Gebruik ook eens andere waarden voor een windowed game.
2. Wat gebeurt er wanneer je de schermverhoudingen niet wijzigt en overschakelt naar fullscreen?
3. Wat gebeurt er wanneer je _ApplyChanges_ vergeet?
4. Hoe kan je met een enkele toets (F12) wisselen tussen de twee modi?

