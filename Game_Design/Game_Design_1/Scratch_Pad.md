# Ideas for Progression

Q1 - No-Code GDevelop w/ Small Code-Lite "Bridges" in Godot

1. Intro to UI / Saving Files / Starting a Project
2. Button Masher
	- Timers
	-   Button Interaction (Events) \*
	-   Score \*
	-   High Score \*
3. Endless Runner
	-   Drawing shapes to the screen (lines and rectangles)
	-   Moving objects on screen \*
	-   Basic player controls (jump and duck) \*
	-   Collision (Basic)
4. Shmup
	-   Drawing sprites
	-   Basic player controls (Left, Right, & Shoot) \*
	-   Enemy spawning
	-   Enemy movement \*
	-   Using random values to affect game-play \*
	-   Projectiles and collision (Intermediate)
5. Pong
	-   Keeping an object from leaving the screen
	-   Moving an object on two-axes \*
	-   Axis-Aligned Bounding-Box (AABB) Collision
	-   How to get an NPC to chase an object \*
6. Flappy Bird
	-  Gravity
7. Breakout
	- OOP
8. Platformer
9. Top-Down Adventure
10. Angry Birds
11. Pokémon
12. Mini Game Jam 1
13. Mini Game Jam 2
14. Pick one of the above and polish it

\* Indicates  concepts that will be "bridged" with Godot

# Ideas for Grading

## Require the same 4 items for every microgame

1. **Playable build**
    - HTML export ZIP (ideal), or a packaged build
2. **Short demo video** (60–120 seconds)
    - They show the mechanic working using your checklist
3. **One-page design brief** (template)
4. **Reflection** (5–8 sentences)

## Add “Debug Menu" (Still Considering)

Require simple debug keys in every project:

- **F1** = show debug overlay (score/health/state/wave)
- **F2** = add +100 score
- **F3** = take damage (-1 health)
- **F4** = trigger win / next level
- **F5** = spawn hazard/enemy wave

## Rubrics Checklist-Heavy

For microgames, use a rubric where most items are:

- **0 = missing / broken**
- **1 = present / works**
- **2 = works + polished/clear**
### Example microgame rubric

**Mechanics (60%)**

- Movement/input works reliably
- Main interaction works (collision consequence / collect / hit / etc.)
- Score/health tracked correctly
- Win/lose condition exists and is reachable
- UI clearly communicates state (score/health/messages)
- Difficulty changes or pacing is intentional (timer, spawn rate, etc.)

**Design Thinking (25%)**

- Core loop is clear within 30 seconds
- Player feedback is readable (sound/flash/text/etc.)
- Evidence of iteration from playtest/reflection

**Organization/Professionalism (15%)**

- Objects/scenes named clearly
- Events organized into logical groups
- Test Mode hooks implemented (F1–F5)
## Moodle Assignment Template

### **Submission Requirements**

1. **Playable Build (.zip)**
    - Export your game as HTML and upload the ZIP.
2. **Demo Video (.mp4, 60–120 seconds)**  
    Your video must show:
    - normal gameplay
    - **F1 debug overlay**
    - **F2 score add**
    - **F3 damage**
    - **F4 win/next**
    - **F5 spawn wave**
3. **Design Brief (.pdf or .docx, 1 page max)**  
    Include:
    - core loop (what player repeats)
    - controls
    - win/lose conditions
    - mechanics list
    - variables list + **5–10 lines of pseudo-code** for one main mechanic
4. **Reflection (in the text box or as a file)**  
    Answer:
    - What did you change after playtesting?
    - What bug/problem took the longest to fix?
    - What would you improve next?


# Game Design 2

1. GDQuest
2. Godot
	1. Button Masher
	2. Endless Runner
	3. Shmup
	4. Platformer
3. Python
4. Blender
5. More Godot

# Game Design 3

1. Godot Wario-Ware
	1. Git - Gitlab
	2. "Jira" - OpenProject
2. JavaScript

# Game Design 4

1. Godot Capstone
2. Java
# Certificate Progression

1. Device Config
2. Python
3. JavaScript
4. Java

# PICO-8 Lessons

0. Lesson 0:
	- Navigating the Command Line:
		- `ls`
		- `mkdir`
		- `cd` / `cd ..`
		- `load`
	- Simple Functions:
		- `print()`
		- `pset()`
		- `cls()`
	- Screen Coordinates
1. Lesson 1:
	- Initial Game Loop:
		- `_init()`
		- `_update()`
		- `_draw()`
	- Programming Basics:
		- Variables / Assignment
		- Conditionals / Equality
		- Frames Per Second (FPS)
		- Printing and Variable Concatenation
2. Lesson 2:
	- Code Organization:
		- Comments
		- Custom Functions
	- Drawing Primitive Shapes:
		- `line()`
		- `rrect()`
		- Spacing and Alignment
		- Z Layers
3. Lesson 3:
	- `spr()`
	- Player movement and stopping at the screen edges
	- Multiplying by -1
	- Hit-scan projectiles
	- Tables
	- `for do` Loops
	- Game State
4. Lesson 4:
	- Moving something on x and y at the same time
	- AABB Collision
	- 