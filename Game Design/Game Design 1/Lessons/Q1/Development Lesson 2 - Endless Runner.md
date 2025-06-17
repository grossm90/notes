## What is an Endless Runner?

An **Endless Runner** is a game where the **player character (PC)** moves automatically through a level and the player must react to obstacles in the path. Examples include _Temple Run_, _Subway Surfers_, and Google Chrome's _Dinosaur Game_. The goal of this type of game is to go as far as possible, and beat your own, other's high score.

## Why make an Endless Runner?

An Endless runner is a great game to make for our next lesson because we have learned many of the game mechanics required in our last lesson (button interaction, score, high score, and timer). We can use the Endless Runner genre to extend these skills with new game mechanics that build on the ones we already learned.

## What will this Game Teach Me?

The new game mechanics we will learn with this lesson are:

-   Drawing shapes to the screen (lines and rectangles)
-   Moving objects on screen
-   Basic player controls (jump and duck)
-   Collision

## Let's Get Started

We'll need to get used to writing the initial game loop, as every PICO-8 game we make will start with this.

```lua
function _init()
end
function _update()
end
function _draw()
  cls()
end
```

The next good habit to get into when starting a new game file is to think of the first variables that will need to be created. This will be a little tricky when you are new, but, as with any skill, you will improve with time and practice.

Every game that has a score will need a `score` and a `high_score` variable. so let's add those now to `_init()`

```lua
function _init()
  score = 0
  high_score = 0
end
function _update()
end
function _draw()
  cls()
end
```

## Code Organization

Though it may not have seemed like it, the clicker game we made in the last lesson was a small amount of code. Even simple games take a lot of code to complete. For this reason, going forward, we will implement a few strategies for keeping our code organized. These strategies are:

-   Writing Comments: comments are notes that are written in the code, but ignored when the code is run.
-   Using Tabs: many code editors have tabs that can keep code organized by what it does instead of writing all of the code in one long file.
-   Writing Custom Functions: we've used a few functions written for PICO-8, but we can create our own functions so we don't have to write repetitive code.

We'll start organizing our code by opening a new tab where we'll write all the code for the player character. On the top-left of PICO-8's code editor screen, we'll click the little plus sign `+` to open a new tab. We'll label this tab with a comment at the top so we know what code lives here.

```lua
-- tab 1: player character
```

## The Player Character

What variables does the PC need? The player will simply be a line that can jump and squish down to duck. In PICO-8, a line is drawn by designating two coordinates for its start and two coordinates for its end, using the screen coordinates we discussed in Development Lesson 0. Let's create the `player_x`, and `player_y` variables for describing the player character's position. We'll choose 8 for `player_x ` to create an 8-pixel gap between the left side of the screen and the player character. We'll choose 103 for `player_y` this creates an 8-pixel tall gap under the PC, because the PC will be 16 pixels tall (127 - 8 - 16 = 103).

```lua
-- tab 1: player character
player_x = 8
player_y = 103
```

Now we'll create our first custom function! This function will draw our PC, we'll name it `draw_player()`, and it will not take in any arguments. All this function will do is draw a line that uses the PC's variables to designate the top of the line, and the bottom of the line will be sixteen pixels lower than its top. In other words, our PC will be a 16 pixel tall vertical line. You may notice, like last lesson, we are putting each argument for the `line()` function on its own line (pressing the ENTER key after each comma). This is totally normal, and the code won't be read any differently than if it was all on one line, but it does make it much more readable on PICO-8's small screen.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end
```

Beautiful! Now, whenever we want to draw the PC, we don't have to rewrite all of that. Instead, we just type `draw_player()`. Let's do that now, back in tab 0, just after we clear the screen with `cls()`.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
end
function _draw()
  cls()
  draw_player()
end
```

Now, if we run the code with CTRL + R, we should see a green line near the bottom-left of the screen.

### Jump Function

Let's get our little line to jump. We'll start very simple and define a "jump" as making the PC's `player_y` variable 16 pixels higher on the screen than normal, and we'll control this with the X button. In other words `if` the player presses X button, `then` set `player_y` to 87, `else` set `player_y` to 103. Why 87 (16 pixels less then 103) and not 121 (16 pixels more)? **_Remember that 𝑦 gets smaller as we go up the screen so we have to subtract if we want to go up_**.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end

function move_player()
  if btn(5) then
    player_y = 87
  else
    player_y = 103
  end
end
```

And we'll call that function in tab 0:

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
end
function _draw()
  cls()
  draw_player()
end
```

Great! The PC goes up when we hold the X button and goes back down when we let go. This isn't perfect. It's more of a teleport than a jump, but we can make this more realistic later. Remember, we always want to create an MVP before adding complexity.

## Obstacles and the Illusion of Movement

