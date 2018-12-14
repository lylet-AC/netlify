---
author: "Tyler Lyle"
date: 2018-12-13
linktitle: The Creation of BlockBuster
title: The Creation of BlockBuster
highlight: true
---


### **Introduction**

BlockBuster is a game that was created for the Computer Science 480: Software Innovation course at Allegheny College.  BlockBuster is a sort of Arkanoid clone game with a twist.  The twist is that the user can insert their own images as playable levels.  BlockBuster comes with pre-selected levels in the form of famous movie title cards.  These title card images are then resized by BlockBuster and reconstructed into playable levels that the user breaks with a ball and paddle similar to that of famous classic games, such as: Arkanoid, Breakout, Block Breaker Deluxe, and the shareware title Super-DX Ball.   

BlockBuster is completely written in the Python programming language and uses PyGame as the primary library.  The PyGame library is needed to process game related information such as images, controller input, and much, much more.  Additionally other packages were needed, such as the Python Imaging Library to manipulate the image files that are used to create the blocks in the game.  Lastly, BlockBuster uses the GNU General Public License v3.0 which was done to give complete permission to others to reuse and distribute this code.

### Initial Concept

Open first conceptualizing BlockBuster, there were many questions that needed to be answered.  What language? What library? What would the final product look like? How do I know this is feasible?  In fact, at first I didn't even know what kind of game I wanted to make; I just knew I wanted to make a game.  The original idea actually came from a basic idea that was formed when considering my senior research project at Allegheny College.  This idea was to take elements from a game, such as Breakout and mix it with ideas from a shoot-em-up style game, such as Galaga.  

The resultant game would be a shoot-em-up, but the block set would move around and attack the paddle, as any boss in a shoot-em-up style game would do.  Due to time constraints for this project, however, coupled with the many other projects that were going to be due at the end of the semester, the choice was made to cut back to a more modest sized project.  This project would be a Breakout clone, but it was still missing some sort of pizzazz that would set it apart from the millions of other Breakout clones.  The twist came while thinking of names for the project.  While considering names for a Breakout clone, a play-on-words came to me.  BlockBuster can be interpreted as the literal breaking of blocks, or alternatively as the BlockBuster movie title levels the game comes with.

Furthermore, the choice to use Python was also a thought out one.  Python was chosen mostly due to its portable nature.  Many libraries in Python are built into the language itself and ones that are not included are easy to download with pip, the Python package installer.  Also, along with Pythons portable nature, it can easily execute code on multiple machines without the need for much altering of code.  Altogether, this made Python an easy choice as long as it had a necessary package to handle game creation, which Python has with the PyGame library.

### How BlockBuster Was Made

The first steps of creating BlockBuster started out with following a PyGame tutorial, as well as reading through the API to understand the different aspects of creating a PyGame project.  Using a tutorial and the API, I was able to figure out the basics of game implementation using PyGame.  However, the initial implementation was drastically different from the current state of the game.  At the first state of the game, there was only a small square that was able to be moved by the user with the arrow keys on the keyboard.  This eventually turned into the paddle, as all I had to do to the code was to stretch the rectangle the player moved, and limit movement to go either left or right in the x-axis direction based on which arrow key that was pressed.

Now that there was a paddle that could move, the relevant code was moved out of the main PyGame method to it's own file called `sprites.py`.  This is currently named the Player object, and can be seen in the current build of BlockBuster's `sprites.py` file.  This file also allowed for any other game object, such as blocks, or the ball to have an organized location outside of the main game logic in `BlockBuster.py`.  Regarding the ball, this was the next step to implement.  Instead of having keyboard keys pressed to move the ball, the ball is supposed to move autonomously and bounce off of objects.  

Since this was not my first PyGame creation, I already had a working ball class that I could copy over from my Pong Clone, which was created in a previous year (good thing for code modularity).  The ball class contains all of the necessary information to check for collisions with other rectangles and also holds a velocity vector that stores its movement information.  This operation was not a direct copy-paste, however, as the code did need to be refactored in order to work with a mutli-file setup.  Additionally, it was at this point that the `settings.py` file was created and the code across both `sprites.py ` and `BlockBuster.py` was modified to have certain information be changeable without the need to change hard-coded variables.

At this point, `BlockBuster.py` is in a class called game.  The game class contained code the initialize the PyGame library, initialize some classes such as the player and ball in the `new()` method, load any sprites for the paddle and ball in the `load_data()` method, has an `update()` method to handle game logic, an `events()` method to handle keyboard input, and a `draw()` method to draw the paddle and ball to the screen after they were updated.  There are also two classes for the Ball and Player in the `sprites.py` file; as well as some directories created to hold sprites, input images, and test cases which would be made later.  There is also the `settings.py` file which contains the display `HEIGHT` and `WIDTH`, some color tuples containing RGB values for `WHITE`, `BLACK`, `DARKGREY`, `LIGHTGREY`, `YELLOW`, `GREEN`, `BLUE`, and `RED`.  Additionally, the `settings.py` file also contains the `FPS` or frames per second of the game, and directories such as `ROOT_FOLDER`, `MAP_INPUT_FOLDER`, `SPRITE_FOLDER`, and `TEST_FOLDER` use the OS package to make directory joining cross compatible. Thus, the `settings.py` file would know where all of the directories would be on nearly any system.

