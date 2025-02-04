# Sokoban (倉庫番): A User Guide
Welcome to Sokoban, a classic puzzle video game where you, a warehouse worker, are tasked with strategically pushing boxes around an into target spots. Sounds easy, right? You’re correct! Unlike in the original game of Sokoban, this version only requires you to push one box into one target. That’s it! However, there are still other aspects of this game that may keep you entertained. This manual will do a deep dive of these elements as well as handling the game itself. 

## Overview
This version of Sokoban is a rectangularly-grided puzzle game where the player must push a box around a warehouse. This is a very simple concept, with only one caveat: you can only push the box, and not pull. This means that pushing the box into the corner may ruin your entire run! Generally, the challenge of this game is to find a way to push the box into its designated spot in the shortest number of moves as possible. 

Here’s what you need to know:
- You can only move one tile at a time.
- You can’t push a box through a wall.
- Finish the game in as few moves as possible.

And now you know enough to get the game started! Continue onto the next section where we discuss the basics of getting the game to run correctly. 

## Starting the game
First, make sure you have the code file for the game. It has been included in this repo. All you need to do is copy the ALL the text. Once you have copied the text:
<ol>
  <li>Go to <strong>cpulator.01xz.net</strong>, or use this <a href="https://cpulator.01xz.net/?sys=rv32-spim"><strong>link</strong></a></li>
  <li>Your immediate prompt should be to choose a system. You want to select “RISC-V RV32” in the architecture section and “RISC-V RV32 SPIM” in the system section</li>
</ol>

Congratulations, you have successfully navigated to the correct website! There is going to be a lot on the screen—you can ignore most of this! On the right, there is a screen that is captioned “Terminal”. This is where the game will be outputted. 

We will now paste the code you have copied into the editor terminal in the centre of the page. Remove anything already in the editor panel and paste what you copied from the document included in the repository. 

Before we can run the game, locate the small “settings” section under the “registers” section on the left. You may drag to enlarge the section, much like you would when resizing an application on your computer. Your first order of business is to find the checkbox labeled "function nesting too deep". Uncheck it.

Now return to the editor's panel. At the very top (scroll up back up) we see ".data" and "gridsize: .byte height,width". Choose your board size by replacing the numbers for “gridsize” under .data in the editor section. For example, if I wanted an 10 by 10 grid, I would enter change this to '10,10’.

<strong>IMPORTANT: </strong>Due to the way the code is being run, please make sure that one dimension is at least 7. Additionally, the board can not be less than 3 pixels wide or long. 

Once you have decided on your board size, press “compile and load” followed by “continue” at the top of the page. Alternatively, just press F5, then F3. Now we are ready to play the game! Continue into the next section where we discuss some of the features of the game and how to use the controls of the game.

## Playing the Game
Once you have compiled and loaded the game, you should be prompted to enter the number of players that are going to be playing the game. This is the multiplayer feature of the game. You do not need to have multiple players to play. 

### General Information
A board should have been printed to the screen by now. It should look something like this (using a 10 by 10 board):
```
How many players? 1                                                                                 
##########                                                                                          
#********#                                                                                          
#**P*B***#                                                                                          
#********#                                                                                          
#****T***#                                                                                          
#********#                                                                                          
#********#                                                                                          
#********#                                                                                          
#********#                                                                                          
##########                                                                                          
Player 1
```

#### Symbol meanings:
Noticing the strange symbols? Here’s what they mean:
-	P is you! This your character representation.
-	T is the target. This where you should be pushing the box to.
-	B is the box. This is what you will be pushing.
-	\# is a wall. You can not pass through it.
-	\* is empty space. You may move freely through here.

#### Game Inputs:
To be able to play the game, you should know the 7 basic inputs that are allowed in the game:
1.	Move up. (0)
2.	Move down. (1)
3.	Move left. (2)
4.	Move right. (3)
5.	Undo move. (7)
6.	Reset game. (9)
7.	Quit game. (10)

Each of these inputs are assigned a value that must be entered into the terminal for the move to render correctly. Only one move can be processed at a time. 

For example, if I wanted to move left, then up, then down, I would enter:
- 2, then hit enter and wait for the board to reprint.
- 0, then hit enter and wait for the board to reprint.
- 1, then hit enter and wait for the board to reprint.

<strong><ins>Single Player</ins></strong>

While there is a multiplayer aspect for this version of Sokoban, the game is primarily designed to be played single player. Simply enter “1” when prompted for the number of players at the beginning of the game. 

Your player number will be printed below the board, like in the image above. Once you have finished the game, the console will automatically prompt you if you would like to play again. If you would like to, simply enter 0. If you do not, enter 1, or any other number. 

<strong><ins>Multiplayer</ins></strong>

When prompted by the console, enter the number of players and press enter. There are no rounds in this system, rather, each player takes a turn to complete the entire board. Once a player has completed the board, the same board is reset for the next player to complete. You can check whose turn it is by looking at the bottom of the board, where the player number is listed. 

### Additional Information:
- A leaderboard of scores is printed at the end of each game (ie, when all players have completed the board in a multiplayer game)
- The “reset board” input resets the board to its original state and resets the number of moves taken.
- The “undo move” input allows you to go back one move. Each player can undo an unlimited number of times, (which also decreases the number of moves), but as a challenge, it is suggested that users not use this function.
- The “quit game” input force stops the game and exits entirely.

## Common Problems and Fixes:
As with most other games, you will often find yourself stuck with an unforeseeable bug or unable to continue playing the game. In this game, you will find your error message in the “messages” box at the bottom of the page. Like with the settings page, you may wish to enlargen this in the situation where an error does occur. 

Here are some common problems and solution: 
### “Instruction opcode differs from original executable”

This is most likely caused by the “reset” button at the top of the screen. As a result of the way the code works, static data, or in this case, the number of players is being changed within the loop. This prevents us from directly resetting by using this button. 

Instead, you want to follow the same steps as in the startup instructions if you want to reset the game. That is, hit compile and load before pressing continue.

#### “Function calls nested too many levels”

This is because you did not turn off this setting like specified earlier in this manual! Go into your settings panel and uncheck “function nesting too deep”.

#### Game is infinitely looping

This is likely because of the way the game is trying to compute random positions for the box, target, and player. This typically occurs usually when the board size is relatively small (i.e. a 5 by 5).

To fix this problem, simply just increase the size of the board. It is recommended that at least one of the dimensions of the board should be at least 7. However, this error can still happen when the size of the other dimension is relatively small (or for larger boards, the randomizer is likely infintely looping).

It is possible to play a game with size 3 by 7 or vice versa, however, there are very limited options for where the randomizer may place the box, character, and target. Hence, it is optimal to keep the board size larger. Besides, it’s more fun when there’s more board space!

