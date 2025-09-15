ommand Cheatsheet

---

## Part 1: Vim Editor Commands

### Opening and Exiting
- `:w` → save  
- `:wq` / `:x` → save and quit  
- `:q!` → quit without saving  
- `:q` → quit  

### Insert Mode
- `i` → insert before cursor  
- `a` → insert after cursor  
- `I` (Shift + i) → insert at beginning of line  
- `A` (Shift + a) → insert at end of line  
- `o` → open new line below the cursor  
- `O` (Shift + o) → open new line above the cursor  

### Navigation
- `h` → left  
- `l` → right  
- `j` → down  
- `k` → up  
- `0` → beginning of line  
- `^` → first non-space character  
- `$` → end of line  
- `w` → jump forward to start of word  
- `e` → jump to end of word  
- `b` → jump backward to start of word  
- `gg` → beginning of file  
- `G` → end of file  
- `:<n>` → go to line n  

### Editing
- `x` → delete character  
- `dd` → delete whole line  
- `yy` → copy whole line  
- `p` → paste after cursor  
- `P` (Shift + p) → paste before cursor  
- `u` → undo  
- `Ctrl + r` → redo  
- `cw` → change and replace word  
- `cc` → change entire line  

### Copying Multiple Lines
- `:<start_line>,<end_line>y` → copies lines from start_line to end_line (then `p` to paste)  
- `:<n>yy` → copies n lines from line number n down  

### Search and Replace
- `/word` → search for a word  
- `n` → next matching word  
- `N` → previous matching word  

#### Command Breakdown
- `%` → select all lines (no `%` means just the current line)  
- `s` → substitute command  
- `^` → beginning of the line  
- `$` → end of the line  
- `g` → global (replace all occurrences on the line)  

#### Examples
- `:%s/^/ /g` → add spaces at the beginning of the line  
- `:%s/^/new_word/g` → add a word at the beginning  
- `:%s/$/ /g` → add a space at the end of the line  
- `:%s/$/new_word/g` → add a word at the end of the line  
- `:%s/old/new/g` → replace a word  
- `:%s/^  //g` → remove 2 spaces from the beginning (removes indentation)  
- `:%s/old/new/gc` → replace with confirmation  

---

## Part 2: Additional Linux Commands

- `ls -lSh` → lists all files from largest to smallest in current directory  
- `ls -lShr` → lists all files from smallest to largest in current directory  
- `find . -type f -exec du -h {} + | sort -hr` → finds all files in current directory, shows their human-readable size, and sorts from largest to smallest  

