The post API lives in the `castle.post` module. The post API lets you integrate with Castle's post system, which lets users share in-game moments or artifacts, and see and load those shared by others. Posts can attach arbitrary data, so they can serve as distributable containers for high-scores, levels, game state, or basically any artifact for games to save and load back.

## Creating posts

In Castle, users should always be aware that a post is being created on their part and they should be able to verify or edit the contents of the post or cancel the whole operation. So the post-creation APIs offered to games always lead to a confirmation screen rather than directly making posts unbeknownst to the user.

### `castle.post.create(options)`

Request the creation of a post on the part of the user. Must be called in a `network.async` block (see [storage API reference](/documentation/reference/storage-api-reference) under "Using `network.async`"). Takes a table `options` with the following keys:

- `message` (*string*): A default message to include in the post. The user will be able to edit this message in the confirmation screen.
- `media` (*string* or *ImageData*): Indicates the image to be included with the post. If it is the string `'capture'`, Castle automatically takes a screenshot to include as this image. If it is a LÖVE [ImageData](https://love2d.org/wiki/ImageData), that image is included. The *ImageData* form allows for many flexible forms of usage, say by rendering to a [Canvas](https://love2d.org/wiki/Canvas) then using `[Canvas:newImageData](https://love2d.org/wiki/Canvas:newImageData)` to generate *ImageData* from it.
- `data` (storage value type): Arbitrary data to include with the post that is given back to the game when the post is loaded. Must have a value type as described in the [storage API reference](/documentation/reference/storage-api-reference) under "Keys and values".

Returns the post id. This is a *string* that is unique for each post created and identifies that particular post for its entire lifetime.

## Loading posts

When the user clicks the "Open data" action on a post, Castle loads the post into a new instance of the game. The game can read this post either by calling the `castle.post.getInitialPost` function to get the initial post the game was opened with, or by defining the `castle.postopened` callback which Castle will call when a post is opened into your game.

You can also load a specific post by its id using `castle.post.get`. This is especially useful when combined with saving post ids in [storage](/documentation/reference/storage-api-reference).

Posts are read into your game as a table with the following fields:

- `postId` (*string*): The post id uniquely identifying this post. Same as the value returned by the `castle.post.create` call on creating this post.
- `creator` (*table*): A table of data about the user that created this post. Has the same format as returned by `castle.user.getMe` as described in the [user API reference](/documentation/reference/user-api-reference)
- `mediaUrl` (*string*): A URL to the image data displayed with this post (as indicated by the `media` option to the `castle.post.create` call). This URL can be used with `love.graphics.newImage` to load a LÖVE [Image](https://love2d.org/wiki/Image), which you can then draw.
- `data` (storage value type): The arbitrary data attached to this post, equal to the `data` option passed to the `castle.post.create` call that created this post.

### `castle.post.getInitialPost()`

Return the post that this game was opened with, as a table with the fields listed above.

### `castle.post.get(options)`

Load a specific post. Takes a table `options` with the following keys:

- `postId` (*string*, required): The id of the post, as returned by `castle.post.create`.
- `data` (*boolean*, optional): Whether to include the arbitrary data attached to the post. This is `false` by default. The arbitrary data can be large, so this allows skipping sending it over the network when it is not needed (eg. when you just want to preview a post with its media, but only open the data when the user selects it in your game).

Returns a table of post fields in the format described above. The `data` field is only included if `options.data` was truthy.

### `castle.postopened(post)`

If your game code defines this callback (just as you would define a LÖVE callback like `love.keypressed`), it is called when the game is opened with post data. A single parameter, `post`, is passed to the function, which is a table with the fields listed above.