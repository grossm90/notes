# Intro to Godot: Platformer

*Godot*  is an open source game engine that supports both 2d and 3d game development. You'll find that Godot is  *far* more complex than PICO-8, so try not to get overwhelmed. As with everything in game design, focus on one core idea at a time, and try your best to truly understand it. Then, experiment with connecting that core idea to other core ideas that you've learned previously.

Let's get started!

## Starting a Project

It's pretty simple to start a project in Godot. After opening the program, you'll see the "projects" screen. On the top-left you will see a button labeled "+ New". Click the button and a window will pop up that will ask you to set some options for your new project. We'll set the name to "Platformer". For the project path, we'll navigate to our "Documents" folder, and therein we will create a folder called "godot" and inside of that we will create a folder called "lessons". We'll leave the renderer on "Forward+", and the version control on "Git".

Click on the "Create & Edit" button and wait for the Godot editor to load.

## Importing the Assets

As we discussed last year, there is *much* more to game development than just programming, but we could never finish discussing all of the topics in this class in time if we had to make our own art and music for every game, so for most lessons we will be using pre-made assets.

To get these assets into our project we must first download them from our Moodle course. Once you've downloaded the file, you must extract it because it is compressed. The simplest way to extract the files is to open the compressed folder, and drag its contents onto the desktop. Once the files are extracted, locate the "FileSystem" section of the Godot editor; it is on the bottom-left. Drag the folder called "assets" that you extracted into the FileSystem and delete the folder from your Desktop.

## Nodes and Scenes

Godot projects are created from fundamental building-blocks called *nodes*. A node is comparable to class in object oriented programming, and thus allows us to create game objects such as sprites, sound effects, menu items and much more.

A collection of nodes is called a *scene*. The player for example will be a scene made up of a sprite node, a hitbox node, and a physics node.

Scenes can be loaded into other scenes. This process is called *nesting*. This allows us to have a "Level" scene that has the "Player" scene loaded in when the level loads, along with all of the enemies, platforms, hazards, coins, etc.

### Our First Scene: MainGame

Let's start by creating the main game scene. On the top-left of the editor is a section called "Scene". Click the "2D Scene" button to create the *root node*, the node from which all other nodes branch from. Right-click this new node select "Rename" and name it "MainGame". By convention, we name nodes in Godot using PascalCase, which is similar to camelCase, but the first letter is capitalized. 

Now would be a good time to save this scene. Press `Ctrl+S`, in the new window on the upper-right click on the "Create Folder" button and make a folder called "scenes". Double-click on that folder and click the "Save" button on the bottom of the window to save the scene.

Let's also run this project for the first time. On the top-right of the editor you will see a play icon "▶". Click on the icon and a pop-up message will say that we have not chosen a main scene. Click on the "Select Current" button and the game will load. Nothing exciting will happen, of course, because we haven't made anything, but there should be no errors. Press the stop icon "■" near where you found the play icon to stop the game.

## The Player Scene

We are currently in the `MainGame` scene. To create a new scene, we must click the "+" at the top of the screen where the tabs are located. This time, the root node will not be a 2D Scene node, instead we want a very specific node. In the "Scene" section click on the "Other Node" button. A window will pop up showing a list of all of the nodes. Thankfully there is a search bar to make finding specific nodes easier. The node we are looking for is called "CharacterBody2D". Start typing the first few letters and the search function will narrow down the results quickly. Double-click on the node to select it as the root for this scene. Then right-click on the node, select "Rename" and set the name to "Player".

As mentioned previously, the `Player` scene will be made up of three nodes. We just created the first one, the root node, using `CharacterBody2D`. This contains all of the physics for the player, allowing it to move, jump, fall, and collide with objects. You'll notice however that there is a warning symbol next to the node. There are two issues. First, we won't be able to see the player as a `CharacterBody2D` does not contain any sprite information. Second, `CharacterBody2D` can't do much in the way of physics without a hitbox. Let's fix these issues now.

### Adding a Sprite to the Player Scene

The sprite will need to be a *child* of the root node. To do this, right-click on the root `Player` node and click "Add Child Node". The window with the list of nodes will pop up again. This time, search for "AnimatedSprite2D". Be careful not to select Sprite2D as we want our player to be animated, not static. After adding `AnimatedSprite2D` to the scene-tree, rename it to "PlayerSprite".

