## What is a Minimum Viable Product(MVP)?
An MVP is the smallest, cheapest, quickest to produce version of something you'd like to market. For example, say you'd like to invent a new pet-tracking collar. The MVP for this may simply be some rope with an Apple Air Tag tied to it.

## Why is an MVP Important?
An MVP is important because it allows us to see if a product is marketable before sinking a ton of time, effort, and money into it. For game development this can save a AAA studio millions of dollars and can save an Indie developer years of their life. 

We may think our game idea is super fun, but until we test it with other players we can never be certain. On the other hand, we can't wait until after we have a finished game to test the idea with players because games take many months or years to make. This is where the MVP shines. We can quickly make a short demo that shows off the core game mechanics that we believe are fun and marketable and have players try it to see if we are correct.

## What is the *Absolute* Minimum?
Now that we know the definition of a video game is, let's try to make an MVP. What is the bare minimum we need to code for a program to count as a video game? Remember that all we need is **interaction** and a **win/lose** condition.

For our very first game, we will make a simple clicker game. That is; a game where we have to click a button as fast as we can within a time limit. Will this game be fun? Probably not. But it will give us a great start for learning how to develop a video game, as we are starting with a simple goal with very clear requirements.

## Clicker Game
### What Will this Game Teach Me?
With each game we make, we will be learning game mechanics. The goal is to treat these game mechanics like building blocks that will allow you to make any game you want in the future. In other words, don't think of this lesson as "How to make a Clicker Game" but instead as "Intro to the First Important Game Mechanics". These mechanics are:

* Timers
* Button Interaction (Events)
* Score
* High Score

### Let's get Started!
To get started, in tab 0 of Pico 8 we will write our basic game setup:

``` lua
function _init()
end
function _update()
end
function _draw()
  cls()
end
```

### Score Variable
Let's now add our first variable in `_init()` to hold how many clicks have occurred. Remember that a variable is simply a container that stores data, and we can change the data in the container any time we want.

``` lua
function _init()
  score = 0
end
function _update()
end
function _draw()
  cls()
end
```
### Conditionals
Now we need to find a way to check if the player has pressed a button. In programming, if we want to check *if* something happens we use what is called a **conditional** or **if** statement. As this is game logic, we will put this in the `_update()` function. Many languages treat if statements the same way, but for Pico 8 specifically we write `if` followed by parenthesis `()`. What is inside the parenthesis is checked to be either `true` or `false`. After that we write `then`, press the ENTER key to move to the next line, then the TAB key to indent. All of the code in here will only run if what we wrote in the parenthesis turned out to be `true`. If not, the code will not run. This is very important for programming, as we often want some code to run in one condition, but other code to run in a different condition. For this game, we want the score to increase *if* the O button was pressed, and we do not want the score to increase *if we do not* press the O button.

Pico 8 has six buttons Up, Down, Left, Right, O, and X. For this simple game we will use the O button, which on a computer keyboard will be Z and has a key-code of `4`. The `btnp()` function can be used to check if a button was pressed, which is perfect for a clicker game where we want the player to press the button over and over, not just hold it down. So we'll write `btnp(4)` inside the parenthesis after the word `if` to check if the player pressed the O button and we'll follow that with the word `then` to finish the line.

Inside the `if` statement we will increase the score variable by one by writing `score = score + 1`. This doesn't make much sense as a math equation, but remember that a single `=` in programming does not mean *equal to*, it means *assign to*. So we would read this line in English as "The score variable is assigned the value of the score variable plus one". Since that is the only code we want to run after the player presses the O button, we write `end` on the next line to finish our `if` statement.

``` lua
function _init()
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
end
function _draw()
  cls()
end
```
### Show the Score
If we run the code we just wrote, not much will happen. This is because, while the computer is tracking our score in memory, we can't peek inside the memory to see that process. To make the score visible to the player, we have to show it. To show text, we can use the `print()` function. As this getting drawn to the screen, we will put this in the `_draw()` function. Under `cls()`, we will simply write `print(score)` to show the current value of the score variable.

``` lua
function _init()
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
end
function _draw()
  cls()
  print(score)
end
```

Now when we run the code, we see the score go up as press the Z key.

### Add a Timer
We now have something interactive (and maybe even entertaining to some people), but we don't have a game yet as we can't win or lose. Let's add a timer so the player can try to beat their high score.

