### Paste symbol to line
- Press Esc to enter 'command mode'
- Use Ctrl + V to enter visual block mode.
- Move Up / Down to select the columns of text in the lines you want to comment.
- Then hit Shift + i and type the text you want to insert.
- Then hit Esc , wait 1 second and the inserted text will appear on every line.

### Replace occurence
`:s/foo/bar/g`
Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'.

`:%s/foo/bar/g`
Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.

`:%s/foo/bar/gc`
Change each 'foo' to 'bar', but ask for confirmation first.

`:%s/\<foo\>/bar/gc`
Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation.

`:%s/foo/bar/gci`
Change each 'foo' (case insensitive due to the i flag) to 'bar'; ask for confirmation.

`:%s/foo\c/bar/gc` is the same because \c makes the search case insensitive.
This may be wanted after using :set noignorecase to make searches case sensitive (the default).

`:%s/foo/bar/gcI`
Change each 'foo' (case sensitive due to the I flag) to 'bar'; ask for confirmation.

`:%s/foo\C/bar/gc` is the same because \C makes the search case sensitive.
This may be wanted after using :set ignorecase to make searches case insensitive.

The pattern is:
`[range]s\old\new\[flag]s`
For range we could use:
- `$` - end of a file
- `%` - whole file (an example this is the same, as `1,$s/old/new/` that reads from first line to the end)
- `1` - first line, etc

Replacing in a line with special characters:
`:s#/var/spool#/usr/local#`


### Search in file
`:\search_pattern` + Enter (`n` for the next search result)


### Splitting vim
Ctrl+W, S (upper case) for horizontal splitting

Ctrl+W, v (lower case) for vertical splitting

Ctrl+W, Q to close one

Ctrl+W, Ctrl+W to switch between windows

Ctrl+W, J (xor K, H, L) to switch to adjacent window (intuitively up, down, left, right)

```
-o[N]                Open N windows (default: one for each file)
-O[N]                Like -o but split vertically
```

```vim
vim -o file1.txt file2.txt file3.txt
```


### Open folder search
```vim
:e .
```

### Rezise
```vim
:resize 80
:resize +15
:vertical resize -5
```

### Change case of characters
- Select character or word/line/range
- press `gU` to uppercase
- press `gu` to lowercase
- press `g~` to toggle characters


### Use register
#### Store to register
```vim
“<register-name><command>
"ayy
```
- " - for register edit
- a - is the register name
- yy - is the command for register (yank)

We could also append data to the register with capital name:
`"Ayaw` - will yank a word and append it to the register "a"

#### Paste from register
```vim
"<register-name>p
"ap
```

### Use diff
```vim
vimdiff file1 file2
nvim -d file1 file2
```

### Escape terminal/diff etc mode
```vim
Ctrl+\ Ctrl+n
```

### Editing file
- `i` - edit the current cursor position
- `I` - edit at the begining of the line
- `a` - edit at the character next to the cursor position
- `A` - edit at the end of a line
- `o` - edit at the next line
- `O` - edit at the previouse line

### Text Objects
`{operator}{a}{object}`
`{operator}{i}{object}`

Ex:
- `daw` - Delete A Word
- `ciw` - Change Inner Word
- `das` - Delete A Sentence
- `dap` - Delete a Paragraph
- `ci[` - Change everything inside `[]`
- `ci)` - Change everyting inside `()`
- `yi<` - Yank text inside `<>`
- `cit` - Change inside a tag
- `ci{` - Change everything inside `{}`
- `ci"` - Change everyting inside `""`
- `ciw""EscP` - Surrounf a word by quotes. Change inner word, paste quotes, paste a yanked word
- `"aciw""Esc"aP` - Surround a word by quotes but yank in register "a"

### Macros

Record macro:
`q{register}{commands}q`

Play Macro from register:
`@{register}`

Play last macro:
`@@`

Play macro for range:
`{range}normal @{register}`
`27,35normal @d`

Append commands to macro:
`@{capital register}`
`@Cj` - Will append command `j` to register "c"

Ex, insert word "First: " at the begining of the line:
`qa0iFIRST: Escjq`:
- `qa` - Start recording macro to the register "a"
- `0` - place cursor to the begining of the line
- `i` - change mode to Insert
- `FIRST: ` - type word "FIRST: "
- `Esc` - go to normal mode
- `j` - jump to the next line
- `q` - stop recroding macro

To store macros use ~/.viminfo or ~/.vimrc:
`let @{register} = 'content of the macro commands'`
`let @t = 'ITODO: '`

### Execute bash command
```vim
date "+%m-%d-%Y" # Write command on the vim line, cursor is here

:.!bash
```

or
```vim
:.!date
```

- `.` - Paste at the current line
- `!` - Run bash command
- `date` - Command to run

### Buffers

- `:e {filename}` - open new file in buffer
- `:ls` - view current buffers
- `:b3` - go to budder 3
- `:b vim.md` - go to buffer "vim.md" (if exists)
- `:bp` - go to previouse buffer
- `:bn` - go to next buffer
- `:bufdo {command}` - execute command in all buffers
- `:bd3` - delete buffer 3
- `:ball` - load all buffers in current window (this command is splitting window)

### Windows

- `:sp` - split window horizontally (or `Ctrl+w s`)
- `:vs` - split window vertically (or `Ctrl+w v`)
- `:on` - close all windows except current (or `Ctrl+w o`)
- `Ctrl+w h|j|k|l` - move to the right|bottom|up|left window
- `Ctrl+w r` - rotate windows
- `windo {command}` - execute command in all opened windows
    - Ex: `windo %s/#/@/g` will replace all `#` by `%` symbol

### Remove trailing whitespaces
```vim
:%s/\s\+$//e
```

