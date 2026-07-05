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

## 2. UI Layout & Board Structure

**CRITICAL: The board is the SAME physical 12x12 grid used for all modes. Different modes enable/disable different cell types.**

### 2.1 Board Grid Structure
- [ ] 2.1.1 Board Grid (12x12):
  - [ ] 10x10 Game grid (rows 1-10, columns 1-10)
  - [ ] Row 11: Empty (padding)
  - [ ] Column 11: Empty (padding)
  - [ ] Row 12: Column count cells
  - [ ] Column 12: Row count cells

### 2.2 Board Cell Types & Mode Behavior
- [ ] 2.2.1 Count Cells (Row 12, Column 12):
  - [ ] Count Entry mode: ENABLED for input
  - [ ] Hint Entry mode: ENABLED for input (counts can be changed)
  - [ ] Gameplay mode: DISABLED (locked, read-only)
- [ ] 2.2.2 Hint Cells (10x10 grid during setup):
  - [ ] Count Entry mode: DISABLED (locked, read-only)
  - [ ] Hint Entry mode: ENABLED for toggle/clear
  - [ ] Gameplay mode: DISABLED/LOCKED (cannot be modified or deleted)
- [ ] 2.2.3 Auto-Deduced Sea Cells:
  - [ ] Count Entry mode: Marked automatically from counts
  - [ ] Hint Entry mode: Visible but locked (read-only)
  - [ ] Gameplay mode: DISABLED/LOCKED (cannot be modified or deleted)
- [ ] 2.2.4 Playing-Part Cells (10x10 grid during gameplay):
  - [ ] Count Entry mode: DISABLED (locked)
  - [ ] Hint Entry mode: DISABLED (locked)
  - [ ] Gameplay mode: ENABLED for toggle (ship/sea/empty)

### 2.3 Sidebar
- [ ] 2.3.1 Header:
  - [ ] Bimaru-Solver Logo (text)
  - [ ] Version display
  - [ ] Info button (future use for instructions)
- [ ] 2.3.2 Controls:
  - [ ] New Game button (always enabled)
  - [ ] Game name textbox (setup mode) / label (gameplay mode)
  - [ ] Save button (disabled until entry started)
  - [ ] Reset button
- [ ] 2.3.3 Saved Games List:
  - [ ] Display saved games (setup mode only)
  - [ ] Load game on click
  - [ ] Delete button (red X) per game

## 3. Modes & Functionality

### 3.1 Count Entry Setup Mode
- [ ] 3.1.1 Activation (New Game / Initial Game):
  - [ ] Clears Game grid and Counts
  - [ ] Updates Status text
  - [ ] Sets game name (format: yyyy.mm.dd - nnn index for today)
  - [ ] Enables: Name edit, Count cells only
  - [ ] Disables: Hint cells, Playing-part cells, Play button
- [ ] 3.1.2 Data Entry - Counts:
  - [ ] Single digit input only
  - [ ] Cyclic auto-advance (row to column and back indefinitely)
  - [ ] Arrow navigation (up/down for columns, left/right for rows)
  - [ ] Backspace clears cell and moves back one cell
  - [ ] Delete clears current cell
- [ ] 3.1.3 Data Validation:
  - [ ] Auto-sea detection per row/col based on counts
  - [ ] Auto-sea marked in grid (visual indicator)
  - [ ] Auto-sea skips existing hints
  - [ ] Exits stage when all count cells filled

### 3.2 Setup Mode: Hint Entry
- [ ] 3.2.1 Activation (after counts filled or game loaded):
  - [ ] Enables: Hint cells (for toggle/clear), Count cells (can be changed), Save button
  - [ ] Disables: Playing-part cells, Play button
  - [ ] Continues: List, Delete
- [ ] 3.2.2 Hint Cell Operations:
  - [ ] Click to toggle hint types
  - [ ] Right-click to clear hint
- [ ] 3.2.3 Hint Input Types:
  - [ ] Mid (middle of ship)
  - [ ] Sea (water)
  - [ ] Up (top end of ship)
  - [ ] Down (bottom end of ship)
  - [ ] Left (left end of ship)
  - [ ] Right (right end of ship)
  - [ ] Single (complete 1-part ship)
- [ ] 3.2.4 Count Modification in Hint Entry:
  - [ ] Counts can be edited at any time during hint entry
  - [ ] Auto-sea recalculates when counts change
- [ ] 3.2.5 Play Button Validations (before entering Gameplay):
  - [ ] Test counts validity
  - [ ] Test auto-sea application
  - [ ] Test directed hints and directional consistency
  - [ ] Test solubility (puzzle can be solved)
  - [ ] FUTURE FEATURE: Verify ship counts achievable
  - [ ] Block Play if any validation fails (show warnings)
  - [ ] On validation failure: Mark adjacent hints, stay in setup mode
- [ ] 3.2.6 Auto-Sea Calculation on Play Button:
  - [ ] When Play button validates successfully, auto-deduced sea cells are determined and locked
  - [ ] These cells cannot be modified in gameplay

### 3.3 Gameplay Mode
- [ ] 3.3.1 Activation (after Play button passes validation):
  - [ ] Enables: Playing-part cells (toggle ship/sea/empty)
  - [ ] Disables: Count cells (LOCKED)
  - [ ] Disables: Hint cells (LOCKED)
  - [ ] Disables: Auto-sea cells (LOCKED)
  - [ ] Changes Save to Reset
  - [ ] Hides Saved games list
- [ ] 3.3.2 Playing-Part Input:
  - [ ] Click to toggle: ship part ↔ sea ↔ empty
  - [ ] Drag marks/unmarks sea (skipping hint and ship parts)
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
- [ ] 4.1 Grid rendering (12x12 with structured layout, same board for all modes)
- [ ] 4.2 Count cell management and validation
- [ ] 4.3 Hint placement and storage
- [ ] 4.4 Auto-sea calculation and marking
- [ ] 4.5 Auto-sea locking when Play button succeeds
- [ ] 4.6 Ship placement and adjacency checking
- [ ] 4.7 Clash detection and marking
- [ ] 4.8 Game state management (count entry, hint entry, gameplay)
- [ ] 4.9 Cell disable/lock management across modes
- [ ] 4.10 Save/Load functionality
- [ ] 4.11 Game completion detection
- [ ] 4.12 Input handling (keyboard, mouse, drag)
