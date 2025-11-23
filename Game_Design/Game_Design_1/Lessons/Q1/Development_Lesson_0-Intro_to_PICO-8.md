## What is PICO-8?

PICO-8 is described by their creators as a retro "fantasy console". In other words, it never existed in the past like, say the Atari 2600 did, but it shares some similarities such as a limited set of colors, a very small screen resolution, and a 32k data capacity.

## Why Start with PICO-8?

There is a popular quote in the arts and in engineering that goes "_Limitation breeds creativity_". Having unlimited resources can actually make it harder to create something, as our mind has a hard time choosing from a near infinite set of possibilities. The strict limitations of PICO-8 makes it easier to come up with and code our game ideas. Second, the strict limitations makes it easier to learn as well. In later lessons, we will move to a more complex game engine called Godot. Godot is a great engine, but is overwhelming for beginners as there are _so many_ features and settings to learn before we can make anything cool. You can think of starting our game development journey with PICO-8 as learning how to drive by starting on a go-kart.

## Boot Up & Terminal

When you first open PICO-8, you will see the boot up screen which is a simple animation followed by a short chime sound. You will then see the **terminal** sometimes referred to as the **command line interface (CLI)**. A terminal is how we used to interact with every computer before the **graphical user interface (GUI)** was made popular. Despite being somewhat outdated, programmers still love to use the old-school terminal over the GUI as it allows us to navigate the computer much faster, also there are very useful programs that can only run in the terminal.

### Help!

One of the first things we see after booting up PICO-8 is "Type 'help' for help". If we type "`help`" into the terminal and press the ENTER key, we will see a helpful reference of all the commands we can type into the terminal and what they do. Every one of these commands is important for tasks that we will complete on our game dev journey, but for right now, let's focus on navigating and creating files and folders.

### Creating Folders/Directories

After typing "help", we see a few commands that reference "dir" or "directory". These are just fancy names for what you already call a "folder". Remember: **_a directory is simply a folder_**. So, to create a directory we type "`mkdir`" (short for "Make Directory"), then the SPACE bar, then we will type "`lessons`" to give the directory that name, and press the ENTER key to create the directory.

### Seeing Inside a Directory & Changing Directories

_Okay..._ so we created a directory, but where is it? To see what is inside our current directory, we can type "`ls`" (short for "list"), and press the ENTER key. When we do this, we should see a single directory called "lessons"; the one we just created. To switch to that directory, we will type "`cd`" (short for "change directory"), then the SPACE bar, then we type the name of the directory we'd like to switch to; in this case "`lessons`", and press the ENTER key. We are now in the "lessons" directory. This is where we will save all of games that are part of the guided lessons. Later, we will make a "projects" directory where we will store projects, which are games we make on our own, without a guide.

### Creating our First Cart

Games in PICO-8 are called "carts" (short for "cartridge"). Older consoles such as the _Atari 2600_, _Nintendo Entertainment System (NES)_, and _Sega Genesis_ used to cartridges before we switched to disks. We'll create our first cart by typing "`save`", then pressing the SPACE bar, then typing "`lesson_0_hello_world`" to give it that name, and then press the ENTER key to finish. We will write a simple program in this cart shortly, but first, let's finish exploring the terminal.

### Hello, world!

Getting the sentence "Hello, world!" to show up on the screen is a time-honored tradition for new programmers. Let's uphold this tradition now.

In the terminal we can run any code that can be written into a game by typing the code into the terminal and pressing the ENTER key. This will be _very_ useful later as we debug our games, but for now, let's use this feature to get a feel for programming in PICO-8. One of the most popular functions in PICO-8 is `print()`. This function allows us to show text on the screen. A **function** in programming is a bunch of code that has been given a name so we can run all that code over and over again easily. We can think of a function like a recipe in cooking. If I tell you I'm having pizza for lunch, you'll know exactly what I'm saying. I don't have to mention that pizza is baked bread with tomato sauce and cheese. We can identify a function when we see one because they always have **parenthesis** `()` at then end. Some functions run the exact same code the exact same way every time, and their parenthesis are empty. Other functions can change they way run by accepting **arguments**, which are modifications to the way the function can run. Some arguments are required, while others are optional.

