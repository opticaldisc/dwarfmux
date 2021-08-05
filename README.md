
# Dwarfmux

Dwarfmux is a terminal wrapper for Dwarf Fortress and DFHack that uses Python and Tmux to allow you to use DFHack's keybindings in the game's ncurses terminal mode.

I made this plugin because I was unsatisfied with all the shortcomings of `PRINT_MODE:TEXT` support in DFHack. (and Dwarf Fortress in general...) 
Without this utility, DFHack users who want to play in a real terminal have to just name FN hotkeys after DFHack commands to access any of DFHack's special features. 
On top of that, I was also frustrated with the lack of simple ways to use HJKL keys for movement, like in many traditional roguelike games.

No one wants to rearrange their whole interface.txt for this.

No one wants to be limited to never using custom keybindings.

There has to be a better way.

Dwarfmux is my attempt to fix both of these problems at once, by dynamically generating a Tmux configuration based on the contents of `dfhack.init`. 
There are limitations to what Tmux can do in terms of actual keyboard input, but I've worked around that by adding extra "key tables" to Tmux.

## Features

- Automatically copies every keybinding available in your `dfhack.init` file.
    * And respects keybindings that specify their focused view!
- Includes an HJKL movement mode that works across gamemodes.
    * Shift+key for fast movement in Fortress mode!
    * Alt+key for careful movement in Adventure mode!
- Fixes Shift+arrowkey inputs in the terminal outside of HJKL mode. 
    * `PRINT_MODE:TEXT` normally breaks fast cursor movement altogether...

## Controls

This help screen can be brought up in-game by pressing Alt + Shift + ? in normal mode.
```
  Modifiers:
 ╔═════════════════════╗
 ║ [ M- ]:  Alt (Meta) ║
 ║ [ C- ]:  Control    ║
 ║ [ S- ]:  Shift      ║
 ╚═════════════════════╝
  Built-in keybindings:
 ╔══════════════════════════════════════════════════╗
 ║ [ M-Escape ]:    Exit any current mode.          ║
 ║ [ ` ]:           Toggle HJKL movement mode.      ║
 ║ [ M-` ]:         Enter DFHack mode.              ║
 ║ [ M-` twice ]:   Enter DFHack + Shift mode.      ║
 ║ [ M-` thrice ]:  Open the DFHack command prompt. ║
 ║ [ M-S-? ]:       Display this help message.      ║
 ╚══════════════════════════════════════════════════╝
  HJKL Mode Movement + Menu Controls:
 ╔══════════════════════════╗
 ║ [ M-(direction) ]: y k u ║╔══════════════════════╗
 ║ Careful movement.   \|/  ║║ [ - ]:  Insert - key ║
 ║ [ C-(direction) ]: h-X-l ║║ [ = ]:  Insert + key ║
 ║ Pass input to       /|\  ║║ [ _ ]:  Insert / key ║
 ║ Dwarf Fortress.    b j n ║║ [ + ]:  Insert * key ║
 ╚══════════════════════════╝╚══════════════════════╝
```
Any inputs blocked by movement keys in HJKL mode can be reached by holding Ctrl.
For example, the units screen in Fortress mode would normally be accessed by pressing U, so in HJKL mode you would press Ctrl+U.

## Options

At the moment there are only two extra options, which can be enabled via a special comment line in your `dfhack.init`.

- `hjkl-in-dfhack-mode`: Apply HJKL movement bindings to the DFHACK layer instead of HJKL_MODE.
    * This can allow for some truly awesome setups with HJKL movement and custom DFHack command bindings on the same layer.
- `tmux-bindings`: Allow the usage of Tmux's prefix key and default bindings within Dwarfmux.
    * This allows you to open more terminal windows, potentially useful for running other utilities or scripts alongside the game in the same Tmux session.

NOTE: The default Tmux prefix, Ctrl+B, overrides the commonly used `bodyswap` keybinding. This isn't _super_ important though, since the default example `dfhack.init` doesn't even use the correct command for it, so you would need to edit the file to use it anyway.

You can add these options by prepending a comment line with `#@dwarfmux`. For example, someone using both options would do this:
```
#@dwarfmux tmux-bindings hjkl-in-dfhack-mode
```

## Limitations

- Key combinations involving both Ctrl and Shift together will not work on most terminals.
    * Worked around by assigning Ctrl+Shift keybindings to `DFHACK_SHIFT`
- Diagonal numpad buttons do not seem to work with Shift or Ctrl. (but adventure mode's careful movement works fine with Alt)
- Ctrl+M is generally interpreted by terminals as the same as the Enter key, so it can't be used at all. 

## Installation

Just put `dwarfmux` in your Dwarf Fortress folder and run it.
The whole thing is just a single file.

Users who keep their dwarf fortress folder in `~/.dwarffortress` can also just drop dwarfmux in a bin directory somewhere, or just run it straight from the repo.

