# No_Time_To_Cook

## Behavior Description

This project is a single player Overcooked-style cooking game implemented in VHDL on the Digilent Nexys A7-100T FPGA board. The game is displayed on a display or monitor using VGA output through a VGA-to-HDMI adapter.

The player can control a chef character in a kitchen layout. The goal is to pick up ingredients, prepare food, and complete the order cards before the timer runs out. The kitchen contains ingredient stations, drinks, a cut board and fryer station, a serving counter, plates, and a trash can.

The player can move the chef near an item or station using 4 directional buttons and press the center button to interact. Depending on the chef’s location and held item, the player can pick up items, combine ingredients, serve food, or discard an item.

The game includes an intro screen where the player selects between two chef characters. During gameplay, only the selected chef appears on the screen.

The game has four main states:
```INTRO_SELECT → GAME_PLAYING → GAME_WIN / GAME_OVER```

In INTRO_SELECT, the player can choose a character toggling Switch 0 and Switch 1 on the board and start the game by turning on Switch 2. In GAME_PLAYING, the timer runs and the player completes orders. If all orders are completed before the timer runs out, the game enters GAME_WIN. If the timer reaches zero before all orders are completed, the game enters GAME_OVER.

This project uses finite state machine logic for the states of game flow and Boolean logic for collision and interaction detection. For example, signals such as near_buns, near_cheese, near_fryer, near_counter, and near_trash determine whether the chef is close enough to interact with a station.

**Controls:**
| Input        | Function           | 
| -------------|-------------|
| BTNU | Move character up |
| BTND | Move character down      |   
| BTNL | Move character left      |  
| BTNR | Move character right    |  
| BTNC | Pick up item, combine item, serve food, or discard item   |  
| SW0  | Select Chef M on the right      |  
| SW1  | Select Chef F on the left      |  
| SW2  | Start game when ON / return to intro when OFF (depends on game state)      |  

## Required Hardware and Software
- Digilent Nexys A7-100T FPGA Board
- Micro USB Cable
- VGA to HDMI Adapter
- HDMI Cable
- Any display screen or monitor with HDMI input
- Vivado


We built our game using the Pong starter code. From Pong, we kept the VGA structure, the binary score display on the FPGA board, and the coordinate-based contact logic. In Pong, that logic checks contact between the ball and paddle. In our game, we changed that idea into proximity detection between the chef and different kitchen stations.

The game uses pixel_row and pixel_col to draw everything on the screen. Each object, like the chef, food items, stations, and order cards, has its own display logic. If the current pixel is inside that object, the module outputs a color and sets visible high.

The game has four states: intro select, gameplay, game over, and game win. In the intro state, the player selects between two chef sprites using switches. During gameplay, the player moves the chef with the board buttons and uses BTN0 to interact.

The chef has a held item state, such as none, plate, buns, cheese, patty, burger, potato, fries, cola, or sprite. When the chef is near a station and presses the action button, the held item changes. Ingredients can combine, like buns plus patty plus cheese becoming a burger, and potato becomes fries at the fryer.

The order system uses item codes. Burger, fries, Sprite, and cola each have a 3-bit code. The current order has item A and item B. When the player serves the correct item at the counter, the game marks that item as done. Once all required items for that order are complete, the score increments and the game moves to the next order.

For shuffling, a 3-bit counter runs continuously in the top-level module. When SW2 starts the game, the current counter value is captured as shuffle_sel. That value selects one of eight predefined order sequences, so the orders appear different each game.

The game also has a 3-minute countdown timer. If the player completes all eight orders before time runs out, the game shows the win message. If the timer reaches zero first, it shows the timeout message.
