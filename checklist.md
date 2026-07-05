# Bimaru Solver Checklist

**IMPORTANT: This is a PUZZLE ENTRY and SOLVING APPLICATION. The user enters the entire puzzle (counts and hints) during setup mode. The application does NOT generate puzzles.**

## 1. Bimaru Rules and Definitions
- [ ] 1.1 Counts: Row and column ship part totals
- [ ] 1.2 Hints: Pre-filled ship and sea segments set on the board by the player during setup stage
- [ ] 1.3 Playing-Parts: Ship and sea parts set on the board by the player during gameplay stage
- [ ] 1.4 Adjacency (clashes): Ship-parts not adjacent in any direction
  - Diagonals to a ship-part must be Sea
  - Sides perpendicular to adjacent ship-parts must be sea
  - Capped ship-hint sides must be sea (single part circular ship is completely surrounded by sea)
- [ ] 1.5 Ships: 1 Aircraft-Carrier (4 parts), 2 Battleships (3 parts), 3 Destroyers (2 parts), 4 Torpedoes (1 part)
- [ ] 1.6 Solution:
  - [ ] 1.6.1 Exactly all ships must be in solution
  - [ ] 1.6.2 All rows and columns filled according to their count cells
  - [ ] 1.6.3 OVER: Error state when more parts in row or col than count cell
  - [ ] 1.6.4 Solved/Incomplete: Count cells marked based on correctness

## 2. UI Layout
### 2.1 Board
- [ ] 2.1.1 Board Grid (12x12):
  - [ ] 10x10 Game grid (rows 1-10, columns 1-10)
  - [ ] Row 11: Empty (padding)
  - [ ] Column 11: Empty (padding)
  - [ ] Row 12: Column count cells
  - [ ] Column 12: Row count cells
- [ ] 2.1.2 Grid Modes:
  - [ ] Count Entry mode: Count cells active, game grid disabled, hints disabled
  - [ ] Hint Entry mode: Game grid active for hints, count cells continue from previous mode
  - [ ] Gameplay mode: Game grid active for playing-parts, count cells disabled, hints disabled
- [ ] 2.1.3 Count Cell Status:
  - [ ] Solved (correct number of parts placed)
  - [ ] Incomplete (waiting for more parts)
  - [ ] Over (too many parts - error state)

### 2.2 Sidebar
- [ ] 2.2.1 Header:
  - [ ] Bimaru-Solver Logo (text)
  - [ ] Version display
  - [ ] Info button (future use for instructions)
- [ ] 2.2.2 Controls:
  - [ ] New Game button (always enabled)
  - [ ] Game name textbox (setup mode) / label (gameplay mode)
  - [ ] Save button (disabled until entry started)
  - [ ] Reset button
- [ ] 2.2.3 Saved Games List:
  - [ ] Display saved games (setup mode only)
  - [ ] Load game on click
  - [ ] Delete button (red X) per game

## 3. Modes & Functionality

### 3.1 Count Entry Setup Mode
- [ ] 3.1.1 Activation (New Game / Initial Game):
  - [ ] Clears Game grid and Counts
  - [ ] Updates Status text
  - [ ] Sets game name (format: yyyy.mm.dd - nnn index for today)
  - [ ] Enables: Name edit, Counts, List, Delete
  - [ ] Disables: Game Grid, Play, Save
- [ ] 3.1.2 Data Entry - Counts:
  - [ ] Single digit input only
  - [ ] Cyclic auto-advance (row to column and back indefinitely)
  - [ ] Arrow navigation (up/down for columns, left/right for rows)
  - [ ] Backspace clears cell and moves back one cell
  - [ ] Delete clears current cell
- [ ] 3.1.3 Data Validation:
  - [ ] Auto-sea detection per row/col based on counts
  - [ ] Auto-sea marked in grid
  - [ ] Auto-sea skips existing hints
  - [ ] Exits stage when all count cells filled

### 3.2 Setup Mode: Hint Entry
- [ ] 3.2.1 Activation (after counts filled or game loaded):
  - [ ] Enables: Grid (for hint placement), continue Counts if needed, Save
  - [ ] Continues: List, Delete
- [ ] 3.2.2 Hint Inputs:
  - [ ] Mid (middle of ship)
  - [ ] Sea (water)
  - [ ] Up (top end of ship)
  - [ ] Down (bottom end of ship)
  - [ ] Left (left end of ship)
  - [ ] Right (right end of ship)
  - [ ] Single (complete 1-part ship)
  - [ ] Right-click to clear hint
- [ ] 3.2.3 Play Button Validations (before entering Gameplay):
  - [ ] Test counts validity
  - [ ] Test auto-sea application
  - [ ] Test directed hints and directional consistency
  - [ ] Test solubility (puzzle can be solved)
  - [ ] FUTURE FEATURE: Verify ship counts achievable
  - [ ] Block Play if any validation fails (show warnings)
  - [ ] On validation failure: Mark adjacent hints, stay in setup mode

### 3.3 Gameplay Mode
- [ ] 3.3.1 Activation (after Play button passes validation):
  - [ ] Enables: Grid (playing-part toggle)
  - [ ] Disables: Count cells, Hint entry
  - [ ] Changes Save to Reset
  - [ ] Hides Saved games list
- [ ] 3.3.2 User Input:
  - [ ] Drag marks/unmarks sea (skipping hint and ship parts)
  - [ ] Click toggles ship/sea
- [ ] 3.3.3 Game Logic:
  - [ ] Detect ships: ensure all required ships are placed
  - [ ] Check row/col limits against count cells
  - [ ] Detect and mark clashes (error state)
  - [ ] Double-click marks solved (visual indicator)
- [ ] 3.3.4 Completion Detection:
  - [ ] All required ships placed
  - [ ] All rows/cols match their counts
  - [ ] All cells filled (no empty cells)
  - [ ] No clashes
  - [ ] Display completion message

## 4. Core Functionality Checklist
- [ ] 4.1 Grid rendering (12x12 with structured layout)
- [ ] 4.2 Count cell management and validation
- [ ] 4.3 Hint placement and storage
- [ ] 4.4 Auto-sea calculation and marking
- [ ] 4.5 Ship placement and adjacency checking
- [ ] 4.6 Clash detection and marking
- [ ] 4.7 Game state management (count entry, hint entry, gameplay)
- [ ] 4.8 Save/Load functionality
- [ ] 4.9 Game completion detection
- [ ] 4.10 Input handling (keyboard, mouse, drag)