Now that we have two nodes in a single scene, switch between them by clicking on one, then the other. Notice a change on the right side of the editor? That area is called the *Inspector*. This area allows us to change the properties of the node. Click on the `PlayerSprite` node and look at the Inspector. Near the top you should see a property called "Sprite Frames".  This is where we can load in the individual sprites that make up the animation for the player. Click the drop-down arrow "∨" and select "New Sprite Frames", then click on the box that says "SpriteFrames". This will open a new area at the bottom of the screen called "SpriteFrames" which will let us edit the sprites for our player character.

To add frames from a sprite-sheet in our `res://assets` folder, look for the section labeled "Animation Frames:" on the bottom of the editor. There you will see a toolbar across the top. One of the buttons in the toolbar looks like a grid of squares "▦". If you hover over this button, the tool tip reads: "Add frames from sprite sheet (Ctrl+Shift+O)". Click on this button. A file explorer will open, navigate to `res://assets/sprites/knight.png`. This will open the sprite-sheet for the knight. Godot tries its best to cut the sprite-sheet into a grid based on the art, but will probably fail. We can correctly divide it up manually by changing the "Horizontal" and "Vertical" settings to "8". Select the first four in the top-left from left to right. They should highlight and be labeled "0, 1, 2, 3". Click the "Add 4 Frame(s)" button at the bottom of this window to lock in our sprite frames.

You probably wont be able to see the knight at first as we are working with pixel art which is pretty small on modern screens. Press the `F` key to center this node on the screen and zoom in until you see the knight. You should notice two issues. One, the art is blurry, and two it isn't animated. Let's fix the blurriness first.

At the very top-left of the screen, find the "Project" menu and select "Project Settings...". Under "∨ Rendering", select "Textures". Change "Default Texture Filter" from Linear to "Nearest", and then close the window. The art should look much more crisp. Select the `PlayerSprite` from the node tree if it isn't already select to re-open the "SpriteFrames" window at the bottom of the screen. To preview the animation, click on the play button "▶" in the "Animation Frames:" toolbar. The knight should bounce up and down. It's a little slow though. Let's speed up the animation by changing the "Animation Speed" setting under "Animations:" from 5 to "10". The animation should play a little faster now. While we're here, let's also turn on "Autoplay". It's the little arrow with small "A" inside of it to the right of the trashcan. This will start the animation as soon as the player is loaded into the scene.

With the animation out of the way, let's move on to hitbox.

### Adding a Hitbox to the Player Scene

To add a hitbox to the player, we need to create another child node to the root. Right-click on the `Player` node and select "Add Child Node". This time we will search for "CollisionShape2D", add it to the node tree and rename it to "PlayerHitbox". Select it in the node tree and look over to the inspector. At the top is a property called "Shape". Click on the drop-down menu and select "New CircleShape2D". A bluish circle should appear with two grips. One of these grips changes the diameter of the circle and the other changes its location. Size the circle so it fits completely inside the sprite graphics (nothing is more annoying than getting hurt by an enemy that clearly missed your player), and move the circle so the bottom just barely makes contact with the knight's feet. Don't worry about getting perfect placement, as you will be able to adjust this at any time in the future.

Our player is done for now, so let's save this scene by pressing `Ctrl+S`.

## Adding the `Player` Scene to the `MainGame` Scene

Nesting scenes in Godot is fairly simple. Let's switch back to the `MainGame` scene by selecting its tab at the top of the editor. Then, from the "FileSystem" window in the bottom-right, open the "`scenes`" folder and drag "`Player.tscn`" into the main window of the editor. You should see the knight right away (though you may need to zoom in).

Now we need a camera to follow our player around.

### Adding a Camera to our `Player`

Now that we have two nodes in the `MainGame` scene, the root `MainGame` node and the `Player` node, which should the camera be a child of? Well, we want the camera to follow the player around, so that should make this choice fairly obvious. Right-click on the `Player` node and select "Add Child Node". From the list of nodes, search for "Camera2D" and add it to the node-tree. Rename it to "PlayerCamera". If you zoom out, you'll see a purple rectangle. This represents the borders of our camera. The default is zoomed out too far. In the Inspector change the zoom property to "4" for "x" and "y" (they are linked, so changing one should automatically update the other).

