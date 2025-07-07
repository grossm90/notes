## What is a Space Shooter?

A space shooter, sometimes called a Shmup (short for shoot-em-up), is a video game where the player controls a ship on one end of the screen, and enemies spawn in on the opposite end. As the enemies move toward the player's ship, the player can shoot the enemies to clear them out. Sometimes the enemies fire at the player. Often, the enemies spawn at the top of the screen and the player is at the bottom, but some shmups have the player on the left side of the screen, with the enemies spawning in on the right.

## Why Make a Space Shooter?

A space shooter is a great project to work on next as it will introduce a few new game mechanics that are crucial to learning game development. We'll learn to move a player character left and right with the arrow keys, spawn enemies and get them to move, and we'll learn how to get the player character to shoot a laser and destroy enemies. On top of all these new skills, we can work on the skills we learned previously, such as creating a score that goes up when we eliminate an enemy.

## What will this Game Teach Me?

The new game mechanics we will learn with this lesson are:

-   Drawing sprites
-   Basic player controls (Left, Right, & Shoot)
-   Enemy spawning
-   Enemy movement
-   Using random values to affect game-play
-   Projectiles and collision

## Let's Get Started

As always, we'll start with the initial setup.

```lua
function _init()
end

function _update()
end

function _draw()
  cls()
end
```

Before we move on to creating the first features, it's worth thinking about where you would start if you weren't following a guide. Would you create the player's ship first? Or the enemies? There is no right or wrong answer, but you will develop preferences as you become a better programmer. It is important to think about these things, even when following guides, because one of the hardest things about becoming a better developer, is taking the leap to creating your own projects without a guide. When you follow guides, you should always be thinking "_How could I do this differently?_". It will make the transition to programming without a guide much smoother.

## The Player Ship

There are two ways to draw objects to the PICO-8 screen; simple shapes like lines and rectangles, and **sprites**. A sprite is a 2d image that can be imported into a scene. Sprites are often grouped together on a **sprite sheet**. In many game engines, sprite sheets must be created in a separate art program like _Photoshop_ or _Clip Studio Paint_. Luckily, PICO-8 has a sprite sheet and sprite editor built directly into the engine. If we look at the top-right of the editor, we'll see five icons. So far, we've only used the text-editor, which is represented by the left-most icon; a pair of parenthesis `()`. We're now going to switch to the sprite editor which is the next one over to the right, and is represented by a face.

The sprite editor is fairly simple. On the top-left is the canvas where we will draw our sprites. The top-right is the pallet where we change colors. On the bottom is the sprite sheet. Sprites are eight pixels wide and 8 pixels tall (an eight pixel square). If we look at the top-left of the sprite sheet, we'll see the first slot is taken by a white X. We'll leave that alone for now and click on the slot to the right of that. The number just above the sprite sheet should be "001".

### Drawing the Player Ship

We'll now draw a space ship in this slot of the sprite sheet. Notice that whatever we draw on the canvas will show up in the sprite sheet. It doesn't matter what your ship looks like, but it will be important that we draw it so it takes up the full width of the canvas.

Once we're done drawing, we're going to go back over to the code editor, and under the `cls()` function to clear the screen, we will import our ship with a new function `spr()`, short for "sprite". `spr()` takes in three mandatory parameters; the sprite number, an 𝑥 position, and a 𝑦 position. This function will draw the sprite of the number we choose at the 𝑥 and 𝑦 position that we choose. One important thing to note:

> **A sprite's (𝑥, 𝑦) is its top-left corner**

So, if try to place our new ship at the top-left of the screen (0,0) by writing `spr(1,0,0)`, we'll be able to see the whole thing, but if try to draw it at the top-right of the screen (127,0) by writing `spr(1,127,0)`, we'll only see the left column of pixels that make up our sprite. If we only see one column of our eight-pixel wide sprite, how many columns are not showing? Of course, the answer is seven. So to see the whole thing, we need to move the ship to the left by seven pixels by actually writing `spr(1,120,0)`. Now we see the whole thing!

