# Visual Studio Code Example Setup #

This repository contains some example setups for using VS Code, a great free, open source, multi-platform editor/IDE that supports numerous languages and features via an extensive and ever-growing array of extensions/plugins. I have abandoned Eclipse in favor of VS Code as it seems the depth and breadth of extensions (most critically for me - Vim) is outpacing those for Eclipe. It is very light-weight and therefore easy to become immediately productive.

The simplest way to use vscode is just **File->Open...** and navigate to the root of your project. Vscode will scan the directory tree, show the tree, index the files, and away you go. If you have a more complicated project involving multiple directory trees or want to customize what shows up in the project explorer, you can create a workspace file to configure this (but often this is not necessary). Regardless of whether you have a specific workspace file set up, vscode considers any directory you open a _workspace_.

## Basic Setup ##

There are two differnt scopes for configuring and setting how vscode behaves - user scope and workspace scope. All settings files are in JSON format. The user settings files are located in your home directory (exact path varies with OS). The main one is `settings.json` which  configures look & feel, default behavior, extensions, etc. Additionally, there is `keybindings.json` if you want to customize shortcuts. On MacOS, these two files are located in `$HOME/Library/Application Support/Code/User/`.

In addition to the user scoped files, vscode houses workspace setting files in a `.vscode/` directory at the root of the project directory that you open. The typical files located here are `tasks.json`, `launch.json`, and a language configuration file (in the case of C it would be `c_cpp_properties.json`). These files are typically hand-edited from examples or templates in order to customize them for a project. Also, if you make workspace-specific changes (e.g., unique extension behavior, language formatting differences, etc.), a `settings.json` file will be created in this directory.

`tasks.json` contains command-line tasks to be run, for example make commands if you project is make-based. These commands can be run by executing **Terminal->Run Task...**.

Check out the full vscode documentation [here](https://code.visualstudio.com/docs).

## Repo Structure ##

This repo contains example settings for user setttings, project/workspace settings, and a specific example for building and testing Nordic NRF5-SDK example embedded C projects. The directory structure is as follows:

* `user/` - typical user scope settings located in user's home dir
* `project/` - example template for new C and embedded C projects
* `nrf5_examples/` - configuration for building and testing NRF-SDK example code

When starting a new C project or converting a current one to use vscode, the `project/macos_C/.vscode/` directory can be copied into the project root directory and the contained files modified as needed. Likewise, when starting a new embedded C (i.e., cross-compile) project, the `project/embed_C/.vscode/` directory can be copied and modified as needed.

To use the NRF examples, copy the contents of the `nrf5_examples` directory into the `examples/` subdir of the NRF5-SDK. Then navigate to the desired example project and open its Makefile. With the makefile open, execute **Terminal->Run Task...** and select _make using open Makefile_ and then select the desired make command, e.g. _default_. This will run the make command in the directory containing the make file as if you had navigated to that directory and run the same _make default_ command from that directory. Likewise, if you want to debug this application, execute **Run Start Debugging** which will use the Makefile's directory and the `launch.json` file to start a debugger session on the target.

## Extentions Installed ##

The following list is my currently installed extentions. This is always an evolving list, but the ones toward the top are the ones I most frequently rely on, with Vim being the key extension.

* Vim by vscodevim
* C/C++ by Microsoft
* One Dark Pro theme by binaryify
* vscode-icons by VSCode Icons Team
* Git History by Don Jayamanne
* TODO Highlight by Wayou Liu
* Prettier - Code formatter by Esben Petersen:w
* Whitespace+ by Sardul Mahadik
* markdownlint by David Anson
* Code Runner by Jun Han
* LinkerScript by Zixuan Wang
* Native Debug by WebFreak
* Path Autocomplete by Mihai Vilcu
* CMake Tools by Microsoft (disabled)

***

## VIM Cheat Sheet ##

I am a big fan of Vim, but there are always more useful commands, keystrokes, mappings that I haven't committed to muscle memory yet, so I created this list to help me work them into my repertoire.

Screen navigation:

    <C-E>       scroll up   one line
    <C-Y>       scroll down one line
    <C-U>       scroll up   half screen
    <C-D>       scroll down half screen
    <C-F>       scroll up   full screen
    <C-B>       scroll down full screen
    zz  z.      puts line w/ cursor in middle of window
    zt          puts line w/ cursor at top of window
    zb          puts line w/ cursor at top of window
    gg          jump to first line in buffer
    G           jump to last line in buffer

Cursor motions:

    H   L       puts cursor at beginning / end of line
    M           put cursor at middle of screen
    ge  gE      "go (prev)end" go to previous end of word / WORD
    f{char}     "find" (move cursor to) next occurance of char
    F{char}     find (move cursor to) prev occurance of char
    t{char}     "till" the char before next occurance of char
    T{char}     "till" the char after  prev occurance of char name
    ;   ,       repeat previous f,F,t,T forward / backward
    m{name}     set mark using a single character name (lower per file, CAP is global)
    '{name}     jump to mark with given character name

Text objects:

    aw  as  ap      a word, a sentence, a paragraph (includes surrounding whitespace)
    iw  is  ip      inner word, inner sentence, inner paragraph (does NOT include surrounding whitespace)
    a"  a'  a`  a double/single/back quote
    a)  a]  a}  a paren/bracket/curlybracket
    i"  i'  i`  innerdouble/single/back quote
    i)  i]  i}  inner paren/bracket/curlybracket
    at  a>      a tag (xml) / tag content
    it  i>      inner tag (xml) / tag content

