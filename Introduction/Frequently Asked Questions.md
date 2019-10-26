## What is Castle?

Castle is a platform and a community for making, playing, and sharing games. Right now, Castle is composed of:

- **The Castle community**, a group of creators and players who hang out on [Discord](https://discord.gg/4C7yEEC), [Twitter](https://www.twitter.com/_castlegames), and in the global chat room within Castle's desktop client.
- The **Castle desktop client**, a program for Windows and macOS which lets you build and play Castle games.
- [castle.games](/), a website which contains guides and documentation about Castle, and lets you share web links about Castle games and community members.
- **Community-supported resources** for making games, such as [share.lua](https://github.com/castle-games/share.lua), a library that helps create multiplayer games.

## How do I make Castle games?

If you have a computer with Windows or macOS and a text editor, you already have most of what you need. Castle games are written in Lua, and run inside the Castle client. Head over to our [getting started guide](/documentation/tutorials/make-your-first-castle-game) and we'll walk through creating a simple Castle game.

## Can I use Castle on Linux?

Castle's underlying tech stack can run on Linux, but we're a small team and don't currently maintain a build of the Castle desktop client for Linux. We might do that at some point, so if this interests you, please let us know!

## Can I use Castle on my phone?

For Android, you can get Castle from the [Play Store](https://play.google.com/store/apps/details?id=games.castle).

We are currently working on making Castle available on iOS!

## Is Castle a fantasy console?

No. Castle doesn't impose specific design constraints on its games, or an artificial hardware spec or virtual interface to a machine. You can create anything that can reasonably be expressed in Lua and that can run on a computer.

Castle games use a library called [LÖVE](https://love2d.org/) which contains some assumptions and constraints in its design. The Castle update loop assumes you use callbacks like `love.update(dt)` and `love.draw()`

## Does Castle cost money?

It is free to make, play, and share Castle games. We believe in a low barrier to entry for creating games, and we also believe that games are better with other people. Our primary focus is to build a supportive community.

We also believe that game creators should be able to make money without sacrificing the quality of their art. In the future, if we can build a community that helps creators make money, we might take a cut of that money to help us sustain the Castle platform. We don't do this right now.