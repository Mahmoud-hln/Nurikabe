# Nurikabe
This project is a Prolog-based algorithm that solves a grid-based puzzle by placing "land" and "sea" cells on a grid. The solver respects a set of rules related to adjacency, connected regions, and fixed cells with numeric clues. The program uses logical constraints to ensure each cell placement follows the puzzle's rules.

## Table of Contents
- [Rules of the Puzzle](#rules-of-the-puzzle)
- [Algorithms Used](#algorithms-used)
  - [Breadth-First Search (BFS) for Connected Components](#breadth-first-search-bfs-for-connected-components)
  - [Constraint Checking](#constraint-checking)
  - [Backtracking for Constraint Satisfaction](#backtracking-for-constraint-satisfaction)
  - [Sea and Land Expansion Rules](#sea-and-land-expansion-rules)
- [How to Run](#how-to-run)

## Overview
The program divides the grid into regions of "land" and "sea," with certain cells initially fixed with numeric values. The goal is to fill the grid such that each island meets its number of required land cells, all sea cells form one contiguous body, and no 2x2 sea regions are created.

## Rules of the Puzzle
Each island must have exactly one fixed cell with the specified number of land cells adjacent or connected to it.
All sea cells must form a single, contiguous region.
No 2x2 block of sea cells is allowed on the grid.
All islands must be separated by at least one sea cell.

## Algorithms Used
1. **Breadth-First Search (BFS) for Connected Components**  
   The `bfs_sea` and `bfs_island` predicates are used to check connected components of sea and land cells, respectively. These functions help ensure that:
   - All sea cells form a single contiguous region.
   - Islands meet their size requirements based on the fixed cell constraints.
   
   BFS is implemented using a queue to explore each cell’s neighbors. It proceeds by adding neighbors to the queue if they haven't been visited yet.

2. **Constraint Checking**  
   Several constraints are enforced throughout the puzzle solution process to ensure all rules are followed:
   - `no_2_by_2_sea_blocks`: Ensures no 2x2 sea blocks are present by checking each cell and its neighbors.
   - `island_equals_one_fixed`: Verifies each island has only one fixed cell with the required number of adjacent land cells.
   - `lands_equals_fixeds`: Checks that all islands have been created with the exact number of land cells specified by the fixed cells.
   
   Each constraint is implemented as a Prolog predicate that ensures conditions are met across the grid.

3. **Backtracking for Constraint Satisfaction**  
   The program uses Prolog’s natural backtracking capabilities to handle conflicting placements:
   - When adding a land or sea cell, the solver checks all constraints (like connectivity, 2x2 blocks, and adjacency).
   - If a placement fails, it reverts and tries an alternative, allowing for dynamic adjustments until all conditions are satisfied.

4. **Sea and Land Expansion Rules**  
   The program includes specialized rules to handle the expansion of sea and land cells based on fixed-cell clues:
   - Sea Expansion (`add_sea_cells`): Automatically fills empty cells as sea if they are isolated from land cells.
   - Land Expansion (`add_land`): Adds land cells around fixed cells and prevents the creation of isolated cells.
   
   These functions ensure smooth filling of the grid while maintaining puzzle constraints.

## How to Run
1. Load the Prolog file in your Prolog interpreter.
2. Run the main predicate by executing `solving.` or `solved.` to begin the solution process.
3. Observe the output grid in the console, which shows the placement of land and sea cells.