We'll start by adding a `timer` variable that will represent the time the player has to click the button. Remember that Pico 8 runs at 30 frames per second(fps), so have to multiply the amount of seconds we want the timer to start at by 30. We'll give the player one minute to click the button as fast as they can by writing `timer = 60 * 30`.

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
end
function _draw()
  cls()
  print(score)
end
```

### Make the Timer Count Down
In the `_update()` function we will make the timer count down by one each frame by simply writing `timer = timer - 1`, which makes sense when we remember that `score = score + 1` made our score go up by one.

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
  timer = timer - 1;
end
function _draw()
  cls()
  print(score)
end
```

Notice that this line is under the `end` that closes the `if` statement. We don't want the timer to count down *only* when the button is pressed, we want it to count down every single frame no matter what.

### Show the Timer (v1)
Just as we had the problem earlier of counting our score up in memory, but not being able to see it, we have the same issue now with our timer. Let's add another `print()` function in `_draw()` to show the timer as it counts down.

Under `cls()` we will add `print(timer)` to show the current value of the `timer` variable.

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
  timer = timer - 1;
end
function _draw()
  cls()
  print(timer)
  print(score)
end
```

If we run this, we'll see the timer count down, but there are a few issues.

* It's a little confusing having two numbers on the screen with nothing to label them
* The timer is formatted in frames which is a big number that counts down very fast

### Show the Timer (v2) with Labels
To add labels we must learn how to combine text (also known as **strings** in programming) with variables in a `print()` function. The process of adding two strings is called **string concatenation**. A very fancy term for such a simple idea. Let's use string concatenation to add labels to our variables.

To do string concatenation in the `print()` function we must use double periods `..` between the strings we'd like to combine. For the timer, we will rewrite `print(timer)` to `print("time left: " .. timer)`. And for the score, we will do `print("Score: " .. score).

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
  timer = timer - 1;
end
function _draw()
  cls()
  print("time left: " .. timer)
  print("score: " .. score)
end
```

Much better! Now lets format the timer to be in seconds, not frames.

### Show the Timer (v3) in Seconds
Because the timer counts down inside `_update()`, it counts down thirty times every second. To convert this one minute, we multiplied sixty (seconds) by thirty (fps) so the timer *actually* takes one minute to count down. The problem now is, most players don't understand what a frame is, and even if they did, a frame is so fast the timer is very hard to read.

We multiplied the amount of seconds we wanted our timer to last by thirty to convert it to frames, so to convert it back to seconds we just have to do the opposite of multiplication, which is division. In the `print()` function for the timer we will update it to `print("time left: " .. timer/30)`.  Note that in the code below I moved `timer/30` to the line below. The code works just fine when we break it up this way and it makes it easier to read in Pico 8, because the screen is so small. 

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
  timer = timer - 1;
end
function _draw()
  cls()
  print("time left: " .. 
    timer/30)
  print("score: " .. score)
end
```

After running this, you may notice another problem. Because we used division, our timer often includes a decimal which flashes very fast and is quite ugly. We only want the whole number. Thankfully this is easy to fix by rounding down with the `flr()` function. Now the `print()` function for the timer will look like this `print("time left: " .. flr(timer/30))`.

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (btnp(4)) then
    score = score + 1
  end
  timer = timer - 1;
end
function _draw()
  cls()
  print("time left: " .. 
    flr(timer/30))
  print("score: " .. score)
end
```

Fantastic! Another problem though... The timer doesn't stop at zero.

### Show the Timer (v4) and Stop the Game at Zero
Finally, we will end the game when the timer reaches zero. To do this, let's think of everything currently happening in `_update()` as "the actual game". We only want to run this code when there is time left on the timer. So, how do we run some code only if a certain condition is `true`? With an `if` statement, of course!

We'll add an `if` statement under `_update()` and above the one that checks when the player presses the O button. The `if` statement will check if the timer is greater zero by writing `if (timer > 0) then`. Don't forget to tab every line in now that all of the code belongs *inside* this new `if` statement, then we'll add another `end` after count the timer down.

``` lua
function _init()
  timer = 60 * 30
  score = 0
end
function _update()
  if (timer > 0) then
    if (btnp(4)) then
      score = score + 1
	end
	timer = timer - 1;
  end
