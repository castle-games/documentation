If you made a game you want to share with others, you can add it to your Castle profile. This article describes why, and how, you would do that.

## Why add games to my profile?

When you add a game you made to your Castle profile, here are some things you get:

- A permanent link you can share, like `http://castle.games/+abc123/@your-name/cool-game`
- A game card that shows up on your profile.
- Presence in Castle Search, Recents, and anywhere else Castle might want to surface your game to players.

![A profile which contains one game.](https://user-images.githubusercontent.com/1316332/58117517-9c1cb400-7bb3-11e9-8881-cf20ec9c0be7.png)

## How do I add games to my profile?

### 1. Click "Add Game".

You can find this button on your own profile. If you don't have a Castle account, now is a good time to [create one](/posts/@castle/creating-an-account).

![The Add Game screen of a profile](https://user-images.githubusercontent.com/1316332/58117417-5d86f980-7bb3-11e9-9e23-1786c5fd4fbd.png)

### 2. Choose the folder with your game's source code.

Click the **Choose Folder** button and find the folder containing the game you want to add.

Your game must have a **Castle Project File** which includes your Castle username in the **owner** key. In most cases, Castle already added this for you. If you don't have a Castle Project File, follow this [guide](/posts/@castle/describe-your-game-with-castle-file) to add one to your game.

![Showing a Castle Project File](https://user-images.githubusercontent.com/1316332/58117583-c0789080-7bb3-11e9-8e40-4d1b2d1ffb8e.png)

### 3. Make sure everything looks right.

After you choose a directory, Castle will render a preview of the game at that directory, including the title, description, and the future link to the game.

![A game preview in Castle](https://user-images.githubusercontent.com/1316332/58117753-21a06400-7bb4-11e9-87a3-e8dcc290fd2f.png)

Bear in mind that after adding your game, you can update it at any time later.

You might notice the greyed out `+id` shown in the previewed url for your game. Your game will get a random id after you Add it, but we don't know the id until you finish adding the game. So we show a placeholder within this url preview.

### 4. Click "Upload and Add Game".

Castle will **upload** your game's code and assets to Castle's server, and then it will **Add** the game to your profile.

Congratulations, you've added a game to your profile.

## What's next?

### Make sure your game looks great

Now that your game is on your profile, anybody in Castle can find it and play it. You might want to make sure the game looks as good as possible, for example by adding some artwork or a primary color. There are lots of ways to customize your game's appearance, so check out the [Castle Project File Reference](/documentation/castle-file) for the full list.

### Update your game

You can **Update** your game at any time. Find the game's card on your profile, click the **U** button, and click **Update....**

### Use your own file hosting

If you prefer not to upload your files to Castle, you are welcome to use a different hosting service. For example, some people like to use a Github repository instead. You can change where your game's files are hosted at any time. For more information, see [Hosting Your Own Games](/posts/@castle/hosting-your-own-games).

### Check in your .castleid file

When you add a game, Castle writes a small file called `.castleid` to your project directory. This file helps Castle maintain an association between your local source code and the online Castle game, so next time you want to update your game, we can recognize that it's the same project.

If you're using source control, we recommend that you check in the `.castleid` file and don't ignore it.