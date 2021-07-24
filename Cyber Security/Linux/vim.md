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
set hlsearch
set incsearch
set laststatus=2
set showcmd
color industry

syntax on

hi LineNr cterm=bold ctermfg=DarkGrey ctermbg=None
hi CursorLineNr cterm=bold ctermfg=Green ctermbg=None
hi CursorLine ctermfg=None ctermbg=None cterm=bold
hi Search cterm=reverse ctermbg=none ctermfg=none

autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab
let g:indentLine+char = '|'
```

Indent
1. VISUAL LINE: `Shift+v`
2. select lines
3. hit ">" (`shift+.`)

