Welcome to the first in a series of tutorials about making games on Castle! In this series we'll first get started with the basics: getting Castle setup, and learning how to draw graphics and react to user input, which form the basis of games. After that, we'll get into the unique social features offered by Castle's platform. These include displaying user avatars in your game, allowing your game to make posts and save data in Castle's database, and making your game multiplayer.

## Learning goals

Here's a list of things that we can hope to learn in this first tutorial:

-   Installing and setting up Castle
-   Software you will need other than Castle itself
-   Starting a new project
-   Drawing shapes
-   Reacting to input
-   Drawing images
-   Adding your game to your profile

## Installing and setting up Castle

_You can skip this section if you've already installed Castle and have a user account._

You can download the latest release of Castle from Castle's [home page](https://castle.games/).

If you're on **Windows**, this will give you a file named like 'Castle-\<version\>-Setup.exe', which you can launch and follow the instructions to install Castle.

For **macOS**, you will get a file like 'Castle-\<version\>.zip'. Extract this and put the 'Castle.app' file inside in your macOS Applications folder. Putting it in the Applications folder is necessary for auto-updates to work properly.

From now on, Castle can automatically check for updates, prompt you and update itself. You won't have to repeat the installation process on this computer!

When you first launch Castle, you will see the following screen:

!['Sign-in' screen](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/sign-in.png)

Follow the instructions to create an account (or sign in if you happen to have an account already). Having an account on Castle allows users to have profiles for their games, interact in chat and play multiplayer games.

You should now be ready to explore and play games on Castle. You probably came to this tutorial to learn how to make your own games, so let's learn how to do that.

## Software you will need other than Castle itself

### Code editor

Currently, games for Castle are made using the [Lua](https://www.lua.org/start.html) programming language. To write Lua code, you will need a code editor. The Castle team recommends [VS Code](https://code.visualstudio.com/) with the [vscode-lua](https://marketplace.visualstudio.com/items?itemName=trixnz.vscode-lua) extension. If you're already familiar with a code editor that supports Lua, you could continue using it. Vim, Notepad++, Sublime Text, Emacs are all popular code editors that have Lua support. In some cases these editors may need a plugin or some additional setup to enable syntax highlighting for Lua.

### Image editor (optional)

Usually game elements are displayed using images. For example, if you're making a Pac-Man clone, you may want to draw an image for Pac-Man, one image for each kind of ghost, and so on. To create or edit such images you will need an image editor. Any editor that exports common file formats such as JPEG or PNG will do (PNG is recommended to to retain image quality).

You can do without an image editor if you find pre-made images on the web, or if you want to just render abstract shapes such as circles and rectangles which you can do with pure code.

Now that we've gotten that out of the way, let's actually start our Castle game project!

## Starting a new project

In Castle's sidebar, click 'Create' to navigate to the Create screen:

![Click 'Create'](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/click-create.png)

On the Create screen, you will be presented with many options for starting a new project or opening an existing one. These include templates that start your game with some pre-existing code and images. In this tutorial we want to learn how to write our own code to start things off, so let's click on the 'blank' option:

![Click 'blank'](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/click-blank.png)

On the next screen, you will have a chance to set your project's name. You may also want to navigate to a different directory to save your project's files in. Under this directory, Castle will create a _new_ 'project directory' for your project, and the project's files wil reside within that new directory. Once you've picked the options you want, click 'Create Project':

!['Create Project' screen](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/create-project.png)

Once you do this, you will be greeted with the following screen, where you can click 'Open Project' to launch your project in it's current form:

![Ready to start making new project](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/open-created-project.png)

The initial version of your project should look like this:

![Initial new project](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/initial-created-project.png)

We're now ready to start writing some code! Open the 'main.lua' file under the project directory in your code editor and check out the current state of the code:

![Initial code](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/initial-code.png)

The project is currently only showing text, so let's start by making it draw some shapes.

## Drawing shapes

The most basic type of drawing involves drawing shapes such as circles, rectangles and ellipses. Let's start off by drawing a circle. Delete all the code currently in 'main.lua' and replace it with just the following 3 lines (we'll dig in and actually understand the code soon):

```lua
function love.draw()
    love.graphics.circle('fill', 40, 40, 20)
end
```

Make sure to have removed the old code, since we want to start from scratch. Save the file. Now hit the 'Reload Project' button in Castle, or hit 'Ctrl + R' (on Windows) or 'Cmd + R' (on macOS). Castle will reload your project, using your modified code. Make sure you saved the new contents of the file before reloading, or Castle won't be able to pick up the changes you made in your code editor! You should now see the following:

![First code change](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/first-change.png)

Congratulations! You've made your first Castle game code change.

