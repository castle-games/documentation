The game API lives in the `castle.game` module. The Castle game API lets you navigate to or get information about other games on Castle. 

Below you will see references to 'game URLs'. These are URLs such as '[https://castle.games/@bridgs/quickdraw-blackjack](https://castle.games/@bridgs/quickdraw-blackjack)' which refer to a game registered on Castle, but could also be HTTPS URIs to raw Lua code or Castle Project Files on the web. You will also see references to 'game ids', which are unique strings that identify each game on Castle. Currently there is no user interface to get the game id of a game on Castle, but this may be added soon.

### `castle.game.load(gameIdOrUrl, params)`

Ask Castle to load a different game. This closes the currently running game to load the other one. `gameIdOrUrl` (*string*) should identify the other game to navigate to, and can either be a URL or a game id. `params` should be a value to pass to the game being opened. `params` must have a value type as described in the [storage API reference](/documentation/reference/storage-api-reference) under "Keys and values". This value could itself be a table, allowing you to pass many values. The target game can retrieve params using `castle.game.getInitialParams`.

### `castle.game.getCurrent()`

Get information about the current game being played. This method will return a table with the following keys:

- `gameId` (*string*): The game id.
- `owner` (*table*): A table of data about the user that owns the game. Has the same format as returned by `castle.user.getMe` as described in the [user API reference](/documentation/reference/user-api-reference)
- `title` (*string*): The game title (as defined in the Castle Project File).
- `url` (*string*): The game URL.
- `description` (*string*): The game description (as defined in the Castle Project File).

### `castle.game.getReferrer()`

Get the game that used `castle.game.load` to load the current game. Returns a table with the same keys as returned in `castle.game.getCurrent`.

### `castle.game.getInitialParams()`

Get the `params` passed to `castle.game.load` when loading this game. If no `params` was passed, or this game was simply opened by clicking on the game or on a post in Castle's user interface, returns `nil`.

### `castle.game.isLocalFile(game)`

Returns true if the game is run the from the local file system and false otherwise. If no `game` is passed in, the current game will be used instead.