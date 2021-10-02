# Understanding Demining Code

Implementation of Demining is split into four files:

- `human.cpp` provide human-played version of Demining (UI)
- `main.cpp` provide AI version of Demining (UI)
- `board.cpp` provide basic structure of Demining
  - `grid` that stores the value of blocks
  - `click`, `tag`, `reset` method
    - after "tagging", corresponding block becomes "unclickable". You can reset it back to normal block by using `reset` method
  - `output`, used to output the grid
  - `finaloutput`, used to output the grid after game ends
- `ai.cpp` provide implementation of Demining AI.

For AI, Demining AI uses knowledge based AI. It uses the following idea to represent knowledge, and make induction:

```cpp
struct GridLocation{
  int x, y;
};

struct Knowledge{
	set<GridLocation> locations;
	int numberOfMines;
};
```

The idea is that if there are two pieces of knowledge $k_1$ and $k_2$ such that $k_1 \subset k_2$. Then, we can use our code to generate a new piece of knowledge $k_3$ such that $k_3.locations = k2.locations - k1.locations$ and $k3.numberOfMines = k2.numberOfMines - k1.numberOfMines$.

Since it is based on knowledge, the AI sometimes can only take random move because it may not have enought knowledge about the game, which means the AI will probability lose the game.