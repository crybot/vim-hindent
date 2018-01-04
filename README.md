# (MODIFIED) vim-hindent

This is just a modified version of the vim-hindent plugin that supports range
selection.

Integrates with [hindent](https://github.com/chrisdone/hindent) so every time
you save a Haskell source file it gets automatically prettified.

Simply using `:%!hindent` replaces your whole source file with an error message
from **hindent** when you happen to have a syntax error in your code, this
plugin manages that annoyance.

*Note:* If you prefer *stylish-haskell* use
[vim-stylishask](https://github.com/alx741/vim-stylishask) instead.

## Installation

Compatible with `Vundle`, `Pathogen`, `Vim-plug`.


## Usage

By default, *vim-hindent* will format your code automatically when saving a
Haskell source file, but you can use the `:Hindent` command at any time to
format the current file.

Use `:HindentEnable`, `:HindentDisable`, `:HindentToggle` to enable, disable, or
toggle running `hindent` on save.


## Configuration

Trigger *hindent* when saving (default = 1):

```vim
g:hindent_on_save = 1
```

Number of spaces per indentation (default = '', uses `hindent` default of 2):

```vim
g:hindent_indent_size = 2
```

Max line length (default = `''`, uses `hindent` default of 80):

```vim
g:hindent_line_length = 100
```

## My personal configuration
I personally prefer to disable formatting on save, therefore 

```vim
g:hindent_on_save = 0
```

Then I integrated some useful filetype specific mappings:

The first one uses [vim-textobj-haskell](https://github.com/gilligan/vim-textobj-haskell)
to select the top level binding on which the cursor currently is, and then calls
Hindent to format just that code fraction (the selection gives an helpful visually
clue of whats going on)
```vim
autocmd FileType haskell map == vih:call hindent#Hindent()<CR>
```

The second one is similar, but it does not use text objects. Instead it formats
the whole file by not passing any range to the function. The empty range is treated
as a whole-file selection by the plugin
```vim
autocmd FileType haskell map =G :call hindent#Hindent()<CR>
```
