
# Dwarfmux

Dwarfmux is a terminal wrapper for Dwarf Fortress and DFHack that uses Python and Tmux to allow you to use DFHack's keybindings with `PRINT_MODE:TEXT`.

I made this plugin because I was unsatisfied with all the shortcomings of `PRINT_MODE:TEXT` support in DFHack.
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
- Includes an HJKL movement mode that automatically detects which gamemode you're in.
  * Shift+key for fast movement in Fortress mode!)
  * Alt+key for careful movement in Adventure mode!
- Fixes Shift+arrowkey inputs in the terminal. 
  * `PRINT_MODE:TEXT` normally breaks fast cursor movement altogether

## Limitations

- Key combinations involving both Ctrl and Shift together will not work on most terminals.
  - Worked around by assigning Ctrl+Shift keybindings to `DFHACK_SHIFT`
- Diagonal D-pad buttons do not seem to work with Shift or Ctrl
- Ctrl+M is generally interpreted by terminals as the same as the Enter key. 

## Installation

Just put `dwarfmux` in your Dwarf Fortress folder, or in some bin directory somewhere.
The whole thing is just a single file.
