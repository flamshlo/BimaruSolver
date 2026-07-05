# Specs.md - Version 1.2

## Bimaru Solver - Complete Specifications

**Bimaru Solver** is a puzzle-solving application for the Bimaru puzzle game. It allows users to enter a puzzle (ship counts and hints) during a setup phase, then solve it by placing ship parts and se[...] 

---

## What is Bimaru?

Bimaru is a logic puzzle similar to Battleship. Players must locate hidden ships on a grid using:
- **Row/Column counts**: How many ship parts are in each row/column
- **Hints**: Pre-filled cells showing ship parts or sea
- **Adjacency rule**: Ship parts cannot be adjacent (orthogonally or diagonally)

**Fleet to find:**
- 1 Aircraft-Carrier (4 parts)
- 2 Battleships (3 parts each)
- 3 Destroyers (2 parts each)
- 4 Torpedoes (1 part each)

---

## User Workflow

### Phase 1: Count Entry (Setup)
1. User clicks "New Game"
2. Names the puzzle (auto-generated: yyyy.mm.dd - index)
3. Enters ship part counts for each row (left side) and column (top)
4. Single-digit input, cyclic auto-advance, arrow navigation
5. Application auto-deduces "sea" cells (empty cells in filled rows/columns)
6. When all counts entered, move to Hint Entry phase

### Phase 2: Hint Entry (Setup)
1. User places hints on the 10x10 grid:
   - **Mid**: Middle part of a ship
   - **Sea**: Water cell
   - **Up/Down/Left/Right**: End parts (directional hints)
   - **Single**: Complete 1-part ship
   - Right-click clears hints
2. User can edit counts if needed; auto-sea recalculates
3. User clicks "Play Game" button
4. Validations run (solubility check, hint consistency, etc.)
5. If valid: auto-sea cells are locked, move to Gameplay
6. If invalid: show warnings, stay in setup

### Phase 3: Gameplay
1. User places ship parts and sea cells by clicking grid cells
2. Hints and counts are locked and visible (read-only)
3. Auto-deduced sea cells are locked and visible
4. User can only toggle the remaining empty cells
5. Gameplay ends when:
   - All ship parts placed correctly
   - All row/column counts matched
   - All cells filled
   - Display "YOU DID IT!" with 3x green glow flash
6. User can click "Reset" to go back to hint entry or start over

---

## Checklist (Instructions Area)

This checklist provides quick, step-by-step instructions for users and a concise set of items for implementation verification.

- Count Setup (see Instructions below)
- Hint Setup (see Instructions below)
- Gameplay (see Instructions below)

<p style="color:red; font-weight:bold; font-size:1.1em">ERRORS: If validation or gameplay errors occur, show clear error indicators and prevent progression until resolved. (Specific error messages: To be determined)</p>

---

## Board Structure

### 12x12 Grid (same grid for all modes, different cells enabled per mode)

| Row | Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 | Col 7 | Col 8 | Col 9 | Col 10 | Col 11 | Col 12 |
|-----|-------|-------|-------|-------|-------|-------|-------|-------|-------|--------|--------|--------|
| 1 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 2 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 3 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 4 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 5 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 6 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 7 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 8 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 9 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 10 | Game | Game | Game | Game | Game | Game | Game | Game | Game | Game | Padding | Count |
| 11 | Padding | Padding | Padding | Padding | Padding | Padding | Padding | Padding | Padding | Padding | Padding | Padding |
| 12 | Count | Count | Count | Count | Count | Count | Count | Count | Count | Count | Padding | Empty |

**Legend:**
- **Game**: 10x10 game grid (rows 1-10, columns 1-10)
- **Count**: Count cells for rows (column 12, rows 1-10) or columns (row 12, columns 1-10)
- **Padding**: Empty spacing (row 11, all columns; column 11, all rows)
- **Empty**: Corner cell [12,12]

---

## Cell Types & Mode Behavior

### Count Entry Mode
- **Count Cells**: ENABLED (input allowed)
- **Game Grid**: DISABLED (locked, read-only)
- **Hints**: Locked
- **Auto-Sea**: Calculated and shown
- **User can change**: Counts only

### Hint Entry Mode
- **Count Cells**: ENABLED (input allowed, counts can be changed)
- **Game Grid**: ENABLED (hints can be placed/cleared)
- **Hints**: Editable
- **Auto-Sea**: Shown, locked
- **User can change**: Counts and hints

### Gameplay Mode
- **Count Cells**: DISABLED (locked, read-only)
- **Game Grid**: ENABLED (playing-parts can be toggled)
- **Hints**: Locked (cannot be modified or deleted)
- **Auto-Sea**: Locked (cannot be modified or deleted)
- **User can change**: Empty cells only (toggle ship/sea/empty)

---

## Key Logic

