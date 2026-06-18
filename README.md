# Adversarial Search & Intelligent Agents for Othello

This repository contains a Python-based implementation of various adversarial search algorithms and heuristic strategies designed to solve and optimize gameplay in a 6x6 Othello (Reversi) board environment. This project has been developed as a B.Sc. Course Project for Artificial Intelligence at the University of Isfahan (UI).

The project demonstrates the application of game theory, look-ahead state evaluation, and branch pruning optimization to build highly competitive automated agents capable of neutralizing both baseline tactics and advanced game-tree paths.

---

## Implemented Agents

The project features four distinct gameplay strategies, structurally integrated to maintain architectural consistency and uniform state execution:

### Random Agent
* **Type:** Baseline / Stochastic Exploration
* **Behavior:** Randomly selects an arbitrary action from the list of legal moves on the board. It serves as a true stochastic baseline for tournament evaluation.

### Greedy Agent
* **Type:** Single-Step Heuristic (Immediate Exploitation)
* **Behavior:** Operates with zero future outlook. It evaluates immediate valid actions and greedily executes the move that yields the highest number of flipped opponent coins in that exact turn.

### Minimax Agent
* **Type:** Adversarial Search (Exhaustive Tree Search)
* **Behavior:** Explores the complete game tree up to a fixed depth of 3. It assumes perfect, rational play from the opponent—recursively maximizing its own utility at MAX layers while minimizing the opponent's utility at MIN layers.

### Alpha-Beta Agent
* **Type:** Optimized Adversarial Search (Pruning-Driven Meta-Search)
* **Behavior:** Yields identical theoretical move selections to Minimax but utilizes mathematical pruning bounds (Alpha and Beta). Whenever a branch condition yields Beta <= Alpha, the remaining sub-tree is instantly discarded, drastically lowering computational footprint and allowing deep look-aheads up to depth 4 within standard runtime bounds.

---

## Environment & Heuristic Formulation

The engine models a 6x6 square board initialized with four central overlapping pieces. Non-terminal leaf nodes are evaluated using a multi-factor linear heuristic formula:

Score = Coin_Parity + (2.5 * Mobility) + (15.0 * Corners)

* **Coin Parity**: The normalized ratio of the difference between player and opponent coins relative to total coins on the board.
* **Mobility**: Measures positional freedom by calculating the difference in the number of legal actions available to the agent vs. the opponent.
* **Corners**: Evaluates ownership of the 4 absolute board corners. Because corner pieces are un-flippable, they are treated as highly stable, permanent assets and assigned a dominant multiplier weight of 15.0.

---

## Tournament Configuration & Performance Summary

To guarantee statistical significance and eliminate first-mover advantage, the simulation uses a Round-Robin Tournament format running 20 games per evaluation pair. The starting turn color alternates strictly between even and odd matches.

The empirical results extracted from the execution engine are summarized below:

| Test Index | Agent 1 (Black/White) | Agent 2 (White/Black) | Total Matches | Agent 1 Wins | Agent 2 Wins | Draws | Agent 1 Win Rate |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **1** | **Minimax Agent (Depth 3)** | Random Agent | 20 | 19 | 1 | 0 | **95.0%** |
| **2** | **Alpha-Beta Agent (Depth 4)** | Random Agent | 20 | 20 | 0 | 0 | **100.0%** |
| **3** | **Minimax Agent (Depth 3)** | Greedy Agent | 20 | 20 | 0 | 0 | **100.0%** |
| **4** | **Alpha-Beta Agent (Depth 4)** | Greedy Agent | 20 | 20 | 0 | 0 | **100.0%** |
| **5** | **Alpha-Beta Agent (Depth 4)** | **Minimax Agent (Depth 3)** | 20 | 10 | 10 | 0 | **50.0%** |

> **Key Analytical Takeaway:** The exact 50%-50% split in the Head-to-Head test perfectly aligns with adversarial search theory. It empirically proves that Alpha-Beta Pruning acts as a pure computational optimization; it never alters the strategic solution space of Minimax, but achieves identical conclusions while processing a fraction of the search nodes.

---

## Code Structure & Footprint

The repository is organized under a modular object-oriented layout:
* **`game/othello.py`**: Houses core logic environment rules, executing legal move extraction (`get_valid_moves`), transition tracking (`make_move`), deep environment cloning (`copy`), and terminal state verification (`game_over`).
* **`agents/`**: An isolated directory containing the agent scripts (`random_agent.py`, `greedy_agent.py`, and the intelligent tree search entities).
* **`main.py`**: The master script managing the round-robin tournament loop, match orchestration, and terminal win-rate outputs.

---

## Environment & Requirements

* **Language:** Python 3.x
* **Core Standard Dependencies:** `random`, `math`, `copy`

---

## Academic Context

* **Institution:** University of Isfahan (دانشگاه اصفهان)
* **Degree:** Bachelor of Science (B.Sc.) in Computer Science
* **Course:** Artificial Intelligence (درس هوش مصنوعی)
* **Professor:** Dr. Faria Nasiri Mofakham

### Group Members
* **Farnoush Pourshaban** - [Student ID: 4024023007]
* **Yeganeh Rastegari** - [Student ID: 4014013040]
* **Farzaneh Salimi** - [Student ID: 4014013059]
