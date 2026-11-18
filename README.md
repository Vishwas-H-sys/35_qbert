# Q*bert Repair Lab

This project is a single-file Q*bert-lite clone using **Pygame**. It introduces students to isometric projection, diagonal hop validation, and enemy chase behavior using a small, readable object-oriented codebase.

---

## What's Provided

The completed Q*bert-lite game includes:

- A pyramid of cubes the player hops across diagonally, painting each cube toward its target color on landing
- Coily, an enemy that chases the player across the pyramid, and red balls that roll downward
- Falling off the edge of the pyramid (or bumping an enemy while grounded) costs a life
- Levels, lives, and scoring, with a win once every cube reaches its target color

The projection bug has been fixed, and the optional palette, cube-completion flash, and bonus-life features are implemented. The original lab tasks are retained below as a record of the assignment.

### **Use an LLM (e.g. ChatGPT or Claude) as your debugging and pair-programming partner for this lab.**

---

## Getting Started

### Setup

1. Make sure you have Python 3.10+ installed.
2. Install dependencies in a virtual environment. On macOS with Python 3.14, use pygame-ce (it imports as `pygame`):

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install pygame-ce
```

3. Run the game:

```bash
python game.py
```

**Controls:** Left/Up/Down/Right to hop diagonally, `R` to reset, Space to continue after clearing a level.

---

## Tasks to Complete

Each task must be completed using an iterative process involving LLM suggestions and your critical code review.

### Task 1: Fix the pyramid projection bug

> Each cube's screen position is computed from its `(row, col)` grid coordinates, and the whole pyramid should come out as a symmetric triangle. In the current build the pyramid is visibly skewed from the very first frame — rows drift sideways in a way that breaks the triangular symmetry. Look at the arithmetic combining `row` and `col` in `cube_center`, and check whether the row offset should be using integer division or true division.

### Task 2: Implement `cube_palette(level)`

> Called once per frame in `draw`, as `colors = cube_palette(self.level) or DEFAULT_PALETTE`. It receives the current level number and should return a list of `TARGET + 1` (currently 3) `(r, g, b)` colors — one per stage from unpainted to fully painted — or `None` to keep `DEFAULT_PALETTE`. Idea: return a different 3-color palette for each level.

### Task 3: Implement `on_cube_completed(cell)`

> Called from `paint()` the instant a specific cube first reaches its target stage — not on every hop onto it, only the hop that finishes it. It receives the `(row, col)` cell that was just completed. Its return value is ignored. Idea: a brief flash on that cube, or a small bonus beyond the 25 points already awarded per paint step.

### Task 4: Implement `bonus_life_threshold()`

> Called every frame in `update()`. It takes no arguments and should return an integer score value, or `None` to disable bonus lives entirely. Whenever the score crosses a multiple of that value for the first time, one life is awarded automatically — the bookkeeping (`self.bonus_awarded`) is already implemented, so you only need to choose the threshold. Idea: return `1000`.

---

## Expected Behavior

- The pyramid renders as a symmetric triangle of cubes
- Landing on a cube advances its color exactly one stage, only once per hop
- Hopping off the edge of the pyramid makes the player fall and costs a life
- Coily chases *toward* the player's current position rather than away from it
- Painting every cube to its target color wins the level; running out of lives ends the game

---

## Folder Structure

```
qbert/
├── game.py
└── README.md
```

---

## Submission Checklist

Submission is only the following three things:

- [] A 10-second video of gameplay **before** your changes, showing the bug/broken behavior
- [] A 10-second video of gameplay **after** your changes, showing the bug fixed and the new features working
- [] The Chat/LLM used page link, with the complete chat history


## Completed work

- Fixed the isometric pyramid projection by using true division (`row / 2`) for the row offset, keeping odd and even rows centered symmetrically.
- Added three level palettes, cycling as the player advances.
- Added a short flash when a cube first reaches its target color.
- Set the extra-life threshold to 1,000 points.
- Kept Coily's existing move selection, which chooses a neighboring cube closer to the player's position.

## Gameplay recordings

- `qbert_before.mov` shows the original projection bug.
- `qbert_after.mov` shows the repaired game and gameplay.

Run with `python game.py` from this folder (after activating the virtual environment).
