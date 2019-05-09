# TextGridRendererJs
Simple text grid renderer in js to constantly update a grid of characters, and their colors / background colors (if changed). Can be used for all kinds of applications, mostly some kind of fun visualization playground. Though, it could also be used as the core for something more complex, like a text based game or a terminal style program.

Initially just wanted to try some stuff with JavaScript string templates, with the idea of a text based game in mind - that turned out to be horribly inefficient (not the string templates themselves, but the way I was using them in this context). I decided to optimize it and make it work because it's a fun concept to play around with.

## Examples
Randomizer (warning: moderately high CPU load): https://gfycat.com/jitterycheerycentipede ~ https://matsyir.github.io/TextGridRendererJs/randomizer/  
This one's kind of a stress test. It looks pretty cool.

Core renderer initialized: https://matsyir.github.io/TextGridRendererJs/  
Nothing special with this one, it's just the blank canvas of the core renderer without any implementation logic.

## Usage
- The core renderer is in the root of the repo, under `textGridRenderer.js`, loaded by `index.html`, logic implemented in `main.js`. For example of a separate implementation, see the randomizer example: you do not need to edit `textGridRenderer.js`, only change the implementation logic in the update function in `main.js`.
- The game is created and started by calling `TextGridRenderer.init()` after the document is done loading (since it appends to the body). The constructor prepares it, but does not actually create it.
- The size of the grid can be changed by changing the `TextGridRenderer.ROWS` and `TextGridRenderer.COLS` static constants in the core renderer.
- Write your update logic in the function called to the renderer's constructor.
- Ideally, `TextGridRenderer.update()` should not take longer to execute than `TextGridRenderer.UPDATE_DELAY` (in ms).
- Do not set any of the main game properties unless you understand what exactly you're doing. For example, use `game.setPoint(r, c, char, charColor, bgColor)` instead of `game.points[r][c] = new TextGridPoint(char, charColor, bgColor)`.

## How it works
`TextGridRenderer.init()` generates a `<div>` filled with `<span>`s with HTML id's to represent a 2D array of TextGridPoints, which hold a character, its color and its background color. Those properties can be fetched from the 2D array without processing the html elements. The HTML id's format is: `r{rowIndex}c{colIndex}`.  
It currently uses jQuery for ease of implementation, but everything could definitely be done without jQuery.