We can now test our game again, but this time actually see something (our animated knight). Click on the play button "▶" on the top-right of the editor and the game should launch with the knight bouncing on the screen. Press the stop icon "■".

Lets add some movement!

## Our First Script

Nodes and their properties in the Inspector will only get us so far. At some point we must write code for our game. In Godot, code is written inside of a *script*, which can then be attached to a node to modify its behavior.

Switch back to the player scene by using the tabs on the top of the editor. Right click on the root `Player` node and click "Attach Script". Now, because this node is a `CharacterBody2D`, Godot has a built-in template script for handling 2D movement. How convenient! You should see the template already applied in the pop-up window. We'll leave that and most other settings alone. The one thing we want to change is where this script is saved. Click on the folder icon "🗀". In this pop-up window click on the "Create Folder"  button, and name the new folder "scripts", and save this script here. You should see the "Path:" option update. Click the "Create" button to finish attaching the script.

You'll see a lot of code here. Don't be intimidated by this as most of it will be perfect for this lesson. You can test the game again now, but it won't look like much has changed. In fact, the player is actually falling, but because the camera is following it and there is no scenery, its hard to tell. Stop the game and let's add some platforms.

## `TileMapLayer`

The `TileMapLayer` node allows us to create grid-based maps using a tile-map from a sprite sheet called a "Tile Set. This makes creating 2D levels very easy and is perfect for our current goal.

Right-click on the `MainGame` node, select "Add Child Node" and select "TileMapLayer". Similar to adding sprites to our player, go over to the inspector, find the "Tile Set" property, click on the drop-down arrow "∨", and select "New TileSet". Then, click on the word "TileSet",  and the section at the bottom of the editor should update. There should be a little error message that says that the TileMap does not have a TileSet source. Switch from TileMap, to "TileSet" at the very bottom of the editor. There will be a section that is labeled "Tiles". There is a plus sign "+" at the bottom that will bring up the file explorer. Navigate to `res://assets/sprites/world_tileset.png`. Godot should ask if you'd like it to automatically slice the sprite-sheet into tiles. You can click "Yes" for this, as this sprite-sheet is much more uniform than the knight is, and should get sliced cleanly. 

There is one small issue to fix. The top of the palm tree got sliced into nine separate tiles, but we would never place some, but not all of them. Click the icon of the eraser in to toolbar at the top of this section and then click on each of the nine squares that make up the top of the palm tree. Those tiles should go dark. Now, turn off the eraser tool by clicking on it again. Finally, click on the top-left tile that made up the top of the palm tree and drag to the bottom-right. Now this will act as a single, large tile.

Let's test the game... and we fall through the map. This is because there is no collision on the tiles.

### Adding Collision to Specific Tiles

In the inspector, find the drop-down labeled "∨Physics Layers" and click on it show the properties. Click on the button labeled "Add Element". Two sets of boxes should appear, one labeled "Collision Layer" and the other "Collision Mask". Both should have the number "1" turned on and the rest turned off. Now we can go back to the "TileSet" section of the editor, and switch to the "Paint" tab. Click on the "Select a property editor ∨" drop-down and click on "Physics". Click on every tile that looks like a terrain block and the two crate tiles. They should now have a light-blue filter over them. We also want collision on the bridge tiles, but notice how they do not take up the entire space of a tile. Use the editor on the left to get the correct shape for the bridge tiles.

Let's test the game again. You should now be able to walk around your map! Be sure to test your custom collision shape for the bridge tiles. The player should not get hung-up on any of the bridge tiles; you should be able to walk smoothly across them.

## Some Small Tweaks

Now that we can move around the map, some things may feel a little off. The camera doesn't move very smoothly. Select the `PlayerCamera` node, go to the inspector, find "∨Position Smoothing" and click the box for "Enabled".

Now go to the script attached to `Player` and change `SPEED` to `130.0` and `JUMP_VELOCITY` to `-300.0`

Test the game again to make sure things feel nice.

## Platforms

A *platform* in a 2D platformer is a part of the level where the player can jump onto them from the bottom, and land on the top. Godot has this functionality built in. Some platforms also move. Godot makes this simple as well.

