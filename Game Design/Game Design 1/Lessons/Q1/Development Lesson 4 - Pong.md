## What is Pong?

Pong is a two player game with similar rules to tennis. Each player controls a rectangular paddle that can move up and down, and a ball moves around the screen. Each player's goal is to prevent the ball from making it past their paddle; scoring the other player a point.

## Why Make Pong?

Pong is a great next step for us as it will build on what we know about drawing shapes to the screen, controlling the player character with the arrow keys and keeping score. We'll be able to now get something to move in two dimensions, and we'll create a slightly smarter enemy than the UFOs that moved randomly..

## What will this Game Teach Me?

The new game mechanics we will learn with this lesson are:

-   Moving an object on two-axes
-   Keeping an object from leaving the screen
-   Axis-Aligned Bounding-Box (AABB) Collision
-   How to get an enemy to chase an object

## Let's Get Started

As always, we'll start with the initial setup in tab 0.

```lua
-- tab 0 main
function _init()
end

function _update()
end

function _draw()
  cls()
end
```

As with last lesson, there are so many places we could start, and feel free to take a moment to think about where _you_ would start. We'll start with creating the player's paddle.

## The Player Paddle

We'll start by opening a new tab, in which we'll write some variables to define the player's paddle. This time, we'll write these variables in the new table format we learned in the last lesson.

```lua
-- tab 1 player
player = {
  x = 5,
  y = 52,
  width = 3,
  height = 16,
  speed = 1
}
```

Now we create a function to draw the player paddle.

```lua
-- tab 1 player
player = {
  x = 5,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function draw_player()
  rectfill(player.x,
    player.y,
    player.x + player.width,
    player.y + player.height,
    7)
end
```

And we'll update the main tab.

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

### Moving the Player Paddle

Moving the player's paddle will be very similar to how we moved the player's ship in the previous lesson. We will do something slightly differently. So far, we've updated variables by writing something like `x = x + 1`, but there is a faster way. In PICO-8, and most other programming languages, we can do the same thing by writing it like this `x += 1`. We'll use this method to update variables from now on.

```lua
-- tab 1 player
player = {
  x = 5,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_player()
  if btn(2) then
    player.y -= 1
  elseif btn(3) then
    player.y += 1
  end
end

function draw_player()
  rectfill(player.x,
    player.y,
    player.x + player.width,
    player.y + player.height,
    7)
end
```

And we'll update the main tab.

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

Good, good. But, let's take this to the next level. This paddle, like our ship from last lesson, can go off the screen. Let's add some code that will prevent the paddle from leaving the screen. All we need is a couple of simple `if`statements that will check if the paddle went off the screen, and if it did, we'll just teleport it back.

```lua
-- tab 1 player
player = {
  x = 5,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_player()
  if btn(2) then
    player.y -= player.speed
  elseif btn(3) then
    player.y += player.speed
  end

  if player.y < 0 then
    player.y = 0
  elseif player.y > 111
    player.y = 111
  end
end

function draw_player()
  rectfill(player.x,
    player.y,
    player.x + player.width,
    player.y + player.height,
    7)
end
```

You'll notice that one of the `if` statements checks if the `y` variable for the player paddle is greater than 111, not 127. Remember that the (𝑥, 𝑦) location of a rectangle is its top-left corner, therefore, if we want to check if the _bottom_ of the rectangle goes off the screen, we have to subtract the height. 127 - 16 = 111.

## The Enemy Paddle

We can use a lot of this code to also create the enemy paddle. We just have to be a little careful with the `x` variable for the enemy, as we'll need to do a little math to ensure it is the same amount of pixels away from the edge of the screen as the player paddle.

```lua
-- tab 2 enemy
enemy = {
  x = 119,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_enemy()
  if enemy.y < 0 then
    enemy.y = 0
  elseif enemy.y > 111
    enemy.y = 111
  end
end

function draw_enemy()
  rectfill(enemy.x,
    enemy.y,
    enemy.x + enemy.width,
    enemy.y + enemy.height,
    7)
end
```

So why 119? There is a five-pixel gap between the right side of the screen and the left side of the player paddle. For the enemy paddle, we need to take that five and add the width of the paddle, which is three pixels, for a total of eight. 127 - 8 = 119.

