## What is this for?

This guide is for creators who made a Castle game, and want to share that game on their Castle profile, but prefer to use their **own file hosting service**.

For most users, we recommend following [this guide to add games to your profile](/documentation/tutorials/adding-games-to-your-profile). However, if you prefer not to upload your files to Castle, you can also host the game files yourself. Examples of non-Castle file hosting services include Github, Bitbucket, or any other website capable of serving static text files and assets.

## How do I add externally-hosted games to my profile?

### 1. Upload your game's files somewhere.

Using your web host of choice, upload the directory containing your game's code, assets, and **Castle Project File**.

The most common way to upload a Castle game is to push it to some hosted source control service, like [Github](https://github.com/) or [Bitbucket](https://bitbucket.com/). You are also welcome to host it on your own website, some other service, or anywhere that gives you a public url for your game's code.

Here is an [example github repository](https://github.com/bridgs/lil-chess/tree/master) containing a simple Castle game. Notice that it contains all the Lua code for the game, as well as the `.castle` project file.

Your game must have a **Castle Project File** which includes your Castle username in the **owner** key. In most cases, Castle already added this for you. If you don't have a Castle Project File, follow this [guide](/documentation/tutorials/describe-your-game-with-a-castle-project-file) to add one to your game.

### 2. Find the uploaded url to your game's Castle Project File.

For example, if you uploaded your game to Github, you can get the url to the .castle file by clicking the "Raw" button:

![Finding the Raw button on Github](https://user-images.githubusercontent.com/1316332/52986850-ebcdc280-33ad-11e9-8713-a186a29b55cd.png)

You'll end up with a url that looks like this one:

```
https://raw.githubusercontent.com/schazers/castle-tutorial/master/castle_tutorial.castle
```

### 3. Add your game's hosted url to Castle.

Open Castle and view your own profile. From your profile, click the **Add Game** button. From here, find the button that says **My game is already hosted online**.

![Hosting a game online in Castle](https://user-images.githubusercontent.com/1316332/58119355-a04ad080-7bb7-11e9-895c-76c4a1dd8d29.png)

You should see a form with a text box and some instructions.

![Hosting a game online in Castle](https://user-images.githubusercontent.com/1316332/58119417-cb352480-7bb7-11e9-9393-fcc05174109b.png)

Paste the **Castle Project File url** from step 2 into the box. This tells Castle where to go load your game. When Castle finds your game, it will render a preview for you.

![Previewing a self-hosted game on Castle](https://user-images.githubusercontent.com/1316332/58119679-61694a80-7bb8-11e9-94bc-af2474e1247d.png)

Click **Add Game**.

Congratulations! You've now added this game to your profile.

## What's next?

Now that your game is on your profile, anybody in Castle can find it and play it. You might want to make sure the game looks great, for example by adding some artwork or a primary color. There are lots of ways to customize your game's appearance, so check out the [Castle Project File Reference](/documentation/reference/castle-project-file-reference) for the full list.

If you upload any changes to your game's code, your players will receive those changes immediately. This is because Castle doesn't host your code, and just reads it from the url you provided.
For metadata changes you make to your Castle Project File, like artwork and title, Castle maintains an index of that information so people can view it on your profile. Castle will update this index about once a day. If you want to synchronize metadata changes immediately, find the game card and click the **U** button.

Happy creating!