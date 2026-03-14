# Scheduling AI

A constraint-based tournament scheduling engine built in Python that generates complete, conflict-free fixture calendars across multiple overlapping competitions.

## The Problem

Scheduling sports tournaments sounds straightforward until you're dealing with all of this at once:

- **5 tournaments** running simultaneously
- **84 teams**, many with sister teams competing across multiple tournaments
- **384 league games** to be scheduled across a 3-month window
- **Ground availability** — limited venues with their own time and capacity constraints
- **80+ individual constraints** including team conflicts, rest days, travel, and shared resources

The core challenge wasn't scheduling one tournament. It was that every decision in one tournament rippled into the others. A team playing on Saturday in Tournament A might have a sister team that can't play Sunday in Tournament B because they share a ground. Solving one created a problem somewhere else.

Manual scheduling at this scale is effectively impossible without errors or conflicts. We needed an engine that could hold all 80+ constraints simultaneously and find a valid solution automatically.

## How It Works

The engine uses a **constraint satisfaction approach** built in Python:

1. **Input parsing** — teams, grounds, tournament structures, and all constraints are loaded and validated
2. **Conflict graph construction** — the engine maps out which teams, grounds, and time slots interact with each other across all 5 tournaments
3. **Constraint propagation** — before assigning any fixture, the engine eliminates impossible slots based on known conflicts
4. **Backtracking search** — where conflicts remain, the engine systematically tries assignments and backtracks when a dead end is reached
5. **Output validation** — every generated fixture is checked against all 80+ constraints before the final schedule is confirmed

The result: a complete 384-game calendar across 3 months with zero conflicts.

## Results

| Metric | Value |
|---|---|
| Tournaments scheduled | 5 |
| Teams | 84 |
| Total fixtures generated | 384 |
| Scheduling window | 3 months |
| Constraints handled | 80+ |
| Conflicts in final output | 0 |

## Stack

- **Language:** Python
- **Core approach:** Constraint satisfaction / backtracking search
- **Input/Output:** Structured data files for team, ground, and tournament configuration

## What I Learned

Building this made clear why scheduling is considered a hard combinatorial problem. The search space grows exponentially as you add teams and constraints. The interesting engineering challenge was making the constraint propagation efficient enough that the engine didn't need to brute-force every possibility — pruning bad branches early was the difference between a solution in seconds and one that never terminates.