Game development is full of creating illusions. We often have to "cheat" or take little "shortcuts" to get the desired effect. The key point is, as long as the player doesn't notice, we can "cheat" all we want!

In a lot of games where the PC moves to the right (such as many Endless Runners and Platformers), the PC isn't actually moving at all. Instead, the map, objects, and enemies move to the left. That is what we'll do here. Let's start by opening a new tab where all the code for the obstacles will go, and we'll create some variables there. This game will have a low obstacle that the player will have to jump over and a high obstacle that the player has to duck under. We'll start with the low obstacle.

We'll give the obstacle a `low_x` variable of 127 so it starts on the opposite side of the screen as the player character. This will give the player plenty of time to react to the obstacle. We'll give the obstacle a `low_y` variable of 111. This will start the line 16 pixels above the bottom of the screen, it'll be 8 pixels tall, and have an 8 pixel tall gap from the bottom of the screen (127 - 8 - 8 = 111).

```lua
-- tab 2: obstacles
low_x = 127
low_y = 111
```

Now, we'll create a function to draw the obstacle similar to how we drew the player.

```lua
-- tab 2: obstacles
low_x = 127
low_y = 111

function draw_obstacles()
  line(
    low_x,
    low_y,
    low_x,
    low_y + 8,
    8)
end
```

Now, we'll make a function for it to constantly move left by subtracting one from its 𝑥 every frame.

```lua
-- tab 2: obstacles
low_x = 127
low_y = 111

function draw_obstacles()
  line(
    low_x,
    low_y,
    low_x,
    low_y + 8,
    8)
end

function move_obstacles()
  low_x = low_x - 1
end
```

And we'll put both in tab 0.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
end
```

Awesome! The obstacle moves left and we can even jump over it. Unfortunately, nothing happens if we hit it.

## Simple Collision

Creating code to detect if two objects collide can be very tricky, but, as always, we'll start as simple as possible, then introduce more complex techniques later.

Let's go back to tab 1 where we write code for the PC. Here, we'll create a function called `collision()` that will check if we hit the low obstacle (and eventually high obstacle too). But what does it mean for two objects to "collide"? In this case, the PC collided with the obstacle `if` their 𝑥 values are the same, `and` the PC is `not` jumping.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end

function move_player()
  if btn(5) then
    player_y = 87
  else
    player_y = 103
  end
end

function collision()
  if player_x == low_x
    and not btn(5) then
    low_x = 119
  end
end
```

Lets add this function to tab 0 and test it out.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
end
```

Great! If the obstacle hits the player, it teleports back to its starting location, but if we jump over it, it keeps going forever. This isn't exactly what we want, but it's a great step in the right direction.

Let's tighten this up a little by having the obstacle start just off the right side of the screen and if we successfully jump over it, it will teleport when it leaves the left side of the screen.

```lua
-- tab 2: obstacles
low_x = 128
low_y = 111

function draw_obstacles()
  line(
    low_x,
    low_y,
    low_x,
    low_y + 8,
    8)
end

function move_obstacles()
  low_x = low_x - 1
  if low_x < 0 then
    low_x = 128
  end
end
```

Nice! Remember that the screen is 128 pixels wide, but the right-most pixel is 127 because we start counting the left-most pixel as 0, so starting and teleporting the obstacle by setting its `low_x` variable to 128 will indeed move it off of the screen.

Let's create a high obstacle to duck under now.

## A High Obstacle

Now that we've done most of the hard work, creating a high obstacle should be a piece of cake. We'll start again with some variables that describe the location. We'll create a `high_x` variable that will get a value of 192. This is the initial value of `low_x`, 128, plus 64. 64 is a number we will see a lot in PICO-8, because it is half the length of the screen (128/2 = 64). This will create a gap between our two obstacles that is one half the size of the screen. We'll also create a `high_y` variable that will get a value of 103. This is so the line will start at the same height as the player.

```lua
-- tab 2: obstacles
low_x = 128
low_y = 111

high_x = 192
high_y = 103

function draw_obstacles()
  line(
    low_x,
    low_y,
    low_x,
    low_y + 8,
    8)
end

function move_obstacles()
  low_x = low_x - 1
  if low_x < 0 then
    low_x = 128
  end
end
```

And we'll recreate the code that moves and draws the low obstacle, but we'll tweak them to work with our new variables.

```lua
-- tab 2: obstacles
low_x = 128
low_y = 111

high_x = 192
high_y = 103

function draw_obstacles()
  line(
    low_x,
    low_y,
    low_x,
    low_y + 8,
    8)
    
  line(
    high_x,
    high_y,
    high_x,
    high_y + 8,
    8)
end

function move_obstacles()
  low_x = low_x - 1
  if low_x < 0 then
    low_x = 128
  end
end

