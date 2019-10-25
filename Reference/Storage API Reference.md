The storage API lives in the `castle.storage` module. The API lets your game use a database that Castle provides to save game state. The data is saved "in the cloud," so it is shared across computers. You do not need to perform any set-up for your game to have access to this database, your games can use these APIs out-of-the-box!

## Storage types

There are two kinds of storage:

- **Global storage**: This storage is shared across all users playing a game. Example data that makes sense to store here includes high scores that you want all users to see or shared world state that you want to persist across runs of the game.
- **User storage**: This storage is private to each user. Example data that makes sense to store here includes the level a user reached in a single-player game with many levels, or the attributes of a character a user developed in a role-playing game.

In both cases, the storage is separate per-game, so that one game can't accidentally overwrite another game's data.

## Keys and values

The databases are "key-value" stores, where you associate a value with a key then use that key again later to retrieve that value. The keys are always strings. The values can each be of one of the following types:

- *boolean*
- *number*
- *string*
- *'string-keyed' table*: Lua tables whose keys are all strings, and values can be of any storage value type. So `{ a = 'hello', b = 'world' }` is allowed, and `{ a = 'hello', b = { c = 'nested' } }` is too, but `{ a = 'hello', 1 = 'world' }` is not (since it has both string and number keys).
- *arrays*: Lua tables whose keys are all consecutive integers starting with 1, and values can be of any storage value type. So `{ 'hello', 'world' }` is allowed, and `{ 'hello', { c = 'nested' } }` is too, but `{ 1 = 100, 5 = 20 }` is not (since the keys are not consecutive).

The purpose of these restrictions is so that the value can be stored in JSON format. For in-depth information on value-type encoding, please refer to the [manual for Lua CJSON](https://www.kyne.com.au/~mark/software/lua-cjson-manual.html#encode), which the API uses internally to save values into the database.

## Using `network.async`

All of the functions below perform network requests to access the database and take time to complete. So, calling them directly from `love.update` or `love.draw` would block the processing or drawing of your game while the network request finished. Instead, you should use `network.async` to run a block of code asynchronously from your game events. For example, to save the high-score when a new score is made:

```
function love.update(key)
    -- ... Other game code ...

    -- When a new score is created at the variable 'score'
    network.async(function()
        local lastHighScore = castle.storage.getGlobal('highscore')
        if not lastHighScore or lastHighScore < score then
            castle.storage.setGlobal('highscore', score)
        end
    end)

    -- ... More other game code ...
end
```

For these reasons it makes sense to **not call these functions every frame**, and instead only once in a while (say at the start of your game, when the user tries to save some data, when an important event such as a new highscore occurs, etc.).

## Global storage functions

### `castle.storage.setGlobal(key, value)`

Save `value` at `key` (*string*) in global storage. `value` must have a value type as described above, or it can be `nil`. If it is `nil`, this key is deleted from global storage.

### `castle.storage.getGlobal(key)`

Get the `value` stored at `key` (*string*) in global storage. Returns `nil` if there was no value saved at `key` or if it was deleted.

## User storage functions

### `castle.storage.set(key, value)`

Save `value` at `key` (*string*) in user storage. `value` must have a value type as described above, or it can be `nil`. If it is `nil`, this key is deleted from user storage.

### `castle.storage.get(key)`

Get the `value` stored at `key` (*string*) in user storage. Returns `nil` if there was no value saved at `key` or if it was deleted.