We want the player ship on the bottom though, the top will be for the enemies. What (𝑥, 𝑦) values should be type into the `spr()` function to get the ship on the bottom-middle? To get the ship in the middle of the screen, we need to divide the width of the screen by two (127/2 = 63). To get the ship at the bottom we need to subtract seven from the total height of the screen like we did when we tried to place it on the right side. Our finial writing of the function will look like this: `spr(1,63,120)`.

```lua
function _init()
end

function _update()
end

function _draw()
  cls()
  spr(1,63,120)
end
```

Looks great!

### Moving the Player Ship

Our ship looks great, but it is not very exciting because it can't move.

Let's get the player ship to move left and right with the arrow keys. To do this, we have to replace the 𝑥 location in the `spr()` function with a variable. We'll move the function over to a new tab for all of the player ship code and replace it with a custom function we'll call `draw_player()`

```lua
-- tab 0 main
function _init()
end

function _update()
end

function _draw()
  cls()
  draw_player()
end
```

```lua
-- tab 1 player
player_x = 63

function draw_player()
  spr(1,player_x,120)
end
```

We moved things around, but nothing should change when we re-run the code.

Now, we'll add a custom function for moving the player called `update_player()`. This will be very similar to how we checked for button presses in the previous lessons, except we need to check for the LEFT ARROW which has a key code of `0` and the RIGHT ARROW which has a key code of `1`.

```lua
-- tab 1 player
player_x = 63

function update_player()
  if btn(0) then
    player_x = player_x - 1
  elseif btn(1) then
    player_x = player_x + 1
  end
end
function draw_player()
  spr(1,player_x,120)
end
```

And we'll call this new function in tab 0 inside `_update()`.

```lua
-- tab 0 main
function _init()
end

function _update()
  update_player()
end

function _draw()
  cls()
  draw_player()
end
```

When we run this code, we can move left and right. Pretty cool! Let's add some lasers!

### Firing Lasers!

We'll have the O button (Z on the keyboard) fire some lasers. Remember that the O button has a keycode of `4`. The lasers will really just be some green lines that that go from the ship to the top of the screen. We've already done code for checking button presses and drawing lines, so this should be fairly simple for us.

```lua
-- tab 1 player
player_x = 63

function update_player()
  if btn(0) then
    player_x = player_x - 1
  elseif btn(1) then
    player_x = player_x + 1
  end
end

function draw_player()
  spr(1,player_x,120)
  player_shoot()
end

function player_shoot()
  if btn(4) then
    line(
      player_x,
      0,
      player_x,
      120)
  end
```

Looking good, but that's only one laser, let's do the other one too.

```lua
-- tab 1 player
player_x = 63

function update_player()
  if btn(0) then
    player_x = player_x - 1
  elseif btn(1) then
    player_x = player_x + 1
  end
end

function draw_player()
  spr(1,player_x,120)
  player_shoot()
end

function player_shoot()
  if btn(4) then
    line(
      player_x,
      0,
      player_x,
      120)

    line(
      player_x + 7,
      0,
      player_x + 7,
      120)
  end
```

Awesome! But a little boring with no enemies to shoot.

## Enemies

Let's add some UFOs for our spaceship shoot!

### Drawing the Enemies

We'll go back to the sprite editor and click on the square to the right of our spaceship sprite on the sprite sheet. This should be sprite number 2. Again, it doesn't really matter what this looks like, so don't be afraid to be creative. When we're finished, we'll go back to the code editor and create the code to get them to spawn in.

Let's create a new tab for the enemies, and create a custom `draw_enemies()` function that draws our new sprite at the top of the screen.

```lua
-- tab 2 enemies
function draw_enemies()
  spr(2, 63, 0)
end
```

And we'll call it in the main tab in `_draw()`

```lua
-- tab 0 main
function _init()
end

function _update()
  update_player()
end

function _draw()
  cls()
  draw_player()
  draw_enemies()
end
```

Great! But, the enemy doesn't move and doesn't get eliminated when shot. Let's get it moving first.

### Enemy Movement

To get the enemy to move we'll need to change both its 𝑥 _and_ 𝑦 position values to variables, as the enemies will need to move side-to-side (𝑥), and down (𝑦).

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0

function draw_enemies()
  spr(2, enemy_x, enemy_y)