And we'll update the main tab.

```lua
-- tab 0 main
function _init()
end

function _update()
  update_player()
  update_enemy()
end

function _draw()
  cls()
  draw_player()
  draw_enemy()
end
```

## The Ball

We'll now move on to creating the ball. We'll start by opening a new tab, creating a table, and filling with the variables needed to define the ball. The ball will need separate (𝑥, 𝑦) speeds so it can travel both left-right, and up-down.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}
```

We'll draw the ball and update its location using its speeds.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}

function update_ball()
  ball.x += ball.x_speed
  ball.y += ball.y_speed
end

function draw_ball()
  pset(ball.x, ball.y, 7)
end
```

And we'll update the main tab.

```lua
-- tab 0 main
function _init()
end

function _update()
  update_player()
  update_enemy()
  update_ball()
end

function _draw()
  cls()
  draw_player()
  draw_enemy()
  draw_ball()
end
```

### Getting the Ball to Bounce Off of the Top and Bottom

One key aspect of Pong, is that the ball bounces off of the top and bottom of the screen. To do this we will combine two techniques that we already know. One, keeping an object from leaving the screen and two, reversing an objects direction. We'll check if the ball leaves the screen the same way we did with the player paddle, then we'll reverse its `y_speed` variable by multiplying it by negative one.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}

function update_ball()
  ball.x += ball.x_speed
  ball.y += ball.y_speed

  if ball.y < 0 then
    ball.y = 0
    ball.y_speed *= -1
  elseif ball.y > 127 then
    ball.y = 127
    ball.y_speed *= -1
  end

end

function draw_ball()
  pset(ball.x, ball.y, 7)
end
```

Awesome! If we run the game, the ball should go down and right, then bounce off of the bottom of the screen. If you'd like to check both the top and the bottom, you can change the `x` variable to `0`, so the ball only moves up and down.

### Axis-Aligned Bounding-Box Collision Detection

**AABB Collision Detection** is a fancy term that simply means, checking if two rectangular objects collide. To set this up can be quite tricky the first time, so as always, we'll take baby-steps. The ball for our pong game is a single pixel, which will make this easier than checking for collision with two large rectangles.

What we want to do in code, is check `if` the 𝑥 location of the ball is `greater than` the the 𝑥 location of the paddle `and` check `if` the 𝑥 location of the ball is `less than` the the 𝑥 location of the paddle plus its width. We also have to check `if` the 𝑦 location of the ball is `greater than` the the 𝑦 location of the paddle `and` check `if` the 𝑦 location of the ball is `less than` the the 𝑦 location of the paddle plus its height. If all of this is `true`, the ball has touched the paddle and we reverse the ball's `x_speed` variable to get it to change direction.

This will also be the first custom function we make that will take in parameters. This is because we want this function to work for both paddles.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}

function update_ball()
  ball.x += ball.x_speed
  ball.y += ball.y_speed

  if ball.y < 0 then
    ball.y = 0
    ball.y_speed *= -1
  elseif ball.y > 127 then
    ball.y = 127
    ball.y_speed *= -1
  end

end

function draw_ball()
  pset(ball.x, ball.y, 7)
end

function collision(paddle)
  if ball.x > paddle.x and
    ball.x < paddle.x + paddle.width and
    ball.y > paddle.y and
    ball.y < paddle.y + paddle.height then
      ball.x_speed *= -1
  end
```

Now we need to call this function in both the `update_player()` and `update_enemy()` functions, using the `player`, and `enemy` tables as the parameter we pass into the function.

```lua
-- tab 1 player
player = {
  x = 5,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_player()
  if btn(2) then
    player.y -= player.speed
  elseif btn(3) then
    player.y += player.speed
  end

  if player.y < 0 then
    player.y = 0
  elseif player.y > 111
    player.y = 111
  end
  collision(player)
end

function draw_player()
  rectfill(player.x,
    player.y,
    player.x + player.width,
    player.y + player.height,
    7)
end
```

```lua
-- tab 2 enemy
enemy = {
  x = 119,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_enemy()
  if enemy.y < 0 then
    enemy.y = 0
  elseif enemy.y > 111
    enemy.y = 111
  end
  collision(enemy)
end

function draw_enemy()
  rectfill(enemy.x,
    enemy.y,
    enemy.x + enemy.width,
    enemy.y + enemy.height,
    7)
end
```

