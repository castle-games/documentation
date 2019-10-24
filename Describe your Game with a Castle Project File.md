Castle uses a type of file called a *Castle Project File* to show useful information about your game, like its title and artwork. This tutorial describes how Castle project files work, how to add one to your game, and how to customize it.

## What is a Castle project file?

A *Castle project file* (for example, `my-project.castle`) is a text file with a special format that you can write to describe your game. For example:

```
main: main.lua
title: Sparkle Unicorn Revenge
description: Join Todd the Unicorn on a journey to collect all the pizza.
```

Castle project files use the `.castle` file extension, and they are written in [YAML](https://en.wikipedia.org/wiki/YAML). You don't need to know much about YAML to understand them. As long as the above example makes sense, that's about all there is.

## What can I do with a Castle project file?

Let's use the same one as an example, and explain each thing in it:

```
main: main.lua
title: Sparkle Unicorn Revenge
description: Join Todd the Unicorn on a journey to collect all the pizza.
```

The title of this game is *Sparkle Unicorn Revenge*. Castle will display this title in your history, on your profile, in search results, and generally anywhere it needs to refer to the game.

The description of this game is *Join Todd the Unicorn on a journey to collect all the pizza*. Castle will use this anywhere it needs to display a longer piece of information about the game.

Lastly, the line `main: main.lua` tells Castle where to find the code to actually run the game. The main key refers to the Lua file (relative to this Castle project file) that Castle should begin reading first, also known as the *entry point* for your game. This way, if you open `my-project.castle` file directly in Castle, it has all the information it needs to start playing.

You can customize more aspects of your game, but those are the basics. Check out the [full spec](/documentation/castle-file) to see all the possibilities.

## How do I add one of these to my game?

Castle automatically creates one of these for you any time you create a *New Project*. Take a look in your project folder and find a file with the `.castle` file extension. If you don't have one and want to add one, follow these steps:

1. 1. Copy and paste this into your favorite text editor:

```
---
main: main.lua
title: My Great Game
```

**Note:** Make sure that the `main:` key actually has the name of your entry point file. The most common name is `main.lua`, but if you named yours something else like `my-game.lua`, you might need to update it.

![Example Castle Project File](https://user-images.githubusercontent.com/1316332/53039231-93d99f00-3433-11e9-890d-f2fae7bb903c.png)

2. From your text editor, save this file as `project.castle` in the same directory as your game's lua code.

![Saving project.castle](https://user-images.githubusercontent.com/1316332/53039243-99cf8000-3433-11e9-87a7-f8172b0fea3c.png)

That's it! You can now open `project.castle` directly in Castle, and you should see the *My Great Game* title appear with your game.

## What's Next?

You can customize more than just the title and description of your game using this kind of file. Check out the [full Castle Project File spec](https://castle.games/documentation/castle-file) to see all the possibilities.

Adding a Castle project file to your game is required if you want to add your game to your Castle profile. Check out our guide on [Adding Games to your Profile](/posts/@castle/adding-game-to-castle-profile) to learn more.