Cursor history:

    <C-O>       jump to previous location in history
    <C-I>       jump to next location in history
    '.          jump to last modification line
    `.          jump to exact spot in last modification line
    <C-]>  :tag {name}  jump to definition of keyword under the cursor
    <C-T>  :pop         jump to older entry in tag stack
    :tags       show contents of tag stack

Searching:

    /fred|joe   search for fred OR joe
    /patt/e     cursor stops at end of match
    \v  \V      front of pattern uses normal regex, or no special chars
    \c  \C      for search case (in) sensitivity, can occur start or end of pattern
    \zs  \ze    to surround start and/or end of search pattern of interest
    /\v<word>   the <> is used to delimit a spepcific word to search for
    n  N        repeat last search fwd/backward
    gn  gN      "go next", repeat last fwd/back search enabling char mode visual select
    *           find next forward  occurrence of word
    #          find next backward occurrence of word

Registers:

    "{reg}yy    yank lines into register {reg}
    "{REG}yy    append lines into register {reg}
    "{reg}p     put the text from register {reg} after the cursor
    <C-R>{reg}  paste register {reg} contents (in insert mode)
    "+          to access system clipboard
    "0          to access yank register

Visual mode:

    gq          visual selection, reflow and wordwrap blocks of text (good for documentation)
    gv          reselect last visual mode
    af          visual mode command which selects increasingly large blocks of text
    o           go to other end in visual select mode
    :'<,'>normal @{reg}     run macro in parallel
    :'<,'>normal .          visual mode dot command

Ex commands:

    :reg        shows register contents
    :cd ..      move to parent directory
    :his        list of all your commands
    :[range]s/{patt}/{str}/[flags]      complete substitute command
        range   n,m line range, % entire file, '<,'> visual selection
        flags   g replaces all in the line, c confirms each replacement, iI ignores/no_ignore case in pattern, n reports number of matches
    :%s/patt//n     gives count of matches

Macros:

    q{reg}      create macro (end with q)
    @{reg}      run macro (@@ repeats last macro)

Programming stuff:

    [[          jump to top of current function
    ]]          jump to top of next function
    %           find matching brace or paren
    =           smart indent visual block (== indent line)
    gq{motion}  format {motion} or visual block
    ga          "go ascii" display dec,hex,octal value of ascii character under cursor
    gd          "go defintion", jump to definition whose name is under cursor
    gf          "go file", open file whose name is under cursor
    <C-A>       increment number under cursor
    <C-X>       decrement number under cursor

Miscellaneous:

    gh          "go hover", equivalent to hovering your mouse over whereever the cursor is
    guu         "go lowercase", make entire line lowercase
    gUU         "go Uppercase", make entire line uppercase
    g~{motion}  "go toggle", toggle case for motion
    ~           toggle case char by char, or entire visual selection
    gp  gP      "go put", paste and leave cursor at end of pasted text

## My Customizations ##

Here are my key customizations that deviate from standard vim. I have tried to make my vim (via `$HOME/.vimrc`), JetBrains IdeaVim (via `$HOME/.ideavimrc`) and vscode Vim (via `$HOME/Library/Application Support/Code/User/settings.json`) work as similar as possible, given the limitations of the JetBrains and vscode plugins/extentions. See my [dotfiles repo](https://github.com/markjbianchi/dotfiles) for my `.vimrc` and `.ideavimrc` files.

Searching:

    \<space>    toggle search highlighting
    n N         search forward/backward keeping results in middle of window
    * #         search word under cursor fwd/bwrd keeping results in middle of window

 Display control:

    \N          toggle non-printable (tab, \n, etc) chars   TODO
    \vs         vertical split window into new editor tab
    \hs         horizontal split editor window              TODO
    \w          toggle on/off trailing whitespace           TODO
    \W          remove trailing whitespace                  TODO

 Editing shortcuts:

    <Tab>       indent 1 level (visual mode)
    <S-Tab>     outdent 1 level (visual mode)
    go          open line below w/o entering insert mode (normal mode)
    gO          open line above w/o entering insert mode (normal mode)

 Miscellaneous

    \<Tab>      apply current tab settings to file         TODO
    <C-K>       ex command recall, <C-J>, <C-K> to scroll dwn/up
    gy          select entire buffer
    <C-Tab>     cycle forward  to next buffer               TODO
    <C-S-Tab>  cycle backward to next buffer               TODO
    Q           re-run last macro

Editor window mappings

    \hs         horizontal split window with current buffer TODO
    \vs         vertical   split window with current buffer
    \us         remove split                                TODO
    gh          left  move between windows
    gl          right move between windows
    gk          up    move between windows
    gj          down  move between windows

## Plugin Emulations ##

VS Code's Vim (and Ideavim) doesn't support vim plugins, but rather has chosen to emulate a few of the most popular ones. Here are some quick hints for these, plus links to the original plugins.

vim-commentary[https://github.com/tpope/vim-commentary](https://github.com/tpope/vim-commentary):

    gcc         toggle line comment
    gC          toggle block comment in visual mode

vim-surround[https://github.com/tpope/vim-surround](https://github.com/tpope/vim-surround):

    ys{motion}{desired char}        surround something with something using motion
    S{desired char}                 surround when in visual mode
    ds{existing char}               deletes existing surround
    cs{existing char}<desired char} deletes existing surround
                                    use  t  to mean an html/xml tag
                                    use right )]}> to surround tight
                                    use left  ([{< to separate with a space

vim-sneak [https://github.com/justinmk/vim-sneak](https://github.com/justinmk/vim-sneak):

    s{char}{char}   jump to location specified by 2 chars matching text
    S{char}{char}   s for forward, S for backward
    ;  ,        go to next match forward / backward
    <C-O>  ``   to return to starting point
