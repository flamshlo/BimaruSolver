# Bimaru Solver Version Checklist

## 1. Bimaru Rules and Definitions
- [ ] 1.1 Counts: Row and column ship part totals. 
- [ ] 1.2 Hints: Pre-filled ship and sea segments 
- [ ] 1.3 Parts: Definite, tentative, solved (ship/sea)
- [ ] 1.4 Adjacency (clashes): Ship-parts not adjacent in any direction. 
-- Conclusions: 
-- Diagonals to a ship-part must be Sea.
-- Sides perpendicular to adjacent ship-parts must be sea.
-- Capped ship-hint sides must be sea. (So a TB single part circular ship is completely surrounded by sea. )
- [ ] 1.5 Ships: 1 carrier(4 parts), 2 battleship(3), 3 destroyer(2), 4 torpedo(1 part: circle)
- [ ] 1.6 Solution:
-- [ ] 1.6.1 Exactly all ships must be in solution. 
-- [ ] 1.6.2 All rows and columns filled according to their count cells.

## 2. UI Layout
### 2.1 board
- [ ] 2.1 Board Grid (12x12): 10x10 Game grid, Col 12: Row counts, Row 12: Col counts
// move this to looks section - [ ] 2.2 Visuals: Crimson/emerald/turquoise glass parts, deep brown engraved wood board
// also:  rounded button tips. professional board game look.
// also there: list orange  warning indicators:  adjacent game cells, count cells (too many ships), cannot play LED (not solvable), red led indicator (missing counts)

### 2.2 Sidebar
- [ ] 2.2 Sidebar
-- [ ] 2.2.1 Top (always)  Bemaru-Solver Logo (Text), Version, [i button] (future use: instructions),
  --- New Game (always enabled)
  --- Game name, Save / Reset , Saved list (with Delete X), 
  --- Status/Instructions: Text area
  --- Valid-LED and Play. 

## 3. Modes

### 3.1 Count Entry setup mode
- [ ] 1 From: New Game or initial game.
-- [ ] a. Clears Game grid and Counts.
-- [ ] b. Sets game name. format: yyyy.mm.dd - nnn index for today. 
-- [ ] c. Enables: Name edit, Counts, List, Delete;   Disables: Game Grid, Play, Save;
-- [ ] d. Resets: Empty counts and grid.
-- [ ] e. Hides: (nothing)
- [ ] 2 Data entry:
-- [ ] 2.1  Counts 
-- [ ] a. single digit.
-- [ ] b. cyclic auto-advance - row to column back to row indefinitely
-- [ ] c. arrows (up/down on col, left/right on row) navigate
-- [ ] d. backspace on cell clears cell and moves to one before
-- [ ] e. delete clears cell
-- [ ] f. if has ship hints in row/col, compare and mark solved/over/incomplete. warn if over. 
- [ ] Digit entry auto-advance; backspace resets/moves back
- [ ] 3.1.3 Auto-sea: Detected per row/col; exits stage when all filled

### 3.2 Setup Mode: Hint Entry
- [ ] 3.2.1 Entry: Counts filled/loaded; Enabled: Grid, Counts, Save; Disabled: Play
- [ ] 3.2.2 Inputs: T/M/S/U/D/L/R shortcuts; Right click clear
- [ ] 3.2.3 Play Validation: Tests counts, sea, hints, solubility; blocks Play if invalid

### 3.3 Gameplay Mode
- [ ] 3.3.1 Entry: Passed Validation; Enabled: Grid (part toggle)
- [ ] 3.3.2 Mouse: Drag marks/unmarks sea; click toggles ship/sea
- [ ] 3.3.3 Logic: Double-click solved (round corners); check limits; mark clashes orange 
- [ ] 3.3.4 Completion: Flashing green glow (3x)

## 4. Global Visuals
- [ ] 4.1 Animation: Throbbing arrow at input location
- [ ] 4.2 Part Definitions: Definite (Dark Green/polka dot), Tentative (Red ?), Solved (rounded corners)
- [ ] 4.3 Sea Definitions: Definite Sea (Navy blue/red X), Detected Sea (Dark light-blue/small X)
- [ ] 4.4 Hint Parts: Torpedo(circle), Mid(square), End(U/D/L/R), Sea Hint(wavy lines)

---

**Error Remark:** 4.3(A-D)
