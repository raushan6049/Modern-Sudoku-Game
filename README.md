# Modern-Sudoku-Game
A sleek, interactive chess game built with modern technologies. Featuring smooth animations, real-time move validation, and a clean UI that reimagines the classic game of chess for today’s players.

Here is a step-by-step summary of how this game was built:

Step 1: Building the Skeleton with HTML
The first step was to lay out the entire structure of the game using HTML. This defines all the visible elements and gives them unique ids or classes so they can be styled and controlled later.

Main Layout: A <div class="page-wrapper"> is used to center the main game content on the page. A separate <div class="background-container"> is created to hold the animated background elements that change with the themes.
Game Container: The core of the game resides within <div class="game-container">. This acts as a card that holds all the interactive parts.
Information Display: Inside the container, elements are added for the title (<h1>), game info (<div class="game-info">) which includes the mistakes counter, difficulty display, and timer.
Controls: Buttons for difficulty (.difficulty-controls), main actions (.controls like Hint, Check, New Game), and theme selection (.theme-controls) are laid out.
Interactive Areas: Empty divs are created for the Sudoku board (<div id="sudoku-board">) and the number palette (<div id="number-palette">). These are empty because JavaScript will generate their content dynamically.
Overlays & Feedback: A hidden <div id="game-over-overlay"> is added to be shown when the game ends. A <div id="message-area"> is included to display messages to the player.
Audio: <audio> tags are added for sound effects and background music, each with an id to be controlled by the script.
Step 2: Adding Style and Personality with CSS
With the structure in place, the next step was to bring the game to life visually using CSS. A key strategy here is the heavy use of CSS variables, which makes theming incredibly efficient.

CSS Variables for Theming: The :root or body selector defines a default set of variables for colors, backgrounds, and fonts (e.g., --bg-gradient-start, --cell-border-color).
Theme Definitions: Each theme (e.g., body.theme-forest, body.theme-matrix) is just a small block of CSS that overrides these default variables with its own set of colors. This is how the entire look and feel can change so dramatically with a single class change on the <body> tag.
Board Layout: The 9x9 grid is created using display: grid. The thicker borders between the 3x3 sub-grids are cleverly applied using :nth-child selectors on the cells.
Cell States: Different classes are styled to give the player visual feedback:
.pre-filled: For the initial puzzle numbers.
.user-filled: For numbers the player enters.
.selected: To highlight the active cell with a pulse animation.
.incorrect: To show a mistake with a red background and a shake animation.
Animations: @keyframes are defined for various effects like pulse, shake, pop-in (for new numbers), and the animated backgrounds (float, matrix-rain). These animations are then attached to the relevant CSS classes.
Responsive Design: The board's size is set using vmin units (width: 90vmin), which allows it to scale gracefully based on the smaller of the screen's width or height, ensuring it looks good on both desktop and mobile devices.
Step 3: Implementing the Brains with JavaScript
The final and most complex step was to write the JavaScript code that handles all the game's logic and interactivity.

Initialization (initializeGame): This is the master function that starts or restarts the game. It:

Selects a random puzzle from the puzzles object based on the chosen difficulty.
Sets up the boardState (the current grid) and solutionState arrays.
Resets all game state variables like wrongAttempts, hintCount, and isGameOver.
Calls renderBoard() and renderPalette() to build the UI.
Starts the timer.
Dynamic Rendering (renderBoard, renderPalette):

renderBoard loops 81 times, creating a <div> for each cell, setting its initial value (if any), and attaching a click event listener to empty cells.
renderPalette creates the number buttons (1-9 and 'X') and attaches listeners to them.
Player Input and Validation (handleCellClick, handlePaletteClick, placeNumber):

The handle...Click functions manage which cell and number are currently selected.
When a number is to be placed, placeNumber is called. This is a critical function that:
Checks for conflicts (row, column, 3x3 box) using the findConflictIndices helper function.
If there's a conflict, it increments wrongAttempts, shows an error message, and checks if the game is over.
If the move is valid, it updates the boardState array and the cell's display.
It then checks if the placed number is correct against the solutionState. If it is, the cell is "locked" by changing its style and removing its click listener.
Finally, it deselects the number from the palette.
Game State Management:

Mistakes & Game Over: The wrongAttempts variable is tracked. The handleGameOver function is called when this count reaches 5 or when the timer runs out. It shows the "Game Finished" overlay and disables game controls.
Persistence: The chosen theme is saved to localStorage, so the player's preference is remembered the next time they visit
