# Rubik’s Cube Solver in C++
### Project Overview

This project focuses on implementing a Rubik’s Cube solver in C++ that transforms a given starting configuration of the cube into a desired goal configuration. The solver uses two different search techniques:

1) Iterative Deepening Search (IDS) – an uninformed search strategy.
2) A* – an informed search strategy that relies on heuristics.

The program accepts as input a file containing two lines:
-> The first line represents the initial state of the cube.
-> The second line represents the target state.

Each configuration is expressed as 54 space-separated digits, corresponding to the six faces of the cube. Each digit belongs to {1, 2, 3, 4, 5, 6}, denoting colors. The first 9 digits correspond to the front face, followed by back, top, bottom, left, and right faces in that order.

Every 90° rotation of a face—clockwise or counterclockwise—is counted as one move. The output is a sequence of such moves required to solve the cube.

# Methodology
### Iterative Deepening Search (IDS)

In IDS, we explore states depth by depth. A stack structure is used to keep track of nodes. At each step:

-> The top node is removed and checked against the goal state.
-> If the goal is not reached and the depth limit has not been exceeded, all 12 possible moves are generated to create new states, which are pushed onto the stack.
-> This process continues until either the goal is found or the depth limit is reached.

### A* Search
For the informed strategy, A* search is employed.

-> Each node is evaluated using a heuristic function that estimates its closeness to the goal.
-> The cost function is defined as:
𝑓(𝑛)=𝑔(𝑛)+ℎ(𝑛) where 𝑔(𝑛) is the path cost from the start node and ℎ(𝑛) is the heuristic estimate of the remaining cost.
-> Two lists (OPEN and CLOSED) are maintained. At each iteration, the node with the lowest cost is selected from OPEN. If a successor already exists in OPEN or CLOSED with a better cost, it is ignored; otherwise, it is added for further exploration.
-> The heuristic used here is the count of mismatched positions compared to the goal state.

### Results

-> IDS performs adequately when the cube is only a few moves (5–10) away from the solution. However, as the depth increases, the search space grows exponentially. At depths beyond 12, memory usage becomes extremely high, and execution may take hours or even crash due to exhaustion of resources.
-> A* performs significantly better. By prioritizing states closer to the goal (based on the heuristic), it avoids unnecessary exploration and typically finds solutions much faster and with less memory. However, its performance strongly depends on the quality of the heuristic—better heuristics yield faster, more optimal solutions.

### Conclusion

From the experiments, it is evident that A* outperforms Iterative Deepening in both efficiency and solution quality. IDS suffers from exponential growth in states and quickly becomes impractical at larger depths. In contrast, A* reduces the search space by making informed choices, requiring fewer nodes to be expanded and consuming less time and memory.

That said, A* is only as good as the heuristic guiding it. With a well-designed heuristic (like the mismatch count used here), it can deliver solutions much faster and more optimally. If the heuristic is poor, however, A* may take longer or produce less efficient results.

In summary, A* proves to be the more effective approach for solving the Rubik’s Cube transformation problem in this project, while Iterative Deepening illustrates the limitations of uninformed search strategies in complex problem spaces.