If we check the PICO-8 manual for how to use the `print()` function, we see the following:

```txt
print(str, [col])
Print a string str and optionally set the draw colour to col.
```

So what does this mean? "print" is the name of the function, and it accepts two arguments, "str" (short for **"string"**, which is another word for text) and "col" (short for "color"). Notice that there are **square brackets** `[]` around "col". This means that argument is optional. In other words, when we use the `print()` function, we _must_ put the text we would like to show in the parenthesis, and if we would like to, we _may_ change the color, but we don't _have to_.

Let's use this function now. In the terminal, type "`print("hello, world!")`" and press the ENTER key. If you see the text "Hello, World!" pop up on the line immediately under the function you wrote, congratulations! If not, check that every single character you typed is exactly as I wrote it. Remember that programming languages are _very_ picky, and expect everything to be written in a specific way. These specific instructions are called **syntax** and if we mess up the syntax, we create a **syntax error**.

Let's now use that optional argument we discussed earlier, and give our "hello, world!" some color. If a function accepts more than one argument, each argument must be separated with a comma `,`. Let's do that now by typing `print("hello, world!", 11)` and pressing the ENTER key. You should see the text "hello, world!", but now in green instead of white. Feel free to experiment with other colors by replacing the 11 with another number. There are 16 colors available in PICO-8, and they are numbered 0 - 15. If you don't want to re-type the function, you can press the UP_ARROW key on your keyboard to access the last thing typed into the terminal. This will save us a lot of time in the future! Try some other colors now.

## The Code Editor

As you can imagine, it won't be possible to create a game by writing code line by line into the terminal. Instead, we write our code into a **code editor**. To access the code editor, we tap the ESC key on our keyboard. Try it, and you should see a dramatic change in the way PICO-8 looks. There is a lot going on here, and we will dive into each element in detail in future lessons, but for now, let's just use the editor.

Let's re-type our `print("hello, world!", 11)` into the code editor. You can stay with 11 (green) if you'd like, or choose any other PICO-8 color.

```lua
print("hello, world!", 11)
```

To run the code we can press CTRL + R on our keyboard. Do that now to see the results of the code. Your screen is probably filling up with a lot of `hello, world!` at this point, and if we re-run the program by pressing CTRL + R again, we'll notice that they just keep getting added to the bottom. However, most games start fresh when we run them. So, how do reset the screen each time we run our code?

Let's learn another function. This one is written as `cls()` (short for "clear screen") and takes in no arguments as it simply clears the screen. Let's use this function to clear the screen before showing our text. Press the ESC key again to go back to the editor, then bump the `print()` function down to the second line and write `cls()` on the first line, like this:

```lua
cls()
print("hello, world!", 11)
```

When we run this with CTRL + R, we should only see `hello, world!` at the top of the screen and nothing else before it.

## Screen Coordinates

There is _so much more_ to PICO-8 and I am very excited to show you everything, but we'll wrap up this lesson with one more very important concept; **screen coordinates**. Screen coordinates are how we keep track of the location of everything on screen. We use screen coordinates to place the player, enemies, and objects. We also use screen coordinates to move these things as well. They are _very_ important to understand, and can be a little tricky to work with at first.

### Cartesian Coordinates

If you've taken an algebra class before now, you have been introduced to the **Cartesian Coordinate Grid**, which is a system for describing the location of points in two-dimensional space. The grid consists of an 𝑥-axis which describes a point's horizontal (left-right) location and a 𝑦-axis which describes the point's vertical (up-down) location. We reference a point's location by stating it's (𝑥, 𝑦) on this grid. 𝑥 is always first, 𝑦 is always second, and we use a comma to separate them.

The Cartesian Coordinate Grid has a center point known as the **origin** where 𝑥 = 0 and 𝑦 = 0. From there, on the 𝑥-axis, if we move right, the point's 𝑥 location increases (1, 2, 3, ...) and if we move left from the origin, the point's 𝑥 location decreases (-1, -2, -3, ...). Likewise, from the origin, on the 𝑦-axis, if we move up, the point's 𝑦 location increases (1, 2, 3, ...) and if we move down from the origin, the point's 𝑦 location decreases (-1, -2, -3, ...).