### Auto-Sea Calculation
When entering counts, the system:
1. For each row: Fills empty cells with "sea" when row count is satisfied
2. For each column: Fills empty cells with "sea" when column count is satisfied
3. Marks these cells distinctly (different visual from player-placed sea)
4. Updates if counts are modified

### Auto-Sea Locking
When Play button is pressed and validation succeeds:
- Auto-sea cells are finalized and locked
- User cannot modify them during gameplay
- They remain visible for reference

### Validation on Play Button
Before entering Gameplay, verify:
1. Counts are valid (non-zero, reasonable)
2. Auto-sea application is correct
3. Hints are directionally consistent (e.g., "Up" hint has valid ship below, etc.)
4. Puzzle is solvable (solubility check)
5. FUTURE: Ship counts are achievable with given hints
6. If any validation fails: show warning, mark adjacent hints, stay in setup

<p style="color:red; font-weight:bold; font-size:1.1em">ERRORS (detailed instructions): Right-click to clear a cell. If validation or gameplay errors occur, display clear error indicators and messages. Specific error messages: To be determined.</p>

---

### Clash Detection
During gameplay, detect and mark:
- Ship parts adjacent to other ship parts (orthogonal or diagonal)
- Mark with orange/red highlighting
- Prevent game completion while clashes exist

### Completion Detection
Game ends when:
- All row count cells show "solved" (correct number)
- All column count cells show "solved" (correct number)
- All cells filled (no empty cells remain)
- No clashes detected
- Display completion message with visual feedback

---

## Save/Load System

### Save Functionality
- User clicks "Save" during setup or gameplay
- Game state saved with:
  - Game name
  - Puzzle counts
  - Hints
  - Current playing-parts (if in gameplay)
  - Mode (count entry, hint entry, or gameplay)
- Format: JSON or similar structured format
- Stored locally (browser storage or local file system)

### Load Functionality
- Saved games list displayed in sidebar (setup mode only)
- Click game name to load
- Resume from saved state (count entry, hint entry, or gameplay)
- Can delete games with red X button

### Game Naming
- Auto-generated format: `yyyy.mm.dd - nnn` (e.g., `2026.07.05 - 001`)
- `nnn` increments for multiple games on same day
- User can edit name during setup

---

## Input Methods

### Keyboard (Count Entry)
- **Digits 0-9**: Enter count
- **Arrow keys**: Navigate (up/down for columns, left/right for rows)
- **Tab**: Auto-advance to next count cell
- **Backspace**: Clear and move back
- **Delete**: Clear current cell

### Mouse (Hint Entry & Gameplay)
- **Left-click**: Toggle hint/playing-part/empty
- **Right-click**: Clear hint
- **Drag**: Mark/unmark sea (skipping hints and ship parts)
- **Double-click**: Mark as solved (gameplay only)

---

## Status & Error Handling

### Count Cell Status
- **Green (Solved)**: Correct number of parts placed
- **Yellow (Incomplete)**: Waiting for more parts
- **Red (Over)**: Too many parts - error state

### Validation Errors
- Show warning popup or banner
- Mark problematic cells (adjacent hints, clashes)
- Block transition to next phase
- Allow user to correct and retry

### User Feedback
- Status text updates on mode changes
- Input animation (throbbing arrow) at active cell
- Completion message: "YOU DID IT!" with visual feedback (green glow)

---

## UI Components

### Main Board
- 12x12 grid (responsive sizing)
- Count cells distinct styling
- Clear cell boundaries

### Sidebar
- **Header**: Logo, version, info button
- **Controls**: New Game, Game name (textbox/label), Save, Reset
- **Saved Games**: List with click to load, red X to delete

### Status Area
- Message display (mode, completion, errors)

---

## Implementation Notes

1. **Same Board for All Modes**: One 12x12 grid, different cells enabled/disabled per mode
2. **Data Persistence**: Save/load across sessions
3. **Responsive Design**: Grid and UI scale appropriately
4. **Accessibility**: Clear visual feedback, keyboard support
5. **Validation**: Comprehensive checks before gameplay
6. **Auto-Sea**: Intelligent calculation and locking mechanism

## Instructions (Detailed)

These instructions are also included in the Checklist area above for quick reference.

1. Counts setup:
   - Enter ship part counts (0-8). Entering a digit will move to the next cell. Right mouse button to clear a cell. Once all cells are full you will be able to enter hints, and start playing.

2. Hint setup:
   - Click on the game cells to enter hints. Repeatedly clicking toggles to the next hint shape. Right mouse button clears the cell. You may replace ship count numbers. When done press PLAY GAME.

3. Gameplay:
   - Click on the available game cells to toggle between definite possible and solved game parts. Right Mouse button to clear cell. You cannot change hints and auto-deduced Sea.


