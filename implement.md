# Keno Game Implementation Plan

## Overview
This document outlines a comprehensive implementation plan for the Keno game application. The implementation will be structured to allow for efficient LLM development while maintaining the accuracy of the prize table and all game mechanics.

## Core Game Components

### 1. Game State Management
- **State Structure**: Maintain game state with:
  - selectedNumbers: Array of user-selected numbers (2-10)
  - drawnNumbers: Array of drawn numbers (20 total)
  - gameStarted: Boolean flag for game state
  - totalNumbers: 80 (fixed)
  - numbersToDraw: 20 (fixed)
  - gamesPlayed: Counter for games played
  - totalWinnings: Accumulated winnings
  - credits: Player's current credits (starts at 20)

### 2. Prize Table Implementation
The prize table is a 2D array where:
- Rows represent selected numbers (2-10)
- Columns represent matched numbers (0-10)
- Values represent winnings (0 if no prize)

**Important**: The prize table must be accurate and match the specification:
```
const prizeTable = [
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 10, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 2, 25, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 1, 5, 50, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 2, 15, 300, 0, 0, 0, 0, 0],
    [0, 0, 0, 1, 5, 50, 1000, 0, 0, 0, 0],
    [0, 0, 0, 1, 3, 15, 100, 2500, 0, 0, 0],
    [0, 0, 0, 0, 2, 10, 50, 500, 10000, 0, 0],
    [0, 0, 0, 0, 0, 5, 20, 100, 2500, 25000, 0],
    [0, 0, 0, 0, 0, 2, 10, 50, 400, 4000, 100000]
];
```

### 3. UI Components

#### 3.1 Number Grid
- 80 number cells arranged in 10x8 grid
- Each cell displays a number from 1-80
- Cell styling:
  - Default: Gradient background with rounded shape according to theme
  - Selected: Alternate medium color gradient with pulsing animation according to theme
  - Drawn: Very bright gradient according to theme
  - Matched: Alternate brighter and highlighted color with stronger and faster pulsing animation

#### 3.2 Game Controls
- Start Game button: Initiates game drawing (Disabled durring game play)
- Reset Board button: Clears selections and resets game state (Disabled durring game play)
- Random Pick button: Adds one random number to selection (Disabled durring game play)
- Theme selector buttons (Space, Ocean, Desert, Forest)

#### 3.3 Game Information
- Credits display
- Games played counter
- Total winnings display
- Status message area
- Instructions and payout table at bottom

### 4. Game Logic

#### 4.1 Number Selection
- Users can select 2-10 numbers
- Selection toggles on click or touch
- Maximum of 10 numbers allowed
- Visual feedback for selected numbers

#### 4.2 Game Flow
1. User selects 2-10 numbers
2. Clicks Start Game
3. Deducts 1 credit
4. Draws 20 numbers sequentially from the 80 numbers with 1-second delay
5. Updates UI to show drawn numbers
6. Highlights in bright colors when drawn number matches user selected number
6. Calculates winnings based on matches
7. Updates credits and statistics
8. Informs user of number of matching numbers and winnings and waits
9. Resets information and drawn numbers on the board when Start Game is clicked
10. Resets information, drawn numbers, and user selected numbers when Reset Board is cicked

#### 4.3 Drawing Numbers
- Sequential drawing with 1-second intervals
- Random number generation without repetition
- Visual highlighting of drawn numbers

#### 4.4 Winnings Calculation
- Find intersection between selected and drawn numbers
- Use prize table to determine winnings
- Update game state with winnings

### 5. Theme System
- Four themes: Space, Ocean, Desert, Forest
- Each theme changes:
  - Background gradient
  - Browser background (Very dark gradient colors)
  - Number cell colors
  - Button styles
- Space is set as the default theme upon opening

### 6. Error Handling
- Validate number selection (2-10 numbers)
- Check for sufficient credits
- Handle invalid number selections
- Provide appropriate error messages

### 7. Technical Requirements

#### 7.1 HTML Structure
- Semantic HTML with proper element hierarchy
- Grid layout for number cells
- Responsive design for different screen sizes

#### 7.2 CSS Styling
- Responsive grid layout (10 columns on desktop, 8 on mobile if needed)
- CSS animations for number highlighting
- Gradient backgrounds for visual appeal
- Theme-specific styles
- Mobile-friendly touch targets

#### 7.3 JavaScript Implementation
- Modular functions for game state management
- Event listeners for user interactions
- Asynchronous drawing with timeouts
- Proper state updates
- Error handling and validation

### 8. File Structure
Built in a single HTML file (keno.html). The game will be a complete, self-contained implementation with HTML, CSS, and JavaScript.

### 9. Key Implementation Details

#### 9.1 Prize Table Accuracy
The prize table must be implemented exactly as specified in the original HTML:
- 11 rows (0-10 for matched numbers, with 0s in first two rows)
- 11 columns (0-10 for selected numbers, with 0s in first two columns)
- Values match the provided table exactly

#### 9.2 Game Flow Accuracy
- Exactly 80 numbers (1-80)
- Exactly 20 numbers drawn
- Sequential drawing with 1-second intervals
- Proper credit deduction (1 credit per game)
- Correct prize calculation based on selected vs matched numbers

#### 9.3 Visual Feedback
- Clear visual distinction between selected, drawn, and matched numbers
- Animations for number highlighting
- Responsive design for mobile and desktop
- Theme-specific styling

### 10. Testing Requirements
- Verify prize table accuracy
- Test game flow with various number selections
- Validate credit management
- Ensure proper drawing sequence
- Test all theme changes
- Verify mobile responsiveness