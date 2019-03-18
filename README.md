# LPHK (LaunchPad HotKey)
A Novation Launchpad macro scripting system.

## What does it do?
The goal of this project is to implement a macro scripting system for the Novation Launchpad, in order to use the launchpad as a scriptable, general purpose macro keyboard.

It uses "LPHKscript", a very simple scripting language similar to [DuckyScript](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript), and has a GUI to enter scripts, set colors, and to save/load your setup.

I have specifically chosen to do my best to develop this using as many cross platform libraries as possible, with a hard requirement that Linux and Windows be supported, and a strong preference for Mac as well. The GUI is driven by TK, which works on all of the above plus Unix. The interface with the launchpad and several script functions are built on pygame, which is compatable with basically everything ever. Pretty much everything else is standard Python 3.

## Why would you do that?
Because it could be immensely useful for a wide variety of tasks, such as:
* Gaming, to bind:
  * Items
  * Volume
  * Attacks
  * Typed commands
  * Automatic Glitch/Trick Execution (think ABH or propsurfing in Source)
  * Repetitive tasks (grinding)
  * Reference Website launcher
  * Window switcher
* Editing, to bind:
  * Cuts/insertions
  * Modes
  * Effects
  * Render
  * Preview
  * Scrubbing
* Programming, to bind:
  * Commenting code
  * Autotyping function/loop templates
  * Compiling/excuting
  * Breakpoints
  * Debugger
* ... and many more!



## What is LPHKscript?
LPHKscript is a simple macro scripting language tailor made for LPHK. Syntax is closer to a shell/batch script than, say, JavaScript.

### Scheduling
Only one script runs at a time, and there is a scheduling system for them. If a script is scheduled, it's button will pulse red. If the script is running, the button will flash red quickly. This is true for the 8x8 grid, however, the function keys cannot flash or pulse, as a hardware limitation. These keys will be bright orange for scheduled and bright red for running.

When you press a script button, if there is a script running, it adds the script to the queue. If no scripts are running, the script is added to the queue and the queue execution is started. Tapping a scheduled script's button will unschedule it, and tapping a running scripts button will kill it. If that sounds confusing, load up `user_layouts/examples/all_delays_all_day.LPHKlayout` and press a bunch of buttons.

## What still needs to be written? (in order of priority)
* Make a special color picker for Classic/Mini/S that only has the 16 possible colors (you can select colors with blue atm, it will have the blue component ignored.
* Refactor code to make LPHKscript functions in autoimplementing modules, for ease of delevopment
  * Make modules w/ funcs that can either validate or run
  * Issue # tbd
* Make `PRESS`, `RELEASE`, and `TAP` accept multiple keys
* Let `SOUND` use spaces in it's path if it has double quotes around it
* Rework sound module to use the `sounddevice` library
* Add a `Sound` menu with `Choose default output device...` option
* Add a third argument to `SOUND` for overriding the default sound device
* Add variables and mathematical evaluation (mostly done!)
* Add conditional jumps based on value comparisons (Would this make LPHKscript Turing complete? :D) 
* Add script status icons (bound, playing, queued)
* Let program function as a layout editor without LP connection
* Add syntax highlighting
* Add GUI scaling
* Support for Launchpad Pro
  * The lack of tactile feedback, inability to utilize the pressure sensitive inputs (launchpad.py limitation), and inconvenient function keys where the hand rests makes support for the LP Pro a lower priority.
* Add generalized macro recorder wizard
* Make `Add Command...` menu that acts as a guided helper for making commands
* Add mouse event capture prompts to `Add Command...` menu boxes
* Add keyboard event capture (incl. unknown keycodes) to `Add Commands...` menu boxes
* Add `CMD` command to run OS commands
  * Make multi-level scary warning dialog boxes when binding to a button (incl during load layout)
  * Give option (and strongly reccomend its use) for users to run command once and verify it does what they want before binding to button (incl during load layout)
* Add `@LOAD_LAYOUT` header command to load a specified layout
  * Check if layout currently exists when binding to a button (incl during load layout)
    * If not, prompt user if they want to continue anyway
* MIDI output command? (Low priority)
* Load layout header?

## What have you done so far?
* ~~Support for Launchpad MkII~~
* ~~Events system~~
* ~~Colors system~~
* ~~LPHKScript base iteration~~
* ~~Keyboard lib base~~
* ~~Proof of concept demo~~
* ~~Saving/Loading~~
* ~~Sound functionality~~
* ~~Basic GUI~~
* ~~Save/load single scripts in GUI~~
* ~~Script entry error checking~~
* ~~Add launchpad connection menu~~
* ~~Add `M_MOVE`, `M_TAP`, `M_SCROLL`, and `M_SET` commands~~
* ~~Add `M_PRESS`, `M_RELEASE`, and `M_TAP` commands~~
* ~~Put save/load script into menu~~
* ~~Add `M_LINE`, `M_LINE_SET`, and `M_LINE_MOVE` commands~~
* ~~Add a `WAIT_UNPRESSED` command that delays while the button the script is bound to is pressed~~
* ~~Add `@ASYNC` header command to run script independent of other scripts~~
* ~~Add launchpad connection status indicator/remove popups~~
* ~~Add commenting script lines~~
* ~~Make pressing a running/queued button cancel/terminate execution~~
* ~~Make queued/playing buttons blink instead of be solid~~ 
* ~~Make user defined colors RGB~~
* ~~Add RGB color selector~~
* ~~Add `LABEL` command~~
* ~~Add `IF_PRESSED_GOTO_LABEL` command to jump from this line to a `LABEL` if the key is still pressed~~
* ~~Add `GOTO_LABEL` command~~
* ~~Add `IF_UNPRESSED_GOTO_LABEL` command to jump from this line to a `LABEL` if the key is unpressed~~
* ~~Add `REPEAT_LABEL` command to jump from this line to a `LABEL` n number of times max~~
* ~~Add `IF_PRESSED_REPEAT_LABEL` command to jump from this line to a `LABEL` if the key is still pressed n number of times max~~
* ~~Add `IF_UNPRESSED_REPEAT_LABEL` command to jump from this line to a `LABEL` if the key is unpressed n number of times max~~
* ~~Add `M_STORE`, `M_RECALL`, and `M_RECALL_LINE` functions to remember where the mouse was before execution~~
* ~~Fix syntax checking being done in `main_logic()` instead of the, you know, syntax checker?~~
* ~~Merge `SP_` functions into smart versions of their single-character counterparts~~
* ~~Add feature to syntax checking for SOUND to check if file exists/is usable~~
* ~~Do syntax checks on loading a layout~~
* ~~Add `@SIMPLE` header for simple keybinding of single keyboard keys~~
* ~~Merge `M_TAP`, `M_PRESS`, and `M_RELEASE` commands into their keyboard counterparts~~
* ~~Add button move/swap/copy feature~~
* ~~Fix button highlighting clipping at screen edges~~
* ~~Add warning prompts to move/copy~~
* ~~Add "Do you want to save your layout?" popup on exit if layout is unsaved.~~
* ~~Add save layout if changed prompt to load/new layout~~
* ~~Do not prompt to save blank layout~~
* ~~Do not warn about moving/copying to the same button~~
* ~~Make script being edited highlighted~~
* ~~Fix wierd bug where GOTO and DELAY didn't obey a kill command (caught on video)~~
* ~~Add `OPEN` command to open folders and files~~
* ~~Add `RELEASE_ALL` command~~
* ~~Add `RESET_REPEATS` command to reset the counter on all repeats~~
* ~~Basic support for Launchpad Classic/S/Mini~~

