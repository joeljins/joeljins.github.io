---
layout: default
title: Connect 3 
permalink: /connect_3/
---
## Creating the Optimal Connect 3 Agent
<br>
*Source [code](https://github.com/joeljins/connect_3_solutions) kept private to respect Drexel's academic integrity policies.*

<br>
Explanation of the [game](https://groupgames101.com/connect-four-rules/):

> ### Connect Four Rules  
>
> Player 1 drops a disc into any of the slots at the top of the grid.  
>
> Player 2 drops a disc into any of the slots at the top of the grid.  
>
> Players will alternate turns in this manner until someone gets four-in-a-row vertically, horizontally, or diagonally.

For simiplicity's sake, this implementation only requires three-in-a-row to win.

<br>
*There are three agents:*

### Human
This agent allows players to use the commandline to choose which of the four slots they wish to drop their disc in.

### Random
This agent randomly chooses the column the disc is dropped into.

### Minimax
This agent chooses the optimal column using the minimax algorithm. 

<br>
### A Short Demo:
This demo shows the minimax agent vs random. The minimax should be able defeat the random agent a majority of the time. 