Now let's take a moment to understand the code we wrote. First, we define a function named `love.draw`. What is love? In this case it's [LÖVE](https://love2d.org/), the Lua game framework Castle has built-in to let you code games. LÖVE has a ton of features and functions, which you can learn more about on [its wiki](https://love2d.org/wiki/Main_Page). There's a lot there, but you don't have to worry about digging into it just yet. This tutorial will explain each of the LÖVE features used as they come up. But it's good to know that all of the other LÖVE features are available in Castle, for when you want to go beyond this tutorial and expand your games on your own.

So, back to `love.draw`. LÖVE will run the code in `love.draw` whenever it's drawing the screen to display your game. This happens 60 times a second, to keep your game running smoothly. You can [read more about `love.draw`](https://love2d.org/wiki/love.draw) in the LÖVE wiki. From now on, we'll link LÖVE function names to the relevant wiki section for when you want to dig deeper.

Inside `love.draw`, we use the [`love.graphics.circle`](https://love2d.org/wiki/love.graphics.circle) function to draw a circle on screen. It takes 4 arguments: a drawing `mode` (in our case we use `'fill'` to draw a filled circle, as opposed to just an outline), `x` and `y` coordinates and a `radius`. The coordinate system starts with (0, 0) as the top-left of the game window, with the X-coordinate increasing rightward and the Y-coordinate increasing downward. By default, the width of the game window is 850 units and the height is 400 units. So with the values we put in, we get a little circle on the top-left.

_Note: A 'unit' here doesn't necessarily correspond to on-screen pixels of the user's monitor, since the user is free to resize their Castle window (and thus the game window). In Castle, you don't have to worry about these resizes and can continue assuming 850x450 units--Castle will automatically scale your game's drawing to fit. We will learn later how to use different sizes or even have our own resize logic._

The circle is currently white, but let's try making it a nice magenta. Change the code to the following:

```lua
function love.draw()
    love.graphics.setColor(0.8, 0, 0.8)
    love.graphics.circle('fill', 40, 40, 20)
end
```

We just added a [`love.graphics.setColor`](https://love2d.org/wiki/love.graphics.setColor) call. This function affects the color used in the draw calls after it. It takes 3 arguments: the red, green and blue components of the color respectively. It takes an optional 4th argument that can be used to set the opacity of the color. Each component must be in the 0 to 1 range. So with the values above, we get magenta:

![Change color](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/change-color.png)

Great, so we have a circle on screen, but can we move it around? Let's try it!

## Reacting to input

Let's try to let the user move the circle around with their keyboard. We used a fixed value of (40, 40) for the position of the circle, but if we change this value over time our circle would move. So let's first add some variables to store this. At the top of your file, add the following:

```lua
local x, y = 40, 40
```

Then change your `love.graphics.circle` call to this:

```lua
    love.graphics.circle('fill', x, y, 20)
```

If you reload now your game should be the same as before, and the keyboard doesn't affect anything yet. We need to listen for keyboard input and affect `x` and `y` accordingly. Let's add the following before `love.draw`:

```lua
function love.update(dt)
    if love.keyboard.isDown('left') then
        x = x - 2
    end
    if love.keyboard.isDown('right') then
        x = x + 2
    end
    if love.keyboard.isDown('up') then
        y = y - 2
    end
    if love.keyboard.isDown('down') then
        y = y + 2
    end
end
```

LÖVE runs [`love.update`](https://love2d.org/wiki/love.update) every frame and provides the `dt` parameter which is the amount of time that elapsed in this frame in seconds. Inside, we check if each of the left, right, up or down arrow keys is pressed and update the `x` or `y` values accordingly. If the left arrow key is down, we decrease the `x` coordinate by 2, so that the circle moves leftward. We perform this logic for each arrow key and the coordinate it affects.

If you reload your game now, you should be able to move the circle around with the arrow keys.

To ensure that the circle moves at a constant speed we need to use the `dt` parameter when updating the coordinates. Say we want to move the circle by 120 units each second. That means it would need to move by `120 * dt` each frame, since `dt` is in seconds. So let's change the code in `love.update`:

```lua
function love.update(dt)
    if love.keyboard.isDown('left') then
        x = x - 120 * dt
    end
    if love.keyboard.isDown('right') then
        x = x + 120 * dt
    end
    if love.keyboard.isDown('up') then
        y = y - 120 * dt
    end
    if love.keyboard.isDown('down') then
        y = y + 120 * dt
    end
end
```

If both `love.update` and `love.draw` are called every frame, why are they separate? The idea is to only put logic that _updates_ your game in `love.update`. In this case, that would be the code that changes the `x` and `y` values to move the circle. Then we only put logic that _draws_ the game in `love.draw`, which in this case would be the `love.graphics` calls that draw the circle.

To recap, here is the entire code for the game at this point:

```lua
local x, y = 40, 40

function love.update(dt)
    if love.keyboard.isDown('left') then
        x = x - 120 * dt
    end
    if love.keyboard.isDown('right') then
        x = x + 120 * dt
    end
    if love.keyboard.isDown('up') then
        y = y - 120 * dt
    end
    if love.keyboard.isDown('down') then
        y = y + 120 * dt
    end
end

function love.draw()
    love.graphics.setColor(0.8, 0, 0.8)
    love.graphics.circle('fill', x, y, 20)
end
```

Circles are nice, but let's now try drawing some images!

## Drawing images

First we will have to acquire or create an image to draw. For this tutorial let's try using the following image, from http://millionthvector.blogspot.com/p/free-sprites.html:

![ship.png](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/ship.png)

Put the image with a simple file name such as 'ship.png' next to your 'main.lua' file in your project directory.

Now we'll have to add code to load the image into the game. Add the following line at the top of 'main.lua':

```lua
local shipImage = love.graphics.newImage('ship.png')
```

We're using [`love.graphics.newImage`](https://love2d.org/wiki/love.graphics.newImage) to load the image as an [`Image`](https://love2d.org/wiki/Image) object. Make sure to use the file name of the image you put in your project directory. The object can then be drawn in the `love.draw` function. Let's remove the existing contents of the `love.draw` function and replace it with:

```lua
    love.graphics.draw(shipImage, x, y)
```

We use [`love.graphics.draw`](https://love2d.org/wiki/love.graphics.draw) to draw our image object, with the same `x` and `y` values that we used for the circle before. This should give the following result. You'll be able to move the ship around with the arrow keys:

![Draw image](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/draw-image.png)

Again, for reference, here is the entire code of the game at this point:

```lua
local shipImage = love.graphics.newImage('ship.png')

local x, y = 40, 40

function love.update(dt)
    if love.keyboard.isDown('left') then
        x = x - 120 * dt
    end
    if love.keyboard.isDown('right') then
        x = x + 120 * dt
    end
    if love.keyboard.isDown('up') then
        y = y - 120 * dt
    end
    if love.keyboard.isDown('down') then
        y = y + 120 * dt
    end
end

function love.draw()
    love.graphics.draw(shipImage, x, y)
end
```

That'll be all for our first game on Castle! Now let's add our game to our profile so others can check it out.

## Adding your game to your profile

First, we'll want to update the description and cover image of our game. Open the file with the '.castle' extension in your project directory. You should be able to use your code editor to open this file. You will see something like the following:

```yaml
main: main.lua
title: My Tutorial 1
owner: nikki
```

The `title` field will have the title you set in the 'Create Project' screen initially, and the `owner` field will have your username. Let's add a description and a cover image for our game. Add the following line at the bottom of the file, to give a description for your game:

```yaml
description: I made this game based on Castle tutorial 1! Use your arrow keys to move the spaceship around.
```

You can use your own description. The description should be on one line for the file to be read properly by Castle. Now let's add a cover image. The cover image is used for the display of your game as a game card on Castle, such as on the home page, on your profile, or in search results. We'll use the following cover image in this example, but feel free to use any image of your own:

![cover.png](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/cover.png)

Put this image with a name such as 'cover.png' in your project directory. Then add the following line to your '.castle' file, referencing the same file name:

```yaml
coverImage: cover.png
```

For reference, here is what the '.castle' file may now look like (make sure to use your own username!):

```yaml
main: main.lua
title: My Tutorial 1
owner: nikki
description: I made this game based on Castle tutorial 1! Use your arrow keys to move the spaceship around.
coverImage: cover.png
```

Now let's add the game to our profile. First, navigate to your profile by clicking on your username in the sidebar:

![Click username](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/click-username.png)

Then, click 'Add game' on that page:

![Click 'Add game'](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/click-add-game.png)

This should bring you to the 'Add a Game' screen. Here, click 'Change folder' and select your project directory. You will get a chance to verify the title, description and cover image of your game with the preview below. If everything looks right, click 'Upload and Add Game':

!['Add a Game' screen](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/add-game.png)

Castle will upload the files for your game to Castle's servers and add the game to your profile. After this, you will be taken to your profile, where you will see a new game card for your game:

![Game card on profile](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/game-card.png)

Click the card to play your game! Any Castle user can now go to your profile and find the game to play. You can also use the 'Copy Link' feature on the game card to copy a link to your game and send it to other users:

![Click 'Copy Link'](https://raw.githubusercontent.com/castle-games/castle-tutorials/master/1/copy-link.png)

Congratulations! You've made a Castle game and added it to your profile. You can update your game at any time by editing the '.castle' file or 'main.lua' and repeating this step.

The next tutorial will show you how to add Castle-specific features to your game, such as storing data in a database and making posts.
