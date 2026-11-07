# Keno Game Implementation Plan

## Overview
This document provides a comprehensive implementation plan for a Keno game that will be built in a single HTML file (keno.html). The game will be a complete, self-contained implementation with HTML, CSS, and JavaScript.

## Core Requirements

### Game Structure
- Single HTML file implementation (keno.html)
- Pure HTML/CSS/JavaScript (no external dependencies)
- Responsive design that works on mobile and desktop
- Modern UI with gradient backgrounds and animations

### Game Functionality
1. **Number Grid**
   - Display numbers from 1-80 in a grid layout of 10 columns and 8 lines
   - Interactive selection mechanism (2-10 numbers)
   - Visual feedback for selected numbers (orange gradient)

2. **Game Flow**
   - Player starts with 20 credits
   - Each play costs 1 Credit
   - Players Credit Display should be updated at the start and end of each game
   - Start Game button to initiate drawing
   - Reset Game button to start over
   - Sequential drawing of 20 winning numbers with 1-second delays
   - Fisher-Yates shuffle algorithm for random drawing

3. **Game Mechanics**
   - Selection persistence: User selected numbers are preserved between games
   - Board cleanup: Previously drawn numbers are cleared when starting a new game
   - Winning calculation based on matches with prize table
   - Game state management (buttons disabled during game)

4. **Visual Design**
   - Color scheme:
     * Selected numbers: Orange gradient
     * Drawn numbers: Yellow gradient
     * Matching numbers: Gold gradient that pulses quickly
     * Background: Dark Blue gradient
   - Animations:
     * Pulse animation for drawn numbers
     * Smooth transitions for all UI elements
   - Instructions for how to play and prize table displayed at the bottom

### Prize System
The prize system is implemented as a multidimensional array where prizes are determined based on the number of selected numbers and the number of matches. The structure is:

```javascript
const prizeTable = [
    // 0 selected numbers (shouldn't happen in normal gameplay)
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    
    // 1 selected number (shouldn't happen in normal gameplay)
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    
    // 2 selected numbers
    [0, 0, 10, 0, 0, 0, 0, 0, 0, 0, 0],
    
    // 3 selected numbers
    [0, 0, 2, 25, 0, 0, 0, 0, 0, 0, 0],
    
    // 4 selected numbers
    [0, 0, 1, 5, 50, 0, 0, 0, 0, 0, 0],
    
    // 5 selected numbers
    [0, 0, 0, 2, 15, 300, 0, 0, 0, 0, 0],
    
    // 6 selected numbers
    [0, 0, 0, 1, 5, 50, 1000, 0, 0, 0, 0],
    
    // 7 selected numbers
    [0, 0, 0, 1, 3, 15, 100, 2500, 0, 0, 0],
    
    // 8 selected numbers
    [0, 0, 0, 0, 2, 10, 50, 500, 10000, 0, 0],
    
    // 9 selected numbers
    [0, 0, 0, 0, 0, 5, 20, 100, 2500, 25000, 0],
    
    // 10 selected numbers
    [0, 0, 0, 0, 0, 2, 10, 50, 400, 4000, 100000]
];
```

This structure allows for different payouts based on the number of selections (2-10) and the number of matches. For example, if a player selects 5 numbers and matches 3, they would win the value in `prizeTable[5][3]` which would be 2.

### Game Statistics
- Track games played
- Track total winnings
- Display statistics in the UI

### User Experience
- Clear instructions for players
- Visual feedback for all interactions
- Error handling for invalid selections
- Responsive design for all device sizes
- Intuitive controls

## Implementation Details

### File Structure
```
keno.html - Main game file (complete implementation)
```

### Game State Management
The game maintains state through a gameState object:
- selectedNumbers: Array of currently selected numbers (1-10)
- drawnNumbers: Array of drawn winning numbers (20)
- gameStarted: Boolean indicating if game is in progress
- totalNumbers: Total numbers in the game (80)
- numbersToDraw: Numbers to draw (20)
- gamesPlayed: Counter for games played
- totalWinnings: Accumulated winnings

### Technical Requirements
1. **Number Selection**
   - Click to select/deselect numbers
   - Limit of 10 selections
   - Visual feedback for selection limits

2. **Drawing Process**
   - 20 random winning numbers from 1-80
   - Fisher-Yates shuffle algorithm
   - Sequential drawing with 1-second delays
   - Clear visual indication of drawn numbers

3. **Winning Calculation**
   - Compare selected numbers with drawn numbers
   - Calculate winnings based on prize table
   - Highlight matching numbers with gold color
   - Display winning message

4. **Game Controls**
   - Start Game: Initiates drawing process
   - Reset Game: Clears current game state
   - Button states: Disabled during game play
   - Visual feedback for button interactions

## Special Requirements

### Selection Persistence
- User selected numbers should be preserved between games
- Numbers should only be cleared when Reset Game button is pressed

### Board Management
- Previously drawn numbers should be cleared from the board when starting a new game
- This ensures clean slate for each new game round

### User Feedback
- Clear messages for game state and results
- Visual indicators for all game actions
- Error handling for invalid inputs

## Testing and Validation

### Functionality Testing
- Number selection/deselection
- Drawing algorithm correctness
- Winnings calculation accuracy
- Edge cases (no selections, max selections)
- Sequential drawing with delays
- Game state management
- Matching number highlighting

### Performance Testing
- Game loading time
- Selection feedback speed
- Drawing mechanism performance
- Mobile responsiveness
- Visual effects performance

## Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile responsive design
- Works on various screen sizes

## Future Considerations
- Sound effects
- Themes
- Statistics dashboard
