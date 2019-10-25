When starting a new Castle game, the recommended path is to [use the Create button in Castle](/documentation/tutorials/make-your-first-castle-game).

This tutorial describes how to make a Castle game from scratch, using just a text editor to write the basic files instead of letting Castle provide them for you. This tutorial exists mostly as an educational reference, explaining what's going on in the details of the new project creation process.

## Making a minimal game

The absolute minimum that you need to run a game in Castle is just a text file containing the Lua code for `love.draw()`. Castle supports all the [LOVE](https://love2d-community.github.io/love-api/) callbacks and uses these as the entry point into the code for your game.

To construct a minimal example, put a new text file somewhere that Castle can load it. This would often be in a new directory on your local filesystem, but it's also possible to serve it from a URL on the web or anywhere else. You can name this file anything, but Castle typically follows the convention of calling it `main.lua`.

Put this Lua code in your text file:

```
function love.draw() 
  love.graphics.print("Hello World", 400, 300) 
end
```

You now have a tiny Castle program. You can open `main.lua` directly in Castle and you should see the string `Hello World` printed on screen.

## (Optional) Castle Project Files

If you want to provide metadata for your game with a [Project File](/documentation/tutorials/describe-your-game-with-a-castle-project-file), you can make one. Call it something like `mygame.castle`. You can make "mygame" whatever you want, but make sure you give it the `.castle` extension.

Put this in your `.castle` file:

```
main: main.lua
title: My Game
owner: mycastleusername
description: A description of my game
```

Check out [this guide](/documentation/tutorials/describe-your-game-with-a-castle-project-file) for a lot more information about Castle project files.