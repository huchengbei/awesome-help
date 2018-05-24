# vim-help

## Move The Cursor
```
        ^           Hint:
        k               h: move left
   < h     l >          l: move right
        j               k: move up
        v               j: move down
                        0: move to the start of a line
                        $: move to the end of a line
                        w: move to the start of next word
                        e: move to the end of the word
```

## Exiting Vim
```
    Press ESC, and then
    :q      quit
    :q!     quit and trash all changes
    :w[filename]     save, or save to the file
    :wq     save and quit
```

## Editing
```
    x      delete a character
    i      insert before the cursor
    A      append after a line
    a      append after the cursor
    O      create a new line above the cursor and turn to insert mode
    o      create a new line below the cursor and turn to insert mode
```

## Deletion
```
    dw      delete a word and the space after the word
    de      delete a word
    d$      delete a line from the cursor
    dd      delete the whole line

    Summary
    d   [num]   motion
    [num]   d   motion

    num means one if it was omitted
    motions:
    w   to the start of next word
    e   to the end of this word
    $   to the end of this line
```

## Undo & Redo
```
    u   undo the last commands
    U   fix the whole line
    CTRL+R  redo the commands(undo the undo's)
```

## Put
```
    When we delete something, it will be putted into a register. 
    Press v and move the cursor to select some contents, and press y, the contends will be putted into a register too

    Press 'p', it whill paste into text.

    Tip:
    paste in the next line or next character
```
## Replace & Change
```
    r   replace a character
    R   replace till press ESC(end replace mode)

    ce  delete a word(without the space apend) and turn to insert mode
    cw  delete a word and turn to insert mode
    c$  delete the rest of a line and turn to insert mode

    Summary
    c [num] motion
    it can be used too
```

## Cursor Location & File Status
```
    CTRL+G  show the location of the cursor
    G   move to bottom in the file
    gg  move to start in the file
    num+G   move to the num line
```

## Matching Parentheses
```
    %   move to the matching parentheses or bracket
```

## Substitute & Search
```
    :s/old/new  change the first old to new
    :s/old/new/g    change all old to new in the line
    :#,#s/old/new/g change all old to new from # line to # line
    :%s/old/new/g   change all old to new in the whole file
    :%s/old/new/gc  change all old to new in the whole file with a prompt

    /xxx    search xxx in forward
    ?xxx    search xxx in backward
    use n to find next occurrence in the same direction
    use N to find next occurrence in the opposite direction
    CTRL+O  take back to old positions
    CTRL+I  take to newer positions
```

## Execute External Commands
```
    :!  followed by an external command t execute that command
```

## Write
```
    Use v to select text
    Press ':' to show '<,'>
    type w filename to write the select content to the file
```

## Merge Files
```
    :r filename to insert the contents of a file
    :r !command to insert the result of the command
```

## Set Option
```
    :set ic Set the 'ic'(Ignore case) option
    :set hls is Set the 'hisearch'(Highlight) and 'incsearch'(show partial matchs)
    :set noic   To disable ignoring case

    And we can create a file named 'vimrc' in the home directory to save our setting
```

## Getting Help
```
    we have three method to get help
    * :help <ENTER>
    * press <F1>
    * press <HELP>
    
    CTRL+W  Jump to another window
    :q  quit HELP window

    if we want to find a help about command, we can use this:
    :help command   Find the help about command
    such as
    :help w
    :help c_CTRL_D
    :help insert-index
    :help user-manual
```

## Completion
```
    First, type the start of a command,such as :e
    CTRL+D  Show the list of commands start with 'e'
    <TAB>   Complete the command with a command start with 'e'
```