end
```

Now we need an `update_enemies()` function to get it moving. We'll just make the UFO go down for now, using the same method we used last lesson to get the obstacles to move.

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0

function update_enemies()
  enemy_y = enemy_y + 1
end

function draw_enemies()
  spr(2, enemy_x, enemy_y)
end
```

Cool! Let's get the UFO to move side-to-side now. First, we'll create a variable for the speed the UFO will move side-to-side. We can call this `enemy_speedx`, and we'll set it to `1`. We'll also update the UFOs 𝑥 position using this variable.

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0
enemy_speedx = 1

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx
end

function draw_enemies()
  spr(2, enemy_x, enemy_y)
end
```

Pretty cool, but the UFO only moves to the right.

Now, **randomly**, we want the UFO to reverse its direction. How will we do this? Well, its current direction is to the right, and this is because `enemy_speedx` is positive 1. To get it to move to the left, we need to change this to negative 1.

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0
enemy_speedx = -1

function update_enemies()
  enemy_y = enemy_y - 1
  enemy_x = enemy_x + enemy_speedx
end

function draw_enemies()
  spr(2, enemy_x, enemy_y)
end
```

Alight, but now we have the opposite problem, the UFO only moves left. We need to find a way to get `enemy_speedx` to be `-1` sometimes, and `1` other times, and for this change to happen randomly and automatically. To do this, we'll generate a random number, and create an `if` statement that uses this random number to go back and forth between `-1` and `1`. To do this we'll introduce a new function, `rnd()`, short for random, that will generate a random number between zero and any number we use as a parameter.

We'll generate a random number between 0 and 9 and check if that number is less than 1. This gives us a ten percent chance of the statement being `true` every frame. If it is `true`, we'll switch between `-1` and `1` by multiplying the value by `-1`.

> **Important: We do this _a lot_ in game programming. To get a number to switch between positive and negative, multiply it by -1.**

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0
enemy_speedx = -1

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx

  if rnd(10) < 1 then
    enemy_speedx = enemy_speedx * -1
  end

end

function draw_enemies()
  spr(2, enemy_x, enemy_y)
end
```

This looks really good! Let's move on to removing the enemy if we hit it with our lasers.

### Eliminating Enemies

We'll start this with some setup by creating a variable called `enemy_alive` and we'll set it to `true`. This is the first time we're setting a variable to something other than a number, here we're setting it to a **boolean**. We'll also wrap the `spr()` function in an `if` statement that will only draw the UFO if it is alive.

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0
enemy_speedx = -1
enemy_alive = true

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx

  if rnd(10) < 1 then
    enemy_speedx = enemy_speedx * -1
  end

end

function draw_enemies()
  if enemy_alive then
    spr(2, enemy_x, enemy_y)
  end
end
```

If we re-run this code, nothing should change.

Now, we need to write some code that checks if the enemy touches our laser, and sets `enemy_alive` to `false` if it does. The check for this will be pretty simple, because the lasers are just lines that zap the entire column above our ship, all the way to the top of the screen. So, if any part of the enemy is above our ship when we fire the lasers, we've hit the enemy. How do we translate this into code?

Remember the important thing about a sprite's 𝑥, 𝑦 location? _A sprite's (𝑥, 𝑦) is its top-left corner_. Now, it's 𝑦 location doesn't matter because the laser zaps the entire height of the screen, so we only need to worry about the 𝑥 locations.

Let's imagine that `player_x` is set to `60` and `enemy_x` is also `60`. This would mean that the enemy and the player are perfectly aligned, one on top of the other. All eight pixels align. If the enemy moves one pixel to the right, `enemy_x` would then be set to `61`. In this case , every pixel of the enemy would be directly above the player except for its right-most column of pixels. Seven of the enemies pixels align and one does not. If the enemy moves another pixel to the right, `enemy_x` would be set to `62`. Six of its pixels would align with the player and two would not. If we keep going this way until `enemy_x` is set to `67`, then one pixel would be aligned and seven would not. Finally, if `enemy_x` is `68` none of the enemy's pixels would align with the player's. So in code, we could write something like `if enemy_x < player_x + 8 then`. But that's only true in one direction. The enemy's pixels still align with the player when it moves to the left too, from `59` to `53` and is not aligned at `52` in this example. So we have to update the code to say `if enemy_x < player_x + 8 and enemy_x > player_x - 8 then`. But that's really long and hard to read. Is there a better way? Of course there is! If we subtract `enemy_x` from `player_x` and get the **absolute value**, we only have to check if that result is less than eight. We'll use the `abs()` function to get the absolute value.

