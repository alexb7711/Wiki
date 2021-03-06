# [Code Folding](https://vim.fandom.com/wiki/Folding)
It is convenient to temporarily fold away (hide) parts of your file, leaving only an outline of the major parts visible. This tip presents an overview of using folding.

Many programming languages have a syntax file that supports folding. Typically, each function is regarded as a fold that can be opened or closed. With all folds closed, you see only the first line of each function for an overview of the program.

## Folding Methods
To activate folding in your text, you will need to set the `foldmethod` option.

The possible values are:
* `manual` – folds must be defined by entering commands (such as zf)
* `indent` – groups of lines with the same indent form a fold
* `syntax` – folds are defined by syntax highlighting
* `expr` – folds are defined by a user-defined expression
* `marker` – special characters can be manually or automatically added to your text to flag the start and end of folds
* `diff` – used to fold unchanged text when viewing differences (automatically set in diff mode)

### Manual Folding
Normally it is best to use an automatic folding method, but manual folding is simple and can be useful for dealing with small folds.

When `foldmethod` is set to manual (or marker), a fold can be created in Normal mode by typing `zf`{motion}. For example, `zf'a` will fold from the current line to wherever the mark a has been set, or `zf3j` folds the current line along with the following 3 lines. If you want to create folds in a text file that uses curly braces to delimit code blocks ({...}), you can use the command `zfa`} to create a fold for the current code block.

Alternatively, an arbitrary group of lines can be folded by selecting them to enter Visual mode and pressing `zf`. This allows you to preview the section you've selected before you fold it. The above example of folding the current code block could also be accomplished by first selecting the code block delimited by the curly braces (`va`}) and then creating the fold (`zf`). Putting this together gives `va`}`zf`.

Manual folds can also be created in Command mode :{range}`fo`[`ld`], e.g., the current line along with the following three lines (as in the example above) can be folded by running `:,+3fo`.

Use `zd` to delete the fold at the cursor (no text is deleted, just the fold markers); `zD` is used to recursively delete folds at the cursor.

### Indent Folding
As noted above, with `foldmethod` set to indent, lines with the same level of indentation will be folded together. Note this means text like this:

```
Line one
  Line two
  Line three
Line four
```

will be folded as follows, which may not be expected:

```
Line one
+ Line two and three
Line four
```

Since folding by indent may not be as clear as you like, the `foldcolumn` is especially useful for this method. Setting `foldcolumn` to at least the level of folds you want displayed will show a sidebar, in which you can see which lines in the file can be folded, or are already folded, with a '+' (closed) or '-' (open) indicator.

### Syntax Folding
Try `:setlocal foldmethod=syntax`. Many syntax files define folding based on the language syntax, although you may need to enable it by setting syntax file options. If a specific syntax file doesn't define folding, you can define your own.

Note that this particular fold method especially may define too many folds for your liking. You can change this using the `foldnestmax` option, by setting it to a value low enough for your liking.

### Indent folding with manual `foldsEdit`
If you like the convenience of having Vim define folds automatically by indent level, but would also like to create folds manually, you can get both by putting this in your `vimrc`:

```
augroup vimrc
  au BufReadPre * setlocal foldmethod=indent
  au BufWinEnter * if &fdm == 'indent' | setlocal foldmethod=manual | endif
augroup END
```

The first `autocommand` sets 'indent' as the fold method before a file is loaded, so that indent-based folds will be defined. The second one allows you to manually create folds while editing. It's executed after the `modeline` is read, so it won't change the fold method if the `modeline` set the fold method to something else like 'marker' or 'syntax'.

## Opening and Closing Folds
Opening and closing `foldsEdit`
The command `zc` will close a fold (if the cursor is in an open fold), and `zo` will open a fold (if the cursor is in a closed fold). It's easier to just use `za` which will toggle the current fold (close it if it was open, or open it if it was closed).

The commands `zc` (close), `zo` (open), and `za` (toggle) operate on one level of folding, at the cursor. The commands `zC`, `zO` and `zA` are similar, but operate on all folding levels (for example, the cursor line may be in an open fold, which is inside another open fold; typing `zC` would close all folds at the cursor).

The command `zr` reduces folding by opening one more level of folds throughout the whole buffer (the cursor position is not relevant). Use `zR` to open all folds.

The command `zm` gives more folding by closing one more level of folds throughout the whole buffer. Use `zM` to close all folds.

Mappings to toggle `foldsEdit`
With the following in your `vimrc`, you can toggle folds open/closed by pressing `F9`. In addition, if you have :set `foldmethod=manual`, you can visually select some lines, then press `F9` to create a fold.

```
inoremap <F9> <C-O>za
nnoremap <F9> za
onoremap <F9> <C-C>za
vnoremap <F9> zf

```

Here is an alternative procedure: In normal mode, press Space to toggle the current fold open/closed. However, if the cursor is not in a fold, move to the right (the default behavior). In addition, with the manual fold method, you can create a fold by visually selecting some lines, then pressing Space.

```
nnoremap <silent> <Space> @=(foldlevel('.')?'za':"\<Space>")<CR>
vnoremap <Space> zf
```

In the first mapping for Space, @= refers to the expression register (:help @=). The following expression is evaluated when Enter is pressed (<CR>). The value of `foldlevel`('.') is determined (the fold level at the current line, or zero if the current line is not in a fold). If the result is nonzero (true), the result is `za` (toggle fold); otherwise it is "\<Space>", which evaluates back to the default behaviour of the <Space> key (move forward by one character). `:help expr1`.
