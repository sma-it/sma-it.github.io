---
title: Game Window
---

Of je nu een afbeelding gebruikt om de player te tonen, of particles om een explosie duidelijk te maken, een game heeft altijd graphics en effecten nodig. In dit hoofdstuk bekijken we een aantal bouwstenen die je nodig hebt om die afbeeldingen goed te gebruiken.

# Game Window

Het eerste wat we bespreken is het game window. Er zijn twee manieren om je game te tonen:
- In _Windowed_ mode kies je een specifieke resolutie voor je window, en zie je je game als een _window_, net zoals andere progamma's. - In _Full-screen_ mode neemt je game het hele scherm in. 

Hieronder leer je hoe je wisselt tussen deze twee modes.

1. Maak een nieuw project met de naam GameWindowSize.
2. In de Game1 class declareer je de __variabelen__ windowWidth en windowHeight. We initialiseren ze hier respectievelijk op 1000 en 800 pixels.

    ```csharp
    public class Game1 : Game {
        GraphicsDeviceManager graphics;
        SpriteBatch spriteBatch;

        int windowWidth = 1000;
        int windowHeight = 800;
    ```

3. Nu kan je deze waarden gebruiken in de __constructor__. Daarmee stel je de beginwaarden voor de hoogte en breedte van je game in. Omdat we de variabelen windowWidth en windowHeight reeds de waarde 1000 en 800 gegeven hadden, worden dit ook de beginwaarden voor het game window.

    ```csharp
    public Game1()
        {
            graphics = new GraphicsDeviceManager(this);

            //In de constructor gebruiken we deze extra variabelen
            //om de breedte en hoogte van het game window in te stellen.
            graphics.PreferredBackBufferWidth = windowWidth;
            graphics.PreferredBackBufferHeight = windowHeight;

            Content.RootDirectory = "Content";
        }
    ```
4. Nu kan je in de __update functie__ kijken of er een toets ingedrukt wordt en zo wisselen tussen de twee modi (Windowed en Fullscreen). Denk er wel aan dat je deze wijzigingen nu ook moet toepassen met _ApplyChanges()_. Hierboven in de constructor was dat niet nodig omdat de game nog niet gestart was.
In de code hieronder wordt er tussen de twee modi gewisseld door middel van de toetsen K en L. De toets K schakelt naar Fullscreen, de toets L naar Windowed mode.

    ```csharp
    //De voorwaarde bij if geeft true als de toets K ingedrukt wordt en 
    //het game nog niet in Fullscreen mode werkt (indien het game reeds
    //in Fullscreen mode werkt moet er natuurlijk niets gebeuren, vandaar
    //deze extra test naast het monitoren van de toets K).
    if(Keyboard.GetState().IsKeyDown(Keys.K) && !graphics.IsFullScreen)
    {
        graphics.PreferredBackBufferWidth = 1920;
        graphics.PreferredBackBufferHeight = 1080;
        graphics.IsFullScreen = true;
        graphics.ApplyChanges();
    }

    //De voorwaarde bij if geeft true als de toets L ingedrukt wordt en 
    //het game nog niet in Windowed mode werkt (indien het game reeds
    //in Windowed mode werkt moet er natuurlijk niets gebeuren, vandaar
    //deze extra test naast het monitoren van de toets L).
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
2. Open het opgaveproject Oefening2_GameWindowSize. Je vindt hierin de oefening waarin de ballon getoond wordt met de extra aanpassingen voor het schakelen tussen fullscreen en windowed mode. Wat gebeurt er wanneer je de schermverhoudingen niet wijzigt en overschakelt naar fullscreen?
3. Wat gebeurt er wanneer je _ApplyChanges_ vergeet?
4. Open het opgaveproject Oefening4_GameWindowSize. Je vindt hierin het voorbeeld dat we in dit hoofdstuk uitwerkten. Hoe kan je met een enkele toets (F12) wisselen tussen de twee modi?

