---
layout: default
title: Connect 3 
permalink: /connect_3
---
# Creating the Optimal Connect 3 Agent
<br>
*Source [code](https://github.com/joeljins/connect_3_solutions) kept private to respect Drexel's academic integrity policies.*

## A Quick Demo:
This demo shows the minimax agent vs random. The minimax should be able defeat the random agent a majority of the time. 

<iframe src="https://drive.google.com/file/d/1p74oLOTRQ81AS1mv_OWzh7Z2a2J-54GM/preview" width="640" height="480" allow="autoplay"></iframe>

<br>
Explanation of the [game](https://groupgames101.com/connect-four-rules/):

> *Connect Four Rules*
>
> Player 1 drops a disc into any of the slots at the top of the grid.  
>
> Player 2 drops a disc into any of the slots at the top of the grid.  
>
> Players will alternate turns in this manner until someone gets four-in-a-row vertically, horizontally, or diagonally.

For simiplicity's sake, this implementation only requires three-in-a-row to win.

<br>
*There are three agents:*

## Human
This agent allows players to use the commandline to choose which of the four slots they wish to drop their disc in.

## Random
This agent randomly chooses the column the disc is dropped into.

## Minimax
This agent chooses the optimal column using the minimax algorithm.

### How the Minimax Algorithm Works:

<style>
ul {
      list-style-type: square; /* Square bullet points */
      margin-left: 20px; /* Indentation */
      padding-left: 0; /* Remove extra padding for lists */
    }
</style>

<ul>
    <li>
A tree is used to represent the game, where each edge represents a legal move, and each node represents the resulting state from the legal move.
    </li>
    
    <li>
There are two players, the maximizer and the minimizer. The maximizing player, the current player/agent, chooses the move that will result in the best possible outcome. The minimizing player, or the opponent, chooses the move that will result in the worst possible outcome for the maximizing player. 
    </li>

    <li>
Each state is assigned a score. A winning state usually results in a high score, and a losing state results in a low score. To evaluate none winning/losing states, there are other metrics. For Connect 3, this could be the number of actions, where more actions result in a lower score. 
    </li>

    <li>
    Using recursion, the row of nodes are evaluated, and the greatest value is chosen as the next move. 
    </li>
</ul>

