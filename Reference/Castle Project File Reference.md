A Castle project file (for example, `my-project.castle`) is a text file with a special format that you can write to describe your game. To learn more about Castle project files, why they are useful, and how to add one to your game, check out the full guide: [Describe your game with a Castle project file](/documentation/tutorials/describe-your-game-with-a-castle-project-file)

Castle project files have the file extension `.castle` and are written in [YAML](https://en.wikipedia.org/wiki/YAML).

## List of .castle keys

This section provides a reference of all possible keys you can add to a Castle project file. The only required key is `main`.

- `main`: Relative path to a the Lua entry point file that Castle should use to load this game. For example, `main.lua`.
- `title`: The title of this game.
- `description`: A brief description of this game.
- `owner`: The Castle username of the owner of this game. Required in order to [add this game to a Castle profile](/documentation/tutorials/adding-games-to-your-profile).
- `draft`: A boolean. If `true`, Castle will display "Work in Progress" on your Game's card and won't feature the game on the Castle home screen. Default is `false`.
- `dimensions`: The desired dimensions of your game's screen in [LÖVE units](https://love2d.org/wiki/love.graphics.getDimensions). The default value is 800x450. See [Game Dimensions and Scaling](/documentation/reference/game-dimensions-and-scaling) for much more detailed information.
- `scaling`: How your game should scale when changing size to fit screen space. Can be `on` or `step`. See [Game Dimensions and Scaling](/documentation/reference/game-dimensions-and-scaling) for much more detailed information.
- `upscaling`: Same as `scaling` above but only configures the behavior when the available space is larger than your game's dimensions.
- `downscaling`: Same as `scaling` above but only configures the behavior when the available space is smaller than your game's dimensions.
- `coverImage`: A url or relative path to an image containing some artwork for this game. Castle will use this image when showing a preview of this game on profiles, in search results, and elsewhere.
- `primaryColor`: A hex string (without the `#`) for a color that represents this game. For example, `C0C0C0`. Castle may use this when rendering previews of the game.
- `multiplayer`: A dictionary with the following possible keys. If omitted, the default is a dictionary with a single pair, `enabled: false`.
  - `enabled`: A boolean. If `true`, indicates to Castle that this game is an online multiplayer game that uses Castle's hosted multiplayer servers.
  - `serverMain`: Similar to `main`. A relative path to an alternative entry point Lua file to be used when the game's code is run on a multiplayer server.
- `unlisted`: A boolean. If `true`, Castle will not show this game in Search results, even if you added it to your profile. Default is `false.`

## Deprecated keys

These keys are deprecated, but you might see them in older Castle project files. It is not recommended to add these to your game, because they might stop being supported.

- `name`: Alias for `title`
- `username`: Alias for `owner`.
- `coverImageUrl`: Alias for `coverImage`.

## Example Castle Project Files

All of Castle's starter examples contain Castle Project Files. For example, here is the [lil platformer project file](https://github.com/bridgs/lil-platformer/blob/master/lil-platformer.castle).