```lua
-- tab 2 enemies
enemy_x = 63
enemy_y = 0
enemy_speedx = -1
enemy_alive = true

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx

  if rnd(10) < 1 then
    enemy_speedx = enemy_speedx * -1
  end

  if btnp(4) then
    if abs(player_x - enemy_x) < 8 then
      enemy_alive = false
    end
  end
end

function draw_enemies()
  if enemy_alive then
    spr(2, enemy_x, enemy_y)
  end
end
```

If we run the code now, the UFO should disappear when we hit it with our lasers. Pretty cool!

### More Enemies!

In the previous lesson, we create two obstacles by literally re-writing the same code for both of them, except for their 𝑦 locations. That's fine if we only want two, but shooter games like the one we're making can have hundreds, or even thousands of enemies. We can't re-write the code for drawing and updating each one individually. Thankfully, we can re-use code in programming. One way to re-use code in programming is through the use of something called an **array**. An array is a group of data stored in a list. There are a few names you may hear associated with arrays in programming; arrays, lists, and tables. There are some differences between these terms, but for now, think of them all as being a group of data. PICO-8 uses the term **table** for this, so that's what we'll use from now on.

Creating a table is as simple as creating a variable, but we just have to add some **curly brackets** `{}`. We'll create an empty table now, called `enemies` that we will fill with the data for our enemies in a moment.

```lua
-- tab 2 enemies
enemies = {}
enemy_x = 63
enemy_y = 0
enemy_speedx = -1
enemy_alive = true

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx

  if rnd(10) < 1 then
    enemy_speedx = enemy_speedx * -1
  end

  if btnp(4) then
    if abs(player_x - enemy_x) < 8 then
      enemy_alive = false
    end
  end
end

function draw_enemies()
  if enemy_alive then
    spr(2, enemy_x, enemy_y)
  end
end
```

And like that, we created our first table. Pretty simple!

Now, we need to convert the data for our enemies from separate variables to a table, then add that data to the enemies table. We'll use the `add()` function to do this. This function takes in two parameters. The first parameter is the table that we'd like to add our data to, and the second parameter is the data we want to add; in this case, another table with all the variables that control the enemies.

```lua
-- tab 2 enemies
enemies = {}

add(enemies, {x = 63,
  y = 0,
  speedx = -1,
  alive = true})

enemy_x = 63
enemy_y = 0
enemy_speedx = -1
enemy_alive = true

function update_enemies()
  enemy_y = enemy_y + 1
  enemy_x = enemy_x + enemy_speedx

  if rnd(10) < 1 then
    enemy_speedx = enemy_speedx * -1
  end

  if btnp(4) then
    if abs(player_x - enemy_x) < 8 then
      enemy_alive = false
    end
  end
end

function draw_enemies()
  if enemy_alive then
    spr(2, enemy_x, enemy_y)
  end
end
```

At first glance, this will seem very complex, so let's break this down. We started by creating an empty table called `enemies`. Then we use the `add()` function to add a new table into the `enemies` table. This only happens in the computer's memory, we don't see it in the code, but it is important to know what this would look like so we can mentally picture it as we code. Here is what the `enemies` table looks like after our `add()` function runs:

`enemies = {{x = 63, y = 0, speedx = -1, alive = true}}`

Here we can see that we have a table inside the `enemies` table (notice that there are now two curly brackets at the beginning and end).

Now, lets update how we draw and update our enemy using this new table method. We'll delete the individual variables, and replace the references to them with references to the table. To do this, we need to know how to access variables in a table. We first write the name of the table, then square brackets `[]`, in the square brackets we write the index number that we'd like to reference. There's only one enemy in our `enemies` table right now, so the index number will be `1`. Finally, we add a dot `.` and the name of the variable we'd like to reference. So, to reference the first enemy's `x` variable, we write `enemies[1].x`.

