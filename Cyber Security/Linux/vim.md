use gvim instead of vim for clipboard support

vim >= 7.3.74
```
:set clipboard=unnamedplus
```


行號
```
:set nu
```

Ctrl + n 自動補完

```bash
set clipboard=unnamedplus
set nu
set ai
set cursorline
set bg=dark
color industry

syntax on

hi LineNr cterm=bold ctermfg=DarkGrey ctermbg=None
hi CursorLineNr cterm=bold ctermfg=Green ctermbg=None
hi CursorLine ctermfg=None ctermbg=None cterm=bold

autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab
let g:indentLine+char = '|'
```