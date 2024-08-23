I) Compilation instructions
- Compilation is done from the command line, using the Makefile, and the headers
  and sources are located in the sources folder.

II) Details about the project structure
1) The project contains the following headers:
-> hlt.hpp
-> networking.hpp
-> Robot.hpp
2) The project contains the following sources:
-> Robot.cpp
-> myBot.cpp
3) Additionally, the project contains a Makefile with the required rules for:
-> build 
-> clean
-> run

III) Implementation details
1) The actual implementation of the bot is done in the Robot class. The bot applies
   the following strategy:
- The cells inside the occupied territory will search for the nearest border,
  and if it doesn't exist, they will stay in place.
- The border cells use a greedy approach to attack the yet unoccupied pieces.
  Thus, a piece will attack as soon as possible, and if there are multiple
  such cells that can be attacked, then the piece with the highest score will be chosen.
- If a border cell cannot attack, then it will look for a neighboring border cell
  with which it can combine, without causing an OVERFLOW. 
  For this, a matrix with the strengths of the cells (strength_map) is maintained.
- Following the model from links [2] and [3], the border cells now prioritize
  the most vulnerable enemy cells.
- For the final deadline, I changed the save_strength function for a better heuristic:
  -> Combines Greedy with DP.
  -> The main idea is that, still for cells with 255 strength, it doesn't just look
  at the current move, but also looks at the next cell trying to redirect as much
  excess power as possible to help as many of the surrounding cells as possible.
  Either to conquer a neutral cell or an enemy one. For the enemy cell, it even
  looks at a location after the first enemy cell to transfer even more power.
  And as long as it's still at maximum power, it will keep redirecting power. I put
  emphasis on the offensive part, in the sense that I prioritize cells that are fighting.

2) Complexity:
- Let width be the length of the board and height be the width of the board
- Making a move will be done in constant time O(1) for the border cells
  (exterior), and for an interior cell it will be done in O(height) 
- The power correction remains O((width * height) ^ 2).
- So, the total complexity of the algorithm used will be determined by
  the power correction (which is the largest), that is O((width * height) ^ 2).

IV) Sources of inspiration
1) I started the implementation from the tutorials on the game's website and from
   forums:
[1] - https://2017.halite.io/learn-programming-challenge/downloads-and-starter-kits/improve-basic-bot
[2] - https://2016.forums.halite.io/t/so-youve-improved-the-random-bot-now-what/482.html
[3] - https://2016.forums.halite.io/t/published-bot-source-code/987.html
2) Additionally, I analyzed the strategies used by other players within the
   project:
[4] - https://pa.readerbench.com/