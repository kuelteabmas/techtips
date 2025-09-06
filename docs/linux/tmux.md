# TMUX

*Thursday, May 15th, 2025* by **devP**+

**Default Prefix**: `Ctrl+b`

## Switch Windows

Prefix, p
Prefix, w

## How to join two tmux windows into one horizontal pane

Switch to window 2.
Mark the desired pane with Prefix.
Switch to window 1.
Call join-pane: Prefix, `:join-pane`

or 

Suppose the two windows are number 1 and 2. Use

`join-pane -s 2 -t 1 `

This will move the 2nd window as a pane to the 1st window. The opposite command is break-pane