Let's update our code to match this format.

```lua
-- tab 2 enemies
enemies = {}

add(enemies, {x = 63,
  y = 0,
  speedx = -1,
  alive = true})

function update_enemies()
  enemies[1].y = enemies[1].y + 1
  enemies[1].x = enemies[1].x + enemies[1].speedx

  if rnd(10) < 1 then
    enemies[1].speedx = enemies[1].speedx * -1
  end

  if btnp(4) then
    if abs(player_x - enemies[1].x) < 8 then
      enemies[1].alive = false
    end
  end
end

function draw_enemies()
  if enemies[1].alive then
    spr(2, enemies[1].x, enemies[1].y)
  end
end
```

If we run this, nothing should change, but we can now add more enemies really easily. Let's add two more, one to the left of and one to the right of our first enemy.

```lua
-- tab 2 enemies
enemies = {}

add(enemies, {x = 31,
  y = 0,
  speedx = -1,
  alive = true})

add(enemies, {x = 63,
  y = 0,
  speedx = -1,
  alive = true})

add(enemies, {x = 94,
  y = 0,
  speedx = -1,
  alive = true})

function update_enemies()
  enemies[1].y = enemies[1].y + 1
  enemies[1].x = enemies[1].x + enemies[1].speedx

  if rnd(10) < 1 then
    enemies[1].speedx = enemies[1].speedx * -1
  end

  if btnp(4) then
    if abs(player_x - enemies[1].x) < 8 then
      enemies[1].alive = false
    end
  end
end

function draw_enemies()
  if enemies[1].alive then
    spr(2, enemies[1].x, enemies[1].y)
  end
end
```

Again, running this won't change anything, even though there are two more enemies in the `enemies` table. This is because we didn't add more references to these new enemies. Notice all of the `[1]`s? We need copies of all of those that also say `[2]` and `[3]`, but that would be a lot of re-written code. I said earlier that tables were supposed to help us _not_ re-write code. Well, that's because we need to learn one more programming technique, **loops**. A loop runs code multiple times, and includes a built-in index number that goes up every time the loop wraps back to the top. You'll see the importance of this in a moment.

To create a loop in PICO-8, we write `for i=1,3 do`, then we write the code we want to repeat under, and finish with `end` just like with functions and `if` statements. the number before the comma is the number the index starts with, and the number after the comma is the one it ends with. So in the example, we'll be repeating three times, using the numbers 1, 2, and 3 as our index. This makes sense, because we have three enemies in the table `enemies[1]`, `enemies[2]`, `enemies[3]`. Notice the `i` in the example? This is the variable that holds the index number. So all we have to do to get this to work, is replace all of the `[1]`s with `[i]`s.

```lua
-- tab 2 enemies
enemies = {}

add(enemies, {x = 31,
  y = 0,
  speedx = 1,
  alive = true})

add(enemies, {x = 63,
  y = 0,
  speedx = -1,
  alive = true})

add(enemies, {x = 94,
  y = 0,
  speedx = -1,
  alive = true})

function update_enemies()
  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
      end
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

Beautiful! But we can do even better. See where we add our three enemies to `enemies` table? That can be a loop too. Because each enemy is 31 pixels apart from one another, we can use the index number from the loop by multiplying by 31 to get our `x` variable for each enemy. 1 \* 31 = 31, 2 \* 31 = 62, 3 \* 31 = 93.

```lua
-- tab 2 enemies
enemies = {}

for i=1,3 do
  add(enemies, {x = i*31,
    y = 0,
    speedx = 1,
    alive = true})
end

function update_enemies()
  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
      end
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

Let's use the same strategy to space the UFOs out vertically, every 16 pixels. We'll also start the first enemy just off the screen by setting its `y` variable to -16.

```lua
-- tab 2 enemies
enemies = {}

for i=1,3 do
  add(enemies, {x = i*31,
    y = i*-16,
    speedx = 1,
    alive = true})
end

function update_enemies()
  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
      end
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

That looks really good! Let's wrap this up by adding a score and a game-over screen.

### Score

We've done score many times now, so this should be easy Any time an enemy is zapped, we add one to a `score` variable, and we'll print that variable. We'll go back to tab 0 to declare the variable and print it.

```lua
-- tab 0 main
function _init()
  score = 0
