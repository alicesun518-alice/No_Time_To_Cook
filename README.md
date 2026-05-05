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