It was at this stage that the program started resembling not only a game, but a well organized, configurable coding project.  However, the only playable parts that were correctly implemented were the ball and the paddle.  This made testing the ball physics fairly difficult as the ball would escape well beyond the screen after being reflected by the paddle once.  I then knew it was time to implement the outer walls.  The outer walls were chosen to also be PyGame rectangle objects as the ball was already programmed to reflect it's vector when colliding with this type of object.  The walls were programmed to be a width of 20 pixels wide and follow the outer boundaries of the screen using the `WIDTH` and `HEIGHT` variables in the `settings.py` file.  This means that when the screen is resized, the outer boundaries correctly scale with the window.  A width of 20 was chosen for each rectangle to ensure that the ball cannot pass through the object without triggering a collision, unless it is traveling faster than 20 pixels per frame; a speed that is unplayable for humans.

After the wall boundaries were created in the `sprites.py` file as class and then correctly invoked in the main `BlockBuster.py` file, it was then time to test the ball physics.  Loading `BlockBuster.py` through the terminal and playing this state of the game yielded expected results.  The ball would travel through the empty space and correctly collide with the boundaries. Thus, it was time to start `mapgen.py` implementation to create a tileset of blocks based on the input image. This step was the absolute hardest to achieve, as it was hard to test the actual output of this file.  Thus, a PyTest file was created to check the output of a very simple input image.  The object that was supposed to be returned to the main `BlockBuster.py` file was a list of lists.  This list of lists would contain the color information for the resized image.  Each index in the list would be a tuple containing RGB data that would be reconstructed by the `BlockBuster.py` file in the form of destructible blocks (the blocks weren't implemented yet).

That was the plan at least, however, first runs were not yielding a list of lists with each sub-list containing indices with a color value tuple.  What was implemented was using the Python Imaging Library (PIL).  The image defined in the `settings.py` folder is be uploaded by `mapgen.py` using PIL.  PIL is then used to resize the image and a nested for loop is iterated through to gather the color data.  As it turns out, this plan was correctly implemented aside from the way the list was appended.  This improper list appending created a data set that contained no tuples, but instead it held an empty list of lists.  Once the proper algorithm was figured out, it looked like:

```
from PIL import Image
import os
from settings import *
import sys

def generate_map(in_file):
    # Can be many different formats.
    im = Image.open(os.path.join(MAP_INPUT_FOLDER, in_file))
    im = im.resize((int(WIDTH / TILESIZE), int(HEIGHT * (.65) / TILESIZE)))
    pix = im.load()

    output_list = []

    width, height = im.size

    for w in range(width):
        output_list.append([])
        for h in range(height):
            output_list[w].append(pix[w, h])

    return output_list
```

Now that the data returned from `mapgen.py` passed the unit test `test_mapgen.py` in the `tests` directory using the test image, it was then time for the final object implementation.  The goal here was to take the list of lists with each index holding a color tuple, and use this information to construct a tilemap of colored blocks.  These blocks would need to interact with the ball and also be able to be destructible and countable so the game can know when there are no blocks left and end the game.  Thus, a new block class was created in the `sprites.py` file.  Each block contains the code for a color value, a rectangle which was a square value defined by `TILESIZE` in the `settings.py` file, and an x and y location in the tilemap.  Lastly, these blocks needed to be instantiated correctly based on the `output_list` from `mapgen.py`.  The `output_list` is stored in the game class as `self.map_data`.  Once the value was passed to the game class, the algorithm was much easier to figure out with the expected dataset being generated correctly.  The instantiation algorithm can be seen down below; note that any black tiles are ignored as the background is also black and this would make these tiles invisible:

```
for col, colors in enumerate(self.map_data):
    for row, color in enumerate(colors):
        if color == BLACK:
            pass
        else:
            Block(self, col, row + 4, color)
```

With these last 6 lines of code `BlockBuster.py` was nearly finished.  The last steps were to add a `show_start_screen()`, `show_wait_screen`, `show_gameover_screen`, and `wait_for_key()` methods.  The `show_*_screen` methods were all responsible for showing specific screens depending on the current state of the game.  When the game first started, it would use the `show_start_screen()` method which would draw an image on the screen with the title of the game and a note saying to "Press Any Key To Play".  Next, the `show_wait_screen` would happen after the ball collides with the death plane below the paddle, and if the amount of lives is less than the starting value and greater than zero. At this point a life would be subtracted from the Player class' `self.lives` variable.  If the amount of lives reaches zero, the Player is then prompted with a `show_gameover_screen`, which just says that the game is over.  If the player presses a key at this point, all values are reset and a new game begins.
