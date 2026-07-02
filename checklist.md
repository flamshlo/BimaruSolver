# Bimaru Solver Version Checklist

## 1. Bimaru Rules and Definitions
- [ ] 1.1 Counts: Row and column ship part totals
- [ ] 1.2 Hints: Pre-filled ship and sea segments
- [ ] 1.3 Parts: Definite, tentative, solved (ship/sea)
- [ ] 1.4 Adjacency: Ship parts not adjacent in any direction
- [ ] 1.5 Ships: 1 carrier(4), 2 battleship(3), 3 destroyer(2), 4 torpedo(1/circle)

## 2. UI Layout
- [ ] 2.1 Board Grid (12x12): 10x10 play, Col 12 counts, Row 12 counts
- [ ] 2.2 Visuals: Crimson/emerald/turquoise glass parts, deep brown wood board
- [ ] 2.3 Sidebar: Logo, [i], New Game (always enabled)
- [ ] 2.4 Setup UI: Name, Save, [Valid LED], Play, saved list (delete X)
- [ ] 2.5 Gameplay UI: Name, [i], Reset
- [ ] 2.6 Status: Text area

## 3. Modes

### 3.1 Setup Mode: Count Entry
- [ ] 3.1.1 Entry: New Game; Enabled: Counts, List, Delete; Disabled: Grid, Play, Save
- [ ] 3.1.2 Navigation: Digit entry auto-advance; backspace resets/moves back
- [ ] 3.1.3 Auto-sea: Detected per row/col; exits stage when all filled

### 3.2 Setup Mode: Hint Entry
- [ ] 3.2.1 Entry: Counts filled/loaded; Enabled: Grid, Counts, Save; Disabled: Play
- [ ] 3.2.2 Inputs: T/M/S/U/D/L/R shortcuts; Right click clear
- [ ] 3.2.3 Play Validation: Tests counts, sea, hints, solubility; blocks Play if invalid

### 3.3 Gameplay Mode
- [ ] 3.3.1 Entry: Passed Validation; Enabled: Grid (part toggle)
- [ ] 3.3.2 Mouse: Drag marks/unmarks sea; click toggles ship/sea
- [ ] 3.3.3 Logic: Double-click solved (round corners); check limits; mark red clashes
- [ ] 3.3.4 Completion: Flashing green glow (3x)

## 4. Global Visuals
- [ ] 4.1 Animation: Throbbing arrow at input location
- [ ] 4.2 Part Definitions: Definite (Dark Green/polka dot), Tentative (Red ?), Solved (rounded corners)
- [ ] 4.3 Sea Definitions: Definite Sea (Navy blue/red X), Detected Sea (Dark light-blue/small X)
- [ ] 4.4 Hint Parts: Torpedo(circle), Mid(square), End(U/D/L/R), Sea Hint(wavy lines)

---

**Error Remark:** 4.3(A-D)