function move_high()
  high_x = high_x - 1
  if high_x < 0 then
    high_x = 128
  end
end
```

And update tab 0.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
end
```

Let's also update the `collision()` function.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end

function move_player()
  if btn(5) then
    player_y = 87
  else
    player_y = 103
  end
end

function collision()
  if player_x == low_x
    and not btn(5) then
    low_x = 128
  end

  if player_x == high_x
    and not btn(4) then
    high_x = 128
  end
end
```

There's no need to update tab 0 this time as we did not make any new functions.

So now there's a high obstacle, but we can't avoid hitting it! Let's add in the ability to duck.

## Duck Function

Ducking will be similar to jumping, but we will squish the line a bit. When people jump, they stretch their bodies out, but when they duck, they ball up and look smaller. That will be the visual effect we are trying to achieve here (the PC is just a line, so we'll definitely be using our imagination). We'll take the `player_y` variable and increase it by 12 to make the line appear shorter.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end

function move_player()
  if btn(5) then -- jump
    player_y = 87
  elseif btn(4) then -- duck
    player_y = 115
  else
    player_y = 103
  end
end

function collision()
  if player_x == low_x
    and not btn(5) then
    low_x = 128
  end

  if player_x == high_x
    and not btn(4) then
    high_x = 128
  end
end
```

Okay... the player character isn't really "ducking" so much as "going through the floor". There are a few fixes we can use, but we'll, again, take a little shortcut. We won't be able to see the line dip through the floor if we draw a floor that is always a layer above the player. In `_draw()` after the player and obstacles are drawn, we'll draw a brown floor in the 8-pixel gap we created at the bottom of the screen. Because the ground will be drawn last, it will be drawn on the top most layer. **_This is important. In PICO-8 everything gets drawn on top of everything that came before it_**. We'll draw this floor using a new function called `rectfill()` which takes in two coordinates for one corner of a rectangle, and two coordinates for the opposite corner, then a number for the color. The ground will start at the left side of the screen (𝑥 = 0) and just below the bottom of the player (𝑦 = 103 + 16 + 1 = 120). It will end at the very bottom-right of the screen (𝑥 = 127, 𝑦 = 127).

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
  rectfill(0, 120, 127, 127, 4)
end
```

Much better! Now we can work on the score.

## Score Go Up!

The score for this game will be similar to the timer from our clicker game. Instead of a timer that counts down though, will make it count up. Every frame, we'll add one to our score.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
  score = score + 1
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
  rectfill(0, 120, 127, 127, 4)
end
```

And we'll print it by converting it to seconds.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
  score = score + 1
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
  rectfill(0, 120, 127, 127, 4)
  print("score: " ..
    flr(score/30), 7)
end
```

Nothing happens to our score when we hit an obstacle though. Let's reset the score to zero if we hit something and remove the teleportation.

```lua
-- tab 1: player character
player_x = 8
player_y = 103

function draw_player()
  line(
    player_x,
    player_y,
    player_x,
    player_y + 16,
    11)
end

function move_player()
  if btn(5) then -- jump
    player_y = 87
  elseif btn(4) then -- duck
    player_y = 115
  else
    player_y = 103
  end
end

function collision()
  if player_x == low_x
    and not btn(5) then
    score = 0
  end

  if player_x == high_x
    and not btn(4) then
    score = 0
  end
end
```

### High Score

Looking good! Let's bring `high_score` into the mix. We can keep this simple by just doing an `if` statement in `_update()` that checks if `score` is higher than `high_score`, and if it is, set `high_score` to `score`. This has an added benefit where both scores will count up at the same time when the player is achieving a high score. This looks pretty cool and adds some tension.

```lua
-- tab 0: main
function _init()
  score = 0
  high_score = 0
end
function _update()
  move_player()
  move_obstacles()
  collision()
  score = score + 1
  if score > high_score then
    high_score = score
  end
end
function _draw()
  cls()
  draw_player()
  draw_obstacles()
  rectfill(0, 120, 127, 127, 4)
  print("score: " ..
    flr(score/30), 7)
  print("high score: " ..
    flr(high_score/30), 7)
end
```

And there's our game! It certainly needs some polish before anyone would want to play it for fun, but the core mechanics are there for us to build on top of if we'd like to take this further.
## Final Thoughts

So we have a player character that can jump, duck, and detect when it hits an obstacle. We have obstacles that continuously move left, giving the illusion of the player running to the right. And we have a score system that resets when we hit an obstacle and keeps track of our high score.

We could build on this by creating a game over screen like our last game. We could also add more obstacles, as the game is pretty easy the way it is now.

As we do these lessons, we should keep two things in mind. One, how can I use what I learned in previous lessons to make this game better? Two, how can I use what I learned in previous lessons and this lesson to make different games? 