end
function _draw()
  cls()
  print("time left: " .. 
    flr(timer/30))
  print("score: " .. score)
end
```

Beautiful! But how do see our high score and reset the game?

### Finishing Touches
So we have code in `_update()` that we referred to as "the actual game" which is were the player is expected to click the O button as fast as possible, but there is another part of the game. We might refer to this as "the game over screen". This is where the player can see their high score and press a button to restart the timer to try again. These different situations within a game are called **game states**. Managing game states can be very difficult when we need a lot of them, and we will explore this topic further in future games, but for this game there are only two states, so we can get away with doing this the ugly way for now.

First, let's create a variable for the high score. Note that for this lesson we will create the variable in `_init()` which means it will get set to zero every time we start the game up. In other words, the high score will be deleted if we change games or shut down the console. While there is a way to save our game data, we will keep this lesson as simple as possible.

``` lua
function _init()
  timer = 60 * 30
  score = 0
  high_score = 0
end
function _update()
  if (timer > 0) then
    if (btnp(4)) then
      score = score + 1
    end
  timer = timer - 1;
  end
end
function _draw()
  cls()
  print("time left: " .. 
    flr(timer/30))
  print("score: " .. score)
end
```

Great!

Now, the `if` statement has a few more tricks we haven't used yet. So far, we have only used `if` to check the condition, `then` to start the code portion, and `end` to complete the statement. What if we want to run some code if something is `true` and different code if it is `false`? This is where `else` can be helpful.

If the timer is greater than zero, we are in "the actual game", but if not, we are in "the game over screen". Let's write some code to make this happen. After we make the timer count down we will write `else` and add some code to update our high score if it beats our previous high score. We'll add `if (score > high_score) then` and put `high_score = score` inside that `if` statement and complete it with `end`.

``` lua
function _init()
  timer = 60 * 30
  score = 0
  high_score = 0
end
function _update()
  if (timer > 0) then
    if (btnp(4)) then
      score = score + 1
    end
    timer = timer - 1;
  else
    if (score > high_score) then
      high_score = score;
    end
  end
end
function _draw()
  cls()
  print("time left: " .. 
  flr(timer/30))
    print("score: " .. score)
end
```

Cool! Now let's show that high score on the game over screen.

In `_draw()` we'll add another `if` statement to check if the timer is less than one by writing `if (timer < 1) then` and adding `print("high score: " .. high_score)`. We'll also let the player know that they can press the X button to restart the game. And let's not forget `end`.

``` lua
function _init()
  timer = 60 * 30
  score = 0
  high_score = 0
end
function _update()
  if (timer > 0) then
    if (btnp(4)) then
      score = score + 1
    end
    timer = timer - 1;
    else
      if (score > high_score) then
        high_score = score;
      end
  end
end
function _draw()
  cls()
  print("time left: " .. 
    flr(timer/30))
  print("score: " .. score)
  if (timer < 1) then
    print("high score: " .. high_score)
    print("Press X to restart")
  end
end
```

Almost done! We let the player know they can restart the game with the X button, but we never wrote the code to handle that. Just as we check if the player pressed the O button with an `if` statement, we can do the same for the X button. Let's add that after we update the high score in `_update()`.

We'll add `if (btnp(5) then` and write `timer = 60 * 30` inside. We also need to reset the `score` variable by adding `score = 0` and, of course, we'll finish with `end`.

``` lua
function _init()
  timer = 60 * 30
  score = 0
  high_score = 0
end
function _update()
  if (timer > 0) then
    if (btnp(4)) then
      score = score + 1
    end
    timer = timer - 1;
  else
    if (score > high_score) then
      high_score = score;
    end
    if (btnp(5)) then
      timer = 60 * 30
      score = 0
    end
  end
end
function _draw()
  cls()
  print("time left: " .. 
    flr(timer/30))
  print("score: " .. score)
  if (timer < 1) then
    print("high score: " .. high_score)
	print("Press X to restart")
  end
end
```

And that is our MVP!

## Final Thoughts
Even for an MVP, this may seem like an awful lot of work.  I wont lie, programming is difficult. But, like any other skill, if you stick with it, you will get better and faster over time. You will be able to write more of your own code and you'll rely on tutorials less. I hope with this first lesson you see the potential, fun, and creativity that can only be expressed though game development. Have fun and keep learning! 