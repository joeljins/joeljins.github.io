---
layout: default
title: IQ Puzzle 
permalink: /iq_puzzle/
---

## Solving the IQ Puzzle
<br>
Explanation of the [game](https://blog.crackerbarrel.com/2021/08/13/how-to-beat-the-cracker-barrel-peg-game/):

> Sometimes referred to as “Peg Solitaire” or “Hi-Q”, this simple game has been entertaining our guests for decades, plus it’s a great way to give your noggin a mini workout.  
>  
> **How to Play the Cracker Barrel Peg Game**  
>  
> Place a peg in each of the holes of the game board. You’ll have one place on the board that won’t have a peg.  
>  
> Jump one peg over another to an open space and remove the one that was jumped. Keep doing this until only a single peg remains.  
>  
> If you are successful and leave only one peg, you are a “genius.”  
>  
> Leave two pegs, and you’re “pretty smart.”  
>  
> Leave three pegs, and you are just plain “dumb.”  
>  
> But leave four pegs, and sorry, but you are an “EQ-NO-RA-MOOOSE.” (it’s all in good fun – no judgement here!)

<br>
In an assignment exploring artificial intelligence in games, I was provided with a module to run the IQ puzzle game. Each possible grid arrangement is represented as a node, and each node points to the previous grid arrangement that led to the current configuration.

The search algorithm maintains two lists: open nodes (those yet to be explored) and closed nodes (those that have already been explored). For each node in the open list, the result of each legal move is added to the end of the open list.

Depth-first search (DFS) pops nodes from the end of the open list (LIFO).

Breadth-first search (BFS) and A search* pop nodes from the beginning of the open list (FIFO)

The heuristic used for A* was the number of legal moves (descending). In each iteration of the search, the list of open nodes are sorted by this value. 

<br>
Run the following commands to show the optimal solutions and the number of paths search to find the optimal solution:

```
python3 search.py bfs
```
![IQ Puzzle](\assets\images\iq_puzzle_bfs.png)


```
python3 search.py dfs
```
![IQ Puzzle](\assets\images\iq_puzzle_dfs.png)


```
python3 search.py a_star
```
![IQ Puzzle](\assets\images\iq_puzzle_a_star.png)


All other commands are invalid. 