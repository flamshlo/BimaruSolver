we are going step after step. 
Step 1. 

i don't want anything besides what i ask for:  
its called bimaru solver 3.0
we are making only the grid and buttons nothing functional yet. 
then i'll tell you how to proceed:  
12x12 squares grid.   row and col 11 are disabled (gray). 
sidebar has:  
line 1:  Bimaru Solver version 3.0
line 2: button NEW GAME
line 3  game name:  date-time and index:  format yyyy-mm-dd n
line 4:  Mode:  Set up ship part counts. 
line 5: [disabed]  Play game

That's all.  Nothing else. No functionality yet. This is a place holder. 
DO NOT fill in any functionality or anything else

Step 2
1..  Change to Version text to 3.2
2. Disable entry to game grid. Only digits can be entered in the count rows. digits 0-8.  
3. Entering a digit moves cursor to next count cell. from last row to firs in col, from last in col to first in row. 
4. Arrows move up down in row-counter col (grid col 12). and left and right in col-counter row (grid row 12)
3. Disable entry to r12c12. 

NOTHING ELSE.  

Step 3:  change to version 3.3 
Add instruction area under Mode line:   Enter ship parts count. Once done you'll be able to enter hints. 

1. Keep everything from steps 1 and 2.
2. Only when all counts are entered move to hint entry mode: till then count entry mode. 
reminder: in count entry mode play grid is disabled and so is PLAY GAME button,. 
3. hint entry mode: grid enabled (10x10 enabled) entering digit changes to hint part or empty. PLAY GAME enabled. 
4. change mode to: "Set up hints"
5. Clicking on grid or entering a number toggles between hints:  SEA (Black X on white),  single (Black Circle), MID (black square), Black U parts:  Up, Down, Left, Right..
6. Entering ship-hints, and changing counts, checks ship hints against count, marks full count as green, missing parts as clear, and over-count as red (error) - and disables PLAY GAME. 
fixing count or hint re-enables Game Play if no count errors. 
7. Instructions: Enter Hints: Click on grid to toggle between SEA, MID, SINGLE, DOWN, LEFT, UP, RIGHT. Fix any errors. When done Press Play Game. 

Step 4. PLAY GAME PRESS. change to version 3.4
1. Keep all from steps till this. 
2. On PLAY GAME pressed 
3. Verify no over zero. 
3. Fill in deduced Sea parts (diagonals, sides not in direction of hinted ship. lines with all ships in count. 

Right mouse once clears a square then toggles to add question mark, or add exclamation mark. and again to clear. 
Dragging mouse on several squares set empty ones as SEA. 
