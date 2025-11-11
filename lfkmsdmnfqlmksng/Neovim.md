
## 🪜 Lesson 1 – Basics

### Movement

```
h  → move left  
j  → move down  
k  → move up  
l  → move right
```

### Exiting

```
:q!    → quit without saving  
:wq    → save and quit
```

### Editing

```
x  → delete character  
i  → insert before cursor  
A  → append at end of line  
<Esc>  → return to Normal mode
```

---

## ✂️ Lesson 2 – Deletion & Undo

### Deletion Commands

```
dw   → delete word  
d$   → delete to end of line  
dd   → delete entire line
```

### Counts

```
d2w  → delete two words  
2dd  → delete two lines
```

### Undo / Redo

```
u     → undo last change  
U     → undo changes in current line  
<C-r> → redo
```

---

## 🔁 Lesson 3 – Change & Replace

### Replace

```
r<char>  → replace one character  
R        → replace continuously until <Esc>
```

### Change

```
ce   → change to end of word  
c$   → change to end of line  
c{motion} → change using a motion
```

### Put (Paste)

```
p  → put text after cursor  
P  → put text before cursor
```

---

## 🔍 Lesson 4 – Navigation & Search

### File Navigation

```
<C-g>  → show file info & cursor location  
G      → go to end of file  
gg     → go to top of file  
{num}G → go to specific line
```

### Search

```
/word  → search forward  
?word  → search backward  
n / N  → repeat search (forward/back)
<C-o>  → jump back  
<C-i>  → jump forward
```

### Matching & Substitution

```
%                → match (), [], {}  
:s/old/new/      → replace first occurrence in line  
:s/old/new/g     → replace all in line  
:%s/old/new/gc   → replace all in file with confirmation
```

---

## 📁 Lesson 5 – Files & External Commands

### Shell Commands

```
:!command     → run external shell command
```

### File Writing & Reading

```
:w FILENAME   → write file to disk  
:r FILENAME   → read file into buffer  
:r !command   → insert command output
```

### Visual Selection Write

```
v{motion} :w FILENAME
```

---

## 🧩 Lesson 6 – Advanced Editing

### Opening & Appending

```
o  → open new line below  
O  → open new line above  
a  → append after cursor  
A  → append after end of line
```

### Copy & Paste

```
y{motion}  → yank (copy)  
p / P      → put (paste)
```

### Replace Mode

```
R  → enter replace mode (until <Esc>)
```

### Settings

```
:set ic     → ignore case  
:set hls is → highlight & incremental search  
:set noic   → disable ignorecase  
:set invic  → toggle ignorecase
```

---

## 💡 Lesson 7 – Help, Completion, and Configuration

### Help

```
:help          → open help  
:help TOPIC    → help for topic  
<C-w><C-w>     → switch windows  
:q             → close help window
```

### Command Completion

```
<C-d>  → list possible completions  
<Tab>  → cycle through matches
```

### Configuration (`init.lua`)

```
:exe 'edit' stdpath('config')..'/init.lua'
:read $VIMRUNTIME/example_init.lua
:w ++p
:e $MYVIMRC   → reopen config file
```
