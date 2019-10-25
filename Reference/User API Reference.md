The user API lives in the `castle.user` module. Castle's user API is responsible for retrieving information about the users playing a Castle game.

### `castle.user.isLoggedIn`

A *boolean* variable indicating whether the user is currently logged in.

### `castle.user.getMe()`

If the user is currently logged into Castle, returns a table of information about the user. The table has the following keys:

- `userId` (*string*): A unique string identifying this user across Castle. It is guaranteed to remain constant through the existence of a user in the Castle network. The string is picked automatically by the Castle system when a new user signs up and remains internal to the system and doesn't get displayed to or edited by the user.
- `username` (*string*): The user's username.
- `name` (*string*): The user's name (a separate field from their username that they can choose on their profile).
- `photoUrl` (*string*): A URL to the image representing the user's profile photo. This URL can be used with love.graphics.newImage to load a LÖVE [Image](https://love2d.org/wiki/Image), which you can then draw.

If the user isn't logged in, the function returns `nil`.