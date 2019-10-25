The system API lives in the `castle.system` module. The Castle sytem API lets you access information about or perform activities relating to the underlying system Castle is running on.

### `castle.system.isDesktop()`

Returns `true` if running on a user's desktop (Windows or macOS) system, `false` otherwise.

### `castle.system.isRemoteServer()`

Returns `true` if running on a Castle remote multiplayer server, `false` otherwise.

### `castle.system.setDimensions(width, height)`

Set the expected dimensions of your game in [LÖVE units](https://love2d.org/wiki/love.graphics.getDimensions). This is the same setting defined by the `dimensions` key in the Castle Project File, except you can set it dynamically through code. You can also call `castle.system.setDimensions('full')` to get the `dimensions: full` behavior. See [Game Dimensions and Scaling](/documentation/reference/game-dimensions-and-scaling) for more information on how this setting affects your game.

Since this call updates the Castle UI layout to re-position your game, it is recommended to call this function at most once at the start of your game (in that case preferring to use the Castle Project File so settings take effect immediately on load), or only rarely afterward, say when the user changes a setting or other important events occur.

### `castle.system.setScalingModes(up, down)`

Set the scaling mode for your game when it's not in `dimensions: full` mode. This is the same setting defined by the `upscaling` and `downscaling` keys respectively in the Castle Project File, except you can set them dynamically through code. Each of `up` and `down` can be `'on'`, `'step'` or `'off'`. You can also call this function with just one argument to set the same behavior for both upscaling and downscaling. See [Game Dimensions and Scaling](/documentation/reference/game-dimensions-and-scaling) for more information on how this setting affects your game.

Since this call updates the Castle UI layout to re-position your game, it is recommended to call this function at most once at the start of your game (in that case preferring to use the Castle Project File so settings take effect immediately on load), or only rarely afterward, say when the user changes a setting or other important events occur.

### `castle.system.getGlobalScaling()`

Returns a *number* which is the scaling factor of the user's system Castle is running on. This is equal to 1 on all systems other than Windows. On Windows this depends on the user's scale setting under "Display settings." It returns the fractional value corresponding to this percentage value. So, for example, if the user's setting is 125%, it returns 1.25.