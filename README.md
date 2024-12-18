# vim-macros
Useful vim macros.

## Wrap/unwrap lines
```vim
map <silent> <F9> :set invwrap<CR>
```

## Copy/paste shortcuts 
```vim
" - select all 
nmap <C-A> ggVG 
imap <C-A> <ESC><C-A>i 
" CTRL-X and SHIFT-Del are Cut 
vnoremap <C-X> "+x 
vnoremap <S-Del> "+x 
" CTRL-C and CTRL-Insert are Copy 
vnoremap <C-C> "+y 
vnoremap <C-Insert> "+y 
" CTRL-V and SHIFT-Insert are Paste 
map <C-V>       "+gP 
map <S-Insert>      "+gP 
cmap <C-V>      <C-R>+ 
cmap <S-Insert>     <C-R>+ 
command CWD cd %:p:h
```

## Reversing lines in the buffer
```vim
com! Reverse :g/^/m0 | :nohlsearch
nnoremap = :Reverse<Cr>
```
Based on: https://superuser.com/questions/189947/how-do-i-reverse-selected-lines-order-in-vim#189956                            

## Pretty print XML
```vim
com! FormatXML :set tabstop=2 | :%!python3 -c "import xml.dom.minidom, sys, os; dom = xml.dom.minidom.parse(sys.stdin); pretty_xml = dom.toprettyxml(); pretty_xml = os.linesep.join([s for s in pretty_xml.splitlines() if s.strip()]); print(pretty_xml)"
nnoremap = :FormatXML<Cr>
```
Based on: https://vim.fandom.com/wiki/Pretty-formatting_XML

## Pretty print JSON
```vim
com! FormatJSON :%!python -c "import json, sys; obj = json.load(sys.stdin); print(json.dumps(obj, indent=2, sort_keys=True))"
nnoremap = :FormatJSON<Cr>
```
Based on: https://pascalprecht.github.io/posts/pretty-print-json-in-vim/

## Swap files in single location
Instead of storing the `.swp` files alongside the file being viewed/edited, you can direct vim to just store them in a single location:
```vim
set directory=$HOME/.vim/swapfiles//
```
Based on: https://stackoverflow.com/a/21026618/4698227

## Turning off backup files
```vim
set backupcopy=no
```
Some times needed when accessing remote files that are mounted through [gvfs](https://github.com/vim/vim/issues/5309).
