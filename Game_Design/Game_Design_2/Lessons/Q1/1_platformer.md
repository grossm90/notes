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

At the very top-left of the screen, find the "Project" menu and select "Project Settings...". Under "∨ Rendering", select "Textures". Change "Default Texture Filter" from Linear to "Nearest", and then close the window. The art should look much more crisp. Select the `PlayerSprite` from the node tree if it isn't already select to re-open the "SpriteFrames" window at the bottom of the screen. To preview the animation, click on the play button "▶" in the "Animation Frames:" toolbar. The knight should bounce up and down. It's a little slow though. Let's speed up the animation by changing the "Animation Speed" setting under "Animations:" from 5 to "10". The animation should play a little faster now.

With the animation out of the way, let's move on to hitbox.

### Adding a Hitbox to the Player Scene