Knowing this, if we start with a point at the origin and it moves three whole steps right and one whole step down, what is the point's (𝑥, 𝑦) location?

It is (3, -1).

### How are Screen Coordinates Different from Cartesian Coordinates?

Screen coordinates are similar to Cartesian coordinates, but with one major difference: **_the 𝑦-axis is flipped_**. This means that if a point is on the origin and it moves up, its 𝑦 location decreases (-1, -2, -3, …) and if it moves down from the origin, the point's 𝑦 location increases (1, 2, 3, …).

>[!IMPORTANT]
>In PICO-8 **_the 𝑦-axis is flipped_**.
>𝑦 **increases** as you go down the screen, and **decreases** as you go up the screen.

Let's use the same point with the same movements as our last example, but we'll use screen coordinates instead of Cartesian coordinates. If we start with a point at the origin and it moves three whole steps right and one whole step down, what is the point's (𝑥, 𝑦) location?

It is (3, 1). Notice that there is no difference for its 𝑥 position, it is still 3, but the 𝑦 position is opposite what it was before. Instead of its 𝑦 being -1, it is 1 because the 𝑦-axis flipped when we use screen coordinates.

### Screen Coordinates in Practice

Let's put our new knowledge of screen coordinates into practice. The first thing we will do is change our `print()` function so we write a blank space instead of "hello, world!. like so:

```lua
cls()
print(" ", 11)
```

Now we can test our knowledge of screen coordinates by placing a **pixel** on the screen using various 𝑥 and 𝑦 coordinates. A **pixel** is the smallest unit of light on a screen. The PICO-8 screen is 128 pixels wide and 128 pixels tall. In other words, it is a 128 pixel square.

Let's place our first pixel at the origin (0,0). We place pixels on the PICO-8 screen with the `pset()` function (short for "Pixel Set"). To place a pixel at the origin, we will write `pset(0,0)` on the third line, just under our `print()` function like so:

```lua
cls()
print(" ", 11)
pset(0, 0)
```

Before we run this with CTRL + R, try to imagine where you think this pixel will show on the screen. This may be a complete guess, but it _very_ important in programming to make educated guesses of what will happen before you run code. This is how we engage with what we are learning. If we just type the code we see and run it, we won't learn anything from the lesson. That being said, imagine where you think (0,0) might be, then press CTRL + R to see the result.

Is it where you thought it would be? If not that's totally okay. Educated guesses are about engaging with the code we write, not about being correct every single time.

So, there are two takeaways here.

1. The origin of the PICO-8 screen (and most game engines) is the top-left
2. Notice that the pixel is same color of whatever came before it

We can change the color pixel by adding a third, optional argument to the `pset()` function like so:

```lua
cls()
print(" ", 11)
pset(0, 0, 8)
```

If you chose eight like I did, the pixel should now be red.

Okay, so (0,0) is the top-left of the screen, and we said earlier that the screen is 128 pixels wide and 128 pixels tall. Let's change the first two arguments of the `pset()` function to 128 like so:

```lua
cls()
print(" ", 11)
pset(128, 128, 8)
```

Again, before we run this, imagine where you think the pixel will be. Now let's run it and see.

Hmm... It doesn't seem to be anywhere. Why might that be? If your educated guess was the bottom-right of the screen, you were _very close_. The pixel is actually one pixel off the right side of the screen and one pixel off the bottom of the screen. This is because, while the screen is a 128 pixel square, we start counting the pixels at number 0. that means the lowest, right-most pixel is actually (127, 127). Let's update our code, rerun it, and see if the pixel is indeed on the bottom right.

```lua
cls()
print(" ", 11)
pset(127, 127, 8)
```

Welcome back little pixel!

So, the top-left is (0,0) and the bottom-right is (127, 127). I want to challenge you to place the pixel on the top-right. Applying what we learned about screen coordinates, what will the two numbers need to be? Try this now, then click below to see the answer.

<details>
<summary>SPOILERS</summary>
If you wrote <code>pset(127, 0, 8)</code>, Great job! If not, I hope you gave it a few tries before seeing this answer. Remember, to get better at programming, we have to be willing to try and fail multiple times before looking up the answer. <strong><em>there are no shortcuts!</em></strong>
</details>