### Static Platforms

Create a new scene my clicking on the plus sign "+". at the top of the editor where the tabs are. Click on the "Other Node" button in the "Scene" section, search for and add "AnimatableBody2D" as the root node. Rename it to "Platform". Let's give this platform some graphics. Add a child node to the root called "Sprite2D" and rename it to "PlatformSprite". In the inspector, find the "Texture" property, you'll see "\<empty\>". Go to the "FileSystem" section, go inside the "assets" folder and the "sprites" folder. Drag "`platforms.png`" into that "\<empty\>" section. You'll see that this too is a sprite-sheet with multiple platform graphics, we only want one. Back in the inspector, find the drop-down labeled "∨Region", inside check the "Enabled" property, then click on the "Edit Region" button. An editor window will pop up. Inside, on the top-left change the "Snap Mode:" to "Pixel Snap". Now, create a box around the top-right green platform and click "Close".

Add a child node to the `Platform` node called "CollisionShape2D" and rename it to "PlatformHitbox. Make the "Shape" a rectangle and fit it to the art.

Save this scene with `Ctrl+S`, go back to the `MainGame` scene, and drag a `Platform` scene into the level above the knight's head.

Test the game. You should be able to jump on to it from the side, but you'll bump your head if you try to jump onto it from below.

Go back to the `Platform` scene, select the "PlatformHitbox" node, and look to the inspector. Click the "On" check-box for the "One Way Collision" property. You should now be able to pass through the bottom, and stand on the top.

One problem though, is the knight goes behind the platform when they intersect. This is because, by default, Godot draws everything in order of the scene tree. We don't want to have to move everything in the scene tree to fix this, so instead we will use something called *Z Index*. Go the the `Player` scene, select the root `Player` node, and look to the Inspector. Under "CanvasItem" look for "∨Ordering". Click on it to reveal more properties. Change "Z Index" from 0 to "5".

Test this again and the knight should now go in front of the platform.

### Moving Platforms

Drag another `Platform` scene into the level, right-click on it, and add a child node called "AnimationPlayer" and rename it to "PlatformMover".

Click back on the `Platform2` node and look to the inspector. Find "∨Transform", inside, you'll see "Position". To the right of the number box you'll see a symbol of a key; click on it. Click the "Create" button on the pop-up window.

A small white diamond should now be added to the animation timeline at the bottom of the editor. This is called a *keyframe*. Let's add another one at the end of the timeline. Drag the blue marker to the end of the timeline. Now, drag the platform to the right while holding the `Shift` key to lock the movement to a single axis. Once you have it where you'd like it to stop before heading back to where it started, go back to the key symbol in the Inspector. Click it to add another keyframe. Press the play button in the "Animation" section and you should see the platform move from its first keyframe to its second, then stop. Of course, we don't want it to stop. Look to the top-left of the "Animation" section and you should see a button with two arrows making a loop "🗘"; click this button. Now the platform will move from the first keyframe to the second, then snap back to the first. Click that button again to enable "ping-pong" mode; this is what we want.

Depending on how far the two position keyframes are from each other, the platform may be moving too fast. We can slow things down by increasing the timeline. By default, it is one second. Next to the button we used to make the animation ping-pong is the box to edit the total time of the timeline. Change it from 1 to "1.5",  then drag the second keyframe to the end of the timeline. The platform should now be a little slower.

Finally, let's get the animation to play as soon as the platform is loaded into the scene be clicking on the autoplay button next to the "Edit" button.

## Pickups

Let's create a coin pickup. Just like every new object, this will be a new scene.

Create a new scene and make the root node an "Area2D" node. This allows us to create a hitbox that we can use to code all kinds of interactive behavior, such as increasing our score.

Rename the root node to "Coin",  then add an "AnimatedSprite2D" child node. Go through the same process of adding sprite-frames as we did with the player, but using the `coin.png` sprite-sheet. Now add a "CollisionShape2D" child node to the root node, and create a circle shape that matches the graphics of the coin. Save this scene with `Ctrl+S` and go back to the `MainGame` scene.

Drag a few coins on to the level and test the game. The coins won't do anything when you walk into them, but you should see them and they should be animated.


