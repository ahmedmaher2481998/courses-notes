# Vim/Nvim Insert Mode

Three ways to enter the insert mode:

- `i` for inserting before the current char
- `a` for appending after the current focused char
- `o` for creating a new line then inserting into it
- `Shift + i` enter insert mode and insert at the start of the line
- `Shift + a` enter the insert mode and append at the end of the line
- `Shift + o` enter insert mode and create a new line above

# Quit Nvim

- `:wq` write and quit
- `:q` quit if there's no changes
- `:q!` quit and ignore the changes
- `:set number` activate line numbers
- `j` down, `k` up, `h` left, `l` right
- `set relativenumber` activate relative number in vim
- `set mouse=a` activate mouse in nvim
- `set tabstop=4`
- `set shiftwidth=4`
- `:colorscheme` + `tab`

This is setting in vim, you need a config file `vimrc` or `nvimrc` which will be loaded on every vim/nvim launch.

# Undo and Redo

- `u` undo changes, can be combined with numbers
- `Ctrl + r` redo changes, can be combined with numbers
- `v` enters the visual mode
- In visual mode `d` deletes the selected word
- In visual mode `y` yanks or copies something
- `p` paste after selection/below
- `P` paste above/before selection
- `dd` deletes the whole line
- `cc` delete and enter insert mode, change line
- `d + shift` deletes the rest of the line
- `c + shift` changes the rest of the line
- `w` for next word, `W` for next space-separated word
- `b` for previous word, `B` for previous space-separated word
- `d+w` delete next word
- `d+b` delete previous word
- `d2w` deletes 2 words next
- `d2b` deletes 2 words previous
- `diw` deletes in a word
- `ciw` change in a word
- `di(` delete in `()`
- `di{` delete in `{}`
- `e` jumps to the end of the word
- `0` goes to the start of the line
- `$` goes to the end of the line
- `d0` delete to the start of the line
- `d$` delete to the end of the line
- `de` delete to the end of the word
- `yiw` yank inner word
- `t*` traverse to before next occurrence of `*`
- `f*` find next occurrence of `*`
- `%` jump to the closing of bracket `{` or `(`
- `d%` delete everything including `{}`
- `gg` start of the file
- `Shift + g` to the end of the file
- `123G` goes to line 123
- `:123` goes to line 123

All of the above is the fundamentals.

# Indentation

- `[[` indent to the right
- `]]` indent to the left
- `Ctrl + v` to visual block mode, select column wise
- `gg + = + G` for auto indent a file

# Searching

- `:/hello` search for the next occurrence of `hello`, then press `n` for next, `N` for previous
- `:?hello` search for the previous occurrence of `hello`, then press `n` for previous, `N` for next
- Select token, press `#` to select the previous occurrence, `*` for the next occurrence
- `ma` for marking positions with `a`, then press `'a` to return to the mark
- `zz` center the current line in the middle of the screen

# Searching and Replacing and Repeating Commands

- `:%s/first/last/g` this will search for `first` and replace it with `last` throughout the file
- `.` repeat the last used command
- `:reg` view last stored things copied or cut
- Deleting cuts the deleted thing
- `"7p` paste the register number 7
- Paste the last thing you yanked `"0p`

# Macros

- `qa` record macro `a`
- `q` quit recording
- `@a` execute macro `a`
