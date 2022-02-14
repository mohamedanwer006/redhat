# vim

## vim 3 modes:

1. command mode
2. insert mode
3. execute mode

Default mode is command mode

- to switch to insert mode, use `i`

- to switch back tp command mode , use `esc `

- to switch to execute mode, use `:`

on execute mode, you can use `:q` to quit execute mode `:w` to write `:wq` to write and quit
`:q!` to quit without saving

to search use `/` on command mode`/<searchText>`

use `n` to got to next result

use `N` to got to previous result

### on command mode

use `o` to insert line below

use `O` to insert line above

use `<n>yy` to copy line yank

use `d` to delete line

use `dw` to delete word

use `dl` to delete letter

use `p` to paste line

use `dd` to cut line

use `u` to undo

use `.` to repeat last command

use `gg` to go to first line

use `G` to go to last line


### ***on execute mode***

use `:q` to quit execute mode

use `:w` to write

use `:wq` to write and quit

use `:q!` to quit without saving

use `:.,$ d` to delete from cursor to end of file

use `:<lineNumber>` to go to line number

use `:set number` to show line number

use `:set nonumber` to hide line number

use `:!<command>` to run command on terminal

use `:.!<command>` to run command put output in current cursor position

use `:r <fileName>` to read file

use `:w <fileName>` to write file