end

function _update()
  update_player()
end

function _draw()
  cls()
  draw_player()
  draw_enemies()
  print("score: " .. score, 7)
end
```

Now in tab 2, we can add the code to increase the score when we eliminate an enemy. But, we only want to increase the score if we hit a UFO when it is alive, so we'll have to check for that too.

```lua
-- tab 2 enemies
enemies = {}

for i=1,3 do
  add(enemies, {x = i*31,
    y = i*-16,
    speedx = 1,
    alive = true})
end

function update_enemies()
  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) and enemies[i].alive then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
        score = score + 1
      end
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

Awesome! Let's do the game-over screen now.

## Game-Over

This game will end if the player has eliminated all of the enemies, or if an enemy makes it past the player. First we need to go back to tab 0 and create a variable that will keep track of the **game state**. It'll be set to `"playing"` or `"game-over"`, depending on the current state of the game. We'll also wrap any code that we only want to run during regular game-play in an `if` statement that checks the game state.

```lua
-- tab 0 main
function _init()
  score = 0
  game_state = "playing"
end

function _update()
  if game_state == "playing" then
    update_player()
  end
end

function _draw()
  cls()
  if game_state == "playing" then
    draw_player()
    draw_enemies()
  end
  print("score: " .. score, 7)
end
```

In tab 2, we'll check if one of the UFOs goes past the bottom of the screen, and if it does, we'll set `game_state` to `"game_over"`.

```lua
-- tab 2 enemies
enemies = {}

for i=1,3 do
  add(enemies, {x = i*31,
    y = i*-16,
    speedx = 1,
    alive = true})
end

function update_enemies()
  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) and enemies[i].alive then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
        score = score + 1
      end
    end

    if enemies[i].y > 127 and enemies[i].alive then
      game_state = "game-over"
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

This looks great, but when the game is over, everything just disappears. Let's show a game-over message.

```lua
-- tab 0 main
function _init()
  score = 0
  game_state = "playing"
end

function _update()
  if game_state == "playing" then
    update_player()
  end
end

function _draw()
  cls()
  if game_state == "playing" then
    draw_player()
    draw_enemies()
  elseif game_state == "game-over" then
    print("game-over", 50, 58, 7)
  end
  print("score: " .. score, 7)
end
```

Finally, we'll check if the `score` variable is greater than `2`, and set `game_state` to `"game-over"`, because if it is, the player eliminated all of the enemies.

```lua
-- tab 2 enemies
enemies = {}

for i=1,3 do
  add(enemies, {x = i*31,
    y = i*-16,
    speedx = 1,
    alive = true})
end

function update_enemies()
  if score > 2 then
    game_state = "game-over"
  end

  for i=1,3 do
    enemies[i].y = enemies[i].y + 1
    enemies[i].x = enemies[i].x + enemies[i].speedx

    if rnd(10) < 1 then
      enemies[i].speedx = enemies[i].speedx * -1
    end

    if btnp(4) and enemies[i].alive then
      if abs(player_x - enemies[i].x) < 8 then
        enemies[i].alive = false
        score = score + 1
      end
    end

    if enemies[i].y > 127 and enemies[i].alive then
      game_state = "game-over"
    end
  end
end

function draw_enemies()
  for i=1,3 do
    if enemies[i].alive then
      spr(2, enemies[i].x, enemies[i].y)
    end
  end
end
```

And there's our game!

## Final Thoughts

_Phew!_ That was a lot of work and a lot of new concepts. Let's recap them real quick. We learned how the sprite editor and sprite sheet works. We learned how to draw sprites to the game screen and get them to move with the arrow keys and how to get them to move using random numbers. We learned how to create lasers and use a button to fire them. We learned how to stop drawing sprites to the screen if it gets hit by a laser. Finally, we learned how to use loops and tables to re-use code, saving us time and lines of code.

As always, keep in mind the two very important questions we ask our self after every lesson.

1. How can I use what I learned in previous lessons to make this game better?
2. How can I use what I learned in previous lessons and this lesson to make different games?