Looks great! If we want to test this for both paddles, we can set the `y_speed` variable of the ball to `0` so it only moves right-to-left.

### Checking for a Goal

Now we can move on to checking if the ball is past the left or right side of the screen, which means someone scored a point.

First, let's go back to the main tab and print the current score for both the player and the enemy.

```lua
function _init()
end

function _update()
	update_player()
	update_enemy()
	update_ball()
end

function _draw()
	cls(1)
	draw_player()
	draw_enemy()
	draw_ball()
	print(player.score, 42, 5, 7)
	print(enemy.score, 85, 5, 7)
end
```

Now we can go back to the ball tab and create a function that checks if the ball is off the screen.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}

function update_ball()
  ball.x += ball.x_speed
  ball.y += ball.y_speed

  if ball.y < 0 then
    ball.y = 0
    ball.y_speed *= -1
  elseif ball.y > 127 then
    ball.y = 127
    ball.y_speed *= -1
  end
  score_point()
end

function draw_ball()
  pset(ball.x, ball.y, 7)
end

function collision(paddle)
  if ball.x > paddle.x and
    ball.x < paddle.x + paddle.width and
    ball.y > paddle.y and
    ball.y < paddle.y + paddle.height then
      ball.x_speed *= -1
  end

function score_point()
  if ball.x > 127 then
    player.score += 1
  end
  if ball.x < 0 then
    enemy.score += 1
end
```

Okay, we score once the ball leaves the right side of the screen, but the score continues to go up forever. Let's reset the ball back to the center after a score.

```lua
-- tab 3 ball
ball = {
  x = 63
  y = 63
  x_speed = 1
  y_speed = 2
}

function update_ball()
  ball.x += ball.x_speed
  ball.y += ball.y_speed

  if ball.y < 0 then
    ball.y = 0
    ball.y_speed *= -1
  elseif ball.y > 127 then
    ball.y = 127
    ball.y_speed *= -1
  end
  score_point()
end

function draw_ball()
  pset(ball.x, ball.y, 7)
end

function collision(paddle)
  if ball.x > paddle.x and
    ball.x < paddle.x + paddle.width and
    ball.y > paddle.y and
    ball.y < paddle.y + paddle.height then
      ball.x_speed *= -1
  end

function score_point()
  if ball.x > 127 then
    player.score += 1
    reset_ball()
  end
  if ball.x < 0 then
    enemy.score += 1
    reset_ball()
end

function reset_ball()
  ball.x = 63
  ball.y = 63
end
```

## Moving the Enemy

Now we just need to get the enemy to chase the ball. We can think of this as being the same as what we do when we play. If the ball is above our paddle, we move our paddle up. If the ball is below our paddle, we move our paddle down. We'll check if the ball is above or below the middle of the enemy's paddle and move it accordingly. Note that enemy will never miss the ball this way. I'll leave it to you to find out how to use `rnd()` in a creative way to get the enemy to miss every now and then.

```lua
-- tab 2 enemy
enemy = {
  x = 119,
  y = 52,
  width = 3,
  height = 16,
  speed = 1,
  score = 0
}

function update_enemy()
  move_enemy()
  if enemy.y < 0 then
    enemy.y = 0
  elseif enemy.y > 111
    enemy.y = 111
  end
  collision(enemy)
end

function draw_enemy()
  rectfill(enemy.x,
    enemy.y,
    enemy.x + enemy.width,
    enemy.y + enemy.height,
    7)
end

function move_enemy()
  if ball.y < enemy.y + 8 then
    enemy.y -= enemy.speed
  end
  if ball.y > enemy.y + 8 then
    enemy.y += enemy.speed
  end
end
```

And there's our game!

## Finishing Thoughts

We created paddles, got them to move, and made certain that they cannot go off the screen. We created a ball that can move on both axes, bounces off the top and bottom of the screen, bounces off the paddles, and scores a point to the right player if it goes off the left or right side of the screen. Finally, we built simple enemy logic.

As always, keep in mind the two very important questions we ask our self after every lesson.

1. How can I use what I learned in previous lessons to make this game better?
2. How can I use what I learned in previous lessons and this lesson to make different games?
