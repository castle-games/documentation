The dimensions of a game (width and height on screen) make a big difference in how it appears to players. Likewise, the scaling behavior (how your game's graphics change when the screen real estate is bigger or smaller) can have a similar impact. Castle offers several different configurations you can use to make sure your game uses screen space the way you want.

All of these are keys you can change in your game's **Castle Project File**. Check out [this guide](/documentation/tutorials/describe-your-game-with-a-castle-project-file) if you'd like more information about Castle Project Files, and also see the full [Castle Project File Reference](/documentation/reference/castle-project-file-reference).

## dimensions

The `dimensions` key specifies the dimensions of your game. Specifically, it describes the desired dimensions of your game's screen in LÖVE units (as will be returned by [love.graphics.getDimensions](https://love2d.org/wiki/love.graphics.getDimensions)), specified in the format '_widthxheight_' or '_width_' or '_xheight_'.

For example, `dimensions: 400x200` would make your screen size be 400 units wide and 200 units tall. By default this is `dimensions: 800x450`.

[love.graphics.getDimensions](https://love2d.org/wiki/love.graphics.getDimensions) will always return these values, even as on-screen size changes (due to window resizes or layout updates). Castle will automatically scale your game's rendering to fit the available screen space while maintaining the aspect ratio. This way your code doesn't have to handle the various cases. Castle's scaling works at the draw call level so that lines, circles high-res images, etc. are still drawn crisp. See the `scaling`, `upscaling` and `downscaling` settings below to configure this behavior further.

It is also possible to specify only a width, with the '_width_' format (so you could use `dimensions: 400` for example). In this case the game is scaled to fit the width of your game to the available width, and the height is set dynamically based on the available space. This is useful if you want to fill the available space completely. There is also a version of this setting where you specify only the height, in the '_xheight_' format (so `dimensions: x400` for example). In these cases [love.graphics.getDimensions](https://love2d.org/wiki/love.graphics.getDimensions) would return the fixed with or height with the other dimension being the dynamic value.

You can also override all this and set `dimensions: full` to make your game's screen fill the entire available space and disable scaling (recommended for advanced use only). In this case, [love.graphics.getDimensions](https://love2d.org/wiki/love.graphics.getDimensions) will return the dynamic dimensions of the available space. These dimensions will change as the window is resized or the interface layout changes, so make sure your code uses the dynamic values to give the user a good experience.

## scaling

The `scaling` key specifies the scaling behavior of your game depending on the available screen space. Can be `on` or `step`.

`on` is the default and makes Castle smoothly scale your game to fit the available space while maintaining aspect ratio.

`step` makes your game scale up by integer factors only (2x, 3x, ...) and down by power of two factors only (0.5x, 0.25x, ...) on desktop screens. This is recommended for games that have pixel-art-like styles. It works well with nearest-neighbor filtering for images (when you call [love.graphics.setDefaultFilter](https://love2d.org/wiki/love.graphics.setDefaultFilter) or [Image:setFilter](https://love2d.org/wiki/Texture:setFilter) with `'nearest'` parameters). On mobile screens step scaling is ignored and the system provides the `on` behavior because of the small available space and high DPI.

You can use the `upscaling` or `downscaling` settings explained below to configure these for each of those cases (eg. you can make upscaling provide step behavior while making downscaling smooth).

This setting does not apply when your game uses `dimensions: full`.

## upscaling

This key is the same as `scaling` above but only configures the behavior when the available space is larger than your game's dimensions. Like `scaling`, this doesn't apply when your game uses `dimensions: full`.

## downscaling

This key is the same as `scaling` above but only configures the behavior when the available space is smaller than your game's dimensions. Like `scaling`, this doesn't apply when your game uses `dimensions: full`.
