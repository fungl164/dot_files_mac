" ~/.vimrc
" vim:set ft=vim et tw=78 sw=2:

" Section: Options {{{1
" ----------------
"
let g:Powerline_symbols = 'unicode'
set guifont=mensch-Powerline\ 10

set nocompatible
set autoindent
set autowrite       " Automatically save before commands like :next and :make
set backspace=2
set backupdir=~/.vim/tmp
set cmdheight=2
set display=lastline
set incsearch       " Incremental search
set expandtab       " Use spaces instead of tabs
set laststatus=2    " Always show status line
set lazyredraw
set modelines=5     " Debian likes to disable this
" set mousemodel=popup
" set nobackup
" set nowb
" set n
set pastetoggle=<F3>
set scrolloff=1
set shell=/bin/bash\ -i
set showcmd         " Show (partial) command in status line.
set showmatch       " Show matching brackets.
set smartcase       " Case insensitive searches become sensitive with capitals
set smartindent
set smarttab        " sw at the start of the line, sts everywhere else
set splitbelow      " Split windows at bottom
set statusline=[%{winnr()}\ %n]\            " buffer number 
set statusline+=%<%.99f\        " filename   
set statusline+=%h%w%m%r        " status flags
set statusline+=%{SL('CapsLockStatusline')}%y
set statusline+=%{fugitive#statusline()} " git branch (fugitive)
set statusline+=%#ErrorMsg#%{SL('SyntasticStatuslineFlag')}%*%=
set statusline+=0x%-8B          " character value
set statusline+=%-14.(%l,%c%V%) " line, character
set statusline+=%P              " file position
set suffixes+=.dvi  " Lower priority in wildcards
set tags+=../tags,../../tags,../../../tags,../../../../tags
set timeoutlen=1200 " A little bit more time for macros
set ttimeoutlen=50  " Make Esc work faster
set visualbell
set virtualedit=block
set wildmenu
set wildmode=longest:full,full
set wildignore+=*~,*.aux,tags
set wildignore+=*/.git/*,*/.hg/*,*/.svn/*   " for Linux/MacOSX
set wildignore+=*/tmp/*,*.so,*.swp,*.zip
set winaltkeys=no

if exists('+undofile')
  set undofile
endif

if v:version >= 700
  set viminfo=!,'20,<50,s10,h
endif

if has("balloon_eval") && has("unix")
  set ballooneval
endif

if exists("&breakindent")
  set breakindent showbreak=+++
elseif has("gui_running")
  set showbreak=\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ +++
endif

if has("eval")
  let &fileencodings = substitute(&fileencodings,"latin1","cp1252","")
endif

set fileformats=unix,dos,mac
set grepprg=grep\ -rnH\ --exclude='.*.swp'\ --exclude='*~'\ --exclude=tags

if has("eval")
  let &highlight = substitute(&highlight,'NonText','SpecialKey','g')
endif

set spellfile=~/.vim/spell/en.utf-8.add
if $TERM == 'xterm-256color' || $TERM == 'screen-256color'
  set t_Co=256
endif

if $TMUX == ''
  set clipboard+=unnamed
endif

" }}}1

" Section: Visual {{{1
" --------------- 
"
"
syntax on
colorscheme monokai-2

set number
set mouse=a
set ttymouse=xterm2
set ttyfast

set foldmethod=syntax
set foldlevel=4

autocmd WinEnter * setlocal cursorline 
autocmd WinLeave * setlocal nocursorline 

augroup RCVisual
  autocmd!
  autocmd VimEnter *  if !has("gui_running") | set background=dark notitle noicon | endif
  autocmd GUIEnter *  set background=light title icon cmdheight=2 lines=25 columns=80 guioptions-=T
  autocmd GUIEnter *  if has("diff") && &diff | set columns=165 | endif
  autocmd GUIEnter *  silent! colorscheme vividchalk
  autocmd GUIEnter *  call s:initialize_font()
  autocmd GUIEnter *  let $GIT_EDITOR = 'false'
  autocmd Syntax css  syn sync minlines=50
  autocmd Syntax csh  hi link cshBckQuote Special | hi link cshExtVar PreProc | hi link cshSubst PreProc | hi link cshSetVariables Identifier
augroup END

" }}}1

" Section: Plugins {{1
" ----------------------
"
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()

Bundle 'gmarik/vundle' 
Bundle 'Lokaltog/vim-easymotion'
Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
Bundle 'tpope/vim-rails.git'
Bundle 'L9'
Bundle 'FuzzyFinder'
" Bundle 'git://git.wincent.com/command-t.git'
Bundle 'scrooloose/nerdtree'
Bundle 'kien/ctrlp.vim.git'
Bundle 'tComment'
Bundle 'surround.vim'
Bundle 'skwp/vim-rspec.git'
Bundle 'matchit.zip'
Bundle 'tpope/vim-fugitive.git'
Bundle 'rstacruz/sparkup.git'
Bundle 'scrooloose/syntastic.git'
Bundle 'bufexplorer.zip'
Bundle 'skalnik/vim-vroom.git'


filetype plugin indent on     " required!
" }}}1


" Section: Mappings {{{1
" ----------------------
"

let mapleader = ","

map <Esc>[B <Down>

" Clear last search highlighting
nnoremap <Space> :noh<cr>

" Use semicolon instead of colon for commands"
nnoremap ; :

imap ii <Esc>

" Faster Ctrlp
noremap <leader>p :CtrlP<cr>
noremap <leader>pb :CtrlPBuffer<cr>
noremap <leader>pa :CtrlPMixed<cr>

noremap gw <C-w><C-w>

" Faster buffer rotate
noremap ;bn :bn<cr>
noremap ;bp :bp<cr>
noremap ;ls :ls<cr>

" Easier navigation between split windows
" nnoremap <c-j> <c-w>j
" nnoremap <c-k> <c-w>k
" nnoremap <c-h> <c-w>h
" nnoremap <c-l> <c-w>l
" 
nnoremap <leader>j <c-w>j
nnoremap <leader>k <c-w>k
nnoremap <leader>h <c-w>h
nnoremap <leader>l <c-w>l

" Edit & source .vimrc
nnoremap <leader>ev :vsplit $MYVIMRC<cr>
nnoremap <leader>sv :source $MYVIMRC<cr>

" Even easier navigation between windows
map <Tab> <C-W>w
map <Bar> <C-W>v<C-W><Right>
map - <C-W>s<C-W><Down>
map <S-Tab> :tabn<cr>
"
" Switch between windows, maximizing the current window
"
noremap <leader>wh <C-W>h<C-W>_
noremap <leader>wj <C-W>j<C-W>_
noremap <leader>wk <C-W>k<C-W>_ 
noremap <leader>wl <C-W>l<C-W>_ 
noremap <leader>w= <C-W>=<cr> 

" noremap <C-W><left> <c-w>h
" noremap <C-W><down> <c-w>j
" noremap <C-W><up> <c-w>k
" noremap <C-W><right> <c-w>l

" Switch betwen tabs
noremap <leader>th :tabp<cr>
noremap <leader>tl :tabn<cr>
noremap <leader>tn :tabe<cr>

noremap <c-t><c-t> :tabn<cr>

noremap <c-t>h :tabp<cr>
noremap <c-t>l :tabn<cr>
noremap <c-t>n :tabe<cr>

" Move window to next tab
map <c-t>ml :call MoveToNextTab()<CR><C-w>H
nnoremap <c-t>mj :call MoveToNextTab()<CR>
nnoremap <c-t>mk :call MoveToPrevTab()<CR>
map <c-t>mh :call MoveToPrevTab()<CR><C-w>H


" Create vertical split buffer view 
noremap <leader>vsb :vert sb

" Insert blank lines without going into insert mode
nmap go o<esc>
nmap gO O<esc>

" Shortcut for =>
imap <C-l> <Space>=><Space>

" indent/unindent visual mode selection with tas/shift+tab
vmap <tab> >gv
vmap <s-tab> <gv

" F7 reformats the whole file and leaves you where you were (unlike gg)
map <silent> <F7> mzgg=G'z :delmarks z<CR>:echo "Reformatted."<CR>

" open files in directory of current file
cnoremap %% <C-R>=expand('%:h').'/'<cr>
map <leader>e :edit %%
map <leader>v :view %%

" rename current file
map <leader>n :call RenameFile()<cr>

" AckGrep current word
map <leader>a :call AckGrep()<CR>
" AckVisual current selection
vmap <leader>a :call AckVisual()<CR>

" File tree browser - backslash
map \ :NERDTreeToggle<CR>
" map \| :NERDTreeFind<CR>
let NERDTreeMouseMode = 3

" Vroom Tests
" let g:vroom_map_keys = 0
" silent! map <unique> <Leader>t :VroomRunTestFile<CR>
" silent! map <unique> <Leader>T :VroomRunNearestTest<CR>
silent! map <unique> <Leader>tc :!bundle exec cucumber --profile=wip<CR>

" FuzzyFinder 
map <leader>ff :FufFile **/<CR>
map <leader>fb :FufBuffer<CR>

" BufExplorer
map <leader>be :BufExplorer<CR>

" RSpec 
let g:RspecKeymap=0
map <leader>R :RunSpec<cr>
map <leader>r :RunSpecLine<cr>

" TPope's mappings
nmap <silent> <F2> :exec &nu==&rnu? "se nu!" : "se rnu!"<CR>
" nnoremap <F3> :set invpaste paste?<CR>
" imap <F3> <C-O>:set invpaste paste?<CR>
" set pastetoggle=<F3>
map <C-F4>  :bdelete<CR>
nmap <silent> <F6> :if &previewwindow<Bar>pclose<Bar>elseif exists(':Gstatus')<Bar>exe 'Gstatus'<Bar>else<Bar>ls<Bar>endif<CR>
nmap <silent> <F7> :if exists(':Glcd')<Bar>exe 'Glcd'<Bar>elseif exists(':Rlcd')<Bar>exe 'Rlcd'<Bar>else<Bar>lcd %:h<Bar>endif<CR>
map <F9> :Run<CR>

" }}}1


" Section: Cut n Paste {{{1
" --------------------
"
" CTRL-X and SHIFT-Del are Cut
vnoremap <C-X> "+x
vnoremap <S-Del> "+x

" CTRL-C and CTRL-Insert are Copy
vnoremap <C-C> "+y
vnoremap <C-Insert> "+y

" CTRL-V and SHIFT-Insert are Paste
map <C-V> "+gP
map <S-Insert> "+gP

cmap <C-V> <C-R>+
cmap <S-Insert> <C-R>+

" Pasting blockwise and linewise selections is not possible in Insert and
" Visual mode without the +virtualedit feature.  They are pasted as if they
" were characterwise instead.
" Uses the paste.vim autoload script.

exe 'inoremap <script> <C-V>' paste#paste_cmd['i']
exe 'vnoremap <script> <C-V>' paste#paste_cmd['v']

imap <S-Insert>         <C-V>
vmap <S-Insert>         <C-V>

" Use CTRL-Q to do what CTRL-V used to do
noremap <C-Q>           <C-V>

" CTRL-A is Select all
noremap <C-A> gggH<C-O>G
inoremap <C-A> <C-O>gg<C-O>gH<C-O>G
cnoremap <C-A> <C-C>gggH<C-O>G
onoremap <C-A> <C-C>gggH<C-O>G
snoremap <C-A> <C-C>gggH<C-O>G
xnoremap <C-A> <C-C>ggVG

" CTRL-Tab is Next window
noremap <C-Tab> <C-W>w
inoremap <C-Tab> <C-O><C-W>w
cnoremap <C-Tab> <C-C><C-W>w
onoremap <C-Tab> <C-C><C-W>w

" }}}1



" Section: Commands {{{1
" -----------------------
"
if has("autocmd")
  filetype on

  augroup FTMisc " {{{2
    autocmd!

    autocmd VimLeavePre * mksession! ~/.vim/.vim.sess

    autocmd FocusLost   * silent! wall
    autocmd FocusGained * if !has('win32') | silent! call fugitive#reload_status() | endif
    autocmd SourcePre */macros/less.vim set laststatus=0 cmdheight=1
    if v:version >= 700 && isdirectory(expand("~/.trash"))
      autocmd BufWritePre,BufWritePost * if exists("s:backupdir") | set backupext=~ | let &backupdir = s:backupdir | unlet s:backupdir | endif
      autocmd BufWritePre ~/*
            \ let s:path = expand("~/.trash").strpart(expand("<afile>:p:~:h"),1) |
            \ if !isdirectory(s:path) | call mkdir(s:path,"p") | endif |
          \ let s:backupdir = &backupdir |
          \ let &backupdir = escape(s:path,'\,').','.&backupdir |
          \ let &backupext = strftime(".%Y%m%d%H%M%S~",getftime(expand("<afile>:p")))
    endif

    autocmd User Rails-javascript setlocal ts=2
    autocmd User Fugitive if filereadable(fugitive#buffer().repo().dir('fugitive.vim')) | source `=fugitive#buffer().repo().dir('fugitive.vim')` | endif

    autocmd BufNewFile */init.d/*
          \ if filereadable("/etc/init.d/skeleton") |
          \   0r /etc/init.d/skeleton |
          \   $delete |
          \   silent! execute "%s/\\$\\(Id\\):[^$]*\\$/$\\1$/eg" |
          \ endif |
          \ set ft=sh | 1

    autocmd BufNewFile */.netrc,*/.fetchmailrc,*/.my.cnf let b:chmod_new="go-rwx"
    autocmd BufNewFile  * let b:chmod_exe=1
    autocmd BufWritePre * if exists("b:chmod_exe") |
          \ unlet b:chmod_exe |
          \ if getline(1) =~ '^#!' | let b:chmod_new="+x" | endif |
        \ endif
    autocmd BufWritePost,FileWritePost * if exists("b:chmod_new")|
          \ silent! execute "!chmod ".b:chmod_new." <afile>"|
          \ unlet b:chmod_new|
          \ endif

    autocmd BufWritePost,FileWritePost ~/.Xdefaults,~/.Xresources silent! !xrdb -load % >/dev/null 2>&1
    autocmd BufWritePre,FileWritePre /etc/* if &ft == "dns" |
          \ exe "normal msHmt" |
          \ exe "gl/^\\s*\\d\\+\\s*;\\s*Serial$/normal ^\<C-A>" |
          \ exe "normal g`tztg`s" |
          \ endif
    autocmd BufReadPre *.pdf setlocal binary
    autocmd BufReadCmd *.jar call zip#Browse(expand("<amatch>"))
    autocmd FileReadCmd *.doc execute "read! antiword \"<afile>\""
    autocmd CursorHold,BufWritePost,BufReadPost,BufLeave *
          \ if isdirectory(expand("<amatch>:h")) | let &swapfile = &modified | endif
  augroup END " }}}2

  augroup FTCheck " {{{2
    autocmd!
    autocmd BufNewFile,BufRead */apache2/[ms]*-*/* set ft=apache
    autocmd BufNewFile,BufRead *named.conf*       set ft=named
    autocmd BufNewFile,BufRead *.cl[so],*.bbl     set ft=tex
    autocmd BufNewFile,BufRead /var/www/*.module  set ft=php
    autocmd BufNewFile,BufRead *.vb               set ft=vbnet
    autocmd BufNewFile,BufRead *.CBL,*.COB,*.LIB  set ft=cobol
    autocmd BufNewFile,BufRead /var/www/*
          \ let b:url=expand("<afile>:s?^/var/www/?http://localhost/?")
    autocmd BufNewFile,BufRead /etc/udev/*.rules set ft=udev
    " autocmd BufNewFile,BufRead,StdinReadPost *
    " \ if !did_filetype() && (getline(1) =~ '^!!\@!'
    " \   || getline(2) =~ '^!!\@!' || getline(3) =~ '^!'
    " \   || getline(4) =~ '^!' || getline(5) =~ '^!') |
    " \   setf router |
    " \ endif
    autocmd BufRead * if ! did_filetype() && getline(1)." ".getline(2).
          \ " ".getline(3) =~? '<\%(!DOCTYPE \)\=html\>' | setf html | endif
    autocmd BufNewFile,BufRead *.txt,README,INSTALL,NEWS,TODO if &ft == ""|set ft=text|endif
  augroup END " }}}2
  augroup FTOptions " {{{2
    autocmd!
    autocmd FileType c,cpp,cs,java          setlocal ai et sta sw=4 sts=4 cin
    autocmd FileType sh,csh,tcsh,zsh        setlocal ai et sta sw=4 sts=4
    autocmd FileType tcl,perl,python        setlocal ai et sta sw=4 sts=4
    autocmd FileType markdown,liquid        setlocal ai et sta sw=2 sts=2 tw=72
    autocmd FileType javascript             setlocal ai et sta sw=2 sts=2 ts=2 cin isk+=$
    autocmd FileType php,aspperl,aspvbs,vb  setlocal ai et sta sw=4 sts=4
    autocmd FileType apache,sql,vbnet       setlocal ai et sta sw=4 sts=4
    autocmd FileType tex,css,scss           setlocal ai et sta sw=2 sts=2
    autocmd FileType html,xhtml,wml,cf      setlocal ai et sta sw=2 sts=2
    autocmd FileType xml,xsd,xslt           setlocal ai et sta sw=2 sts=2 ts=2
    autocmd FileType eruby,yaml,ruby        setlocal ai et sta sw=2 sts=2 foldmethod=syntax 
    autocmd FileType cucumber               setlocal ai et sta sw=2 sts=2 ts=2
    autocmd FileType text,txt,mail          setlocal ai com=fb:*,fb:-,n:>
    autocmd FileType sh,zsh,csh,tcsh        inoremap <silent> <buffer> <C-X>! #!/bin/<C-R>=&ft<CR>
    autocmd FileType perl,python,ruby       inoremap <silent> <buffer> <C-X>! #!/usr/bin/<C-R>=&ft<CR>
    autocmd FileType sh,zsh,csh,tcsh,perl,python,ruby imap <buffer> <C-X>& <C-X>!<Esc>o <C-U># $I<C-V>d$<Esc>o <C-U><C-X>^<Esc>o <C-U><C-G>u
    autocmd FileType c,cpp,cs,java,perl,javscript,php,aspperl,tex,css let b:surround_101 = "\r\n}"
    autocmd User     ragtag                 if &sw == 8 | setlocal sw=2 sts=2 ts=2 | endif
    autocmd FileType apache       setlocal commentstring=#\ %s
    autocmd FileType aspvbs,vbnet setlocal comments=sr:'\ -,mb:'\ \ ,el:'\ \ ,:',b:rem formatoptions=crq
    autocmd FileType asp*         runtime! indent/html.vim
    autocmd FileType bst  setlocal ai sta sw=2 sts=2
    autocmd FileType cobol setlocal ai et sta sw=4 sts=4 tw=72 makeprg=cobc\ -x\ -Wall\ %
    autocmd FileType cs   silent! compiler cs | setlocal makeprg=gmcs\ %
    autocmd FileType css  silent! setlocal omnifunc=csscomplete#CompleteCSS
    autocmd FileType cucumber silent! compiler cucumber | setl makeprg=cucumber\ "%:p" | imap <buffer><expr> <Tab> pumvisible() ? "\<C-N>" : (CucumberComplete(1,'') >= 0 ? "\<C-X>\<C-O>" : (getline('.') =~ '\S' ? ' ' : "\<C-I>"))
    autocmd FileType git,gitcommit setlocal foldmethod=syntax foldlevel=1
    autocmd FileType gitcommit setlocal spell
    autocmd FileType gitrebase nnoremap <buffer> S :Cycle<CR>
    autocmd FileType help setlocal ai fo+=2n | silent! setlocal nospell
    autocmd FileType help nnoremap <silent><buffer> q :q<CR>
    autocmd FileType html setlocal iskeyword+=~
    autocmd FileType java silent! compiler javac | setlocal makeprg=javac\ %
    autocmd FileType mail if getline(1) =~ '^[A-Za-z-]*:\|^From ' | exe 'norm gg}' |endif|silent! setlocal spell
    autocmd FileType perl silent! compiler perl
    autocmd FileType pdf  setlocal foldmethod=syntax foldlevel=1
    "    autocmd FileType ruby setlocal tw=79 isfname+=: comments=:#\  " | let &includeexpr = 'tolower(substitute(substitute('.&includeexpr.',"\\(\\u\\+\\)\\(\\u\\l\\)","\\1_\\2","g"),"\\(\\l\\|\\d\\)\\(\\u\\)","\\1_\\2","g"))'
    autocmd FileType ruby
          \ if expand('%') =~# '_test\.rb$' |
          \   compiler rubyunit | setl makeprg=testrb\ \"%:p\" |
          \ elseif expand('%') =~# '_spec\.rb$' |
          \   compiler rspec | setl makeprg=rspec\ \"%:p\" |
          \ else |
          \   compiler ruby | setl makeprg=ruby\ -wc\ \"%:p\" |
          \ endif
    autocmd User Bundler if &makeprg !~ 'bundle' | setl makeprg^=bundle\ exec\  | endif
    autocmd FileType text,txt setlocal tw=78 linebreak nolist
    autocmd FileType tex  silent! compiler tex | setlocal makeprg=latex\ -interaction=nonstopmode\ % formatoptions+=l
    autocmd FileType tex if exists("*IMAP")|
          \ call IMAP('{}','{}',"tex")|
          \ call IMAP('[]','[]',"tex")|
          \ call IMAP('{{','{{',"tex")|
          \ call IMAP('$$','$$',"tex")|
          \ call IMAP('^^','^^',"tex")|
          \ call IMAP('::','::',"tex")|
          \ call IMAP('`/','`/',"tex")|
          \ call IMAP('`"\','`"\',"tex")|
          \ endif
    autocmd FileType vbnet        runtime! indent/vb.vim
    autocmd FileType vim  setlocal ai et sta sw=2 sts=2 keywordprg=:help
    autocmd FileType * if exists("+omnifunc") && &omnifunc == "" | setlocal omnifunc=syntaxcomplete#Complete | endif
    autocmd FileType * if exists("+completefunc") && &completefunc == "" | setlocal completefunc=syntaxcomplete#Complete | endif
  augroup END "}}}2


endif " has("autocmd")

command! -bar Invert :let &background = (&background=="light"?"dark":"light")'
command! -bar Fancy :call Fancy()
command! -bar Run :execute Run()

command! -bar -nargs=1 -complete=file E :exe "edit ".substitute(<q-args>,'\(.*\):\(\d\+\):\=$','+\2 \1','')
command! -bar -nargs=0 SudoW   :setl nomod|silent exe 'write !sudo tee % >/dev/null'|let &mod = v:shell_error
command! -bar -nargs=* -bang W :write<bang> <args>
command! -bar -nargs=0 -bang Scratch :silent edit<bang> \[Scratch]|set buftype=nofile bufhidden=hide noswapfile buflisted
command! -bar -count=0 RFC     :e http://www.ietf.org/rfc/rfc<count>.txt|setl ro noma
command! -bar -nargs=* -bang -complete=file Rename :
      \ let v:errmsg = ""|
      \ saveas<bang> <args>|
      \ if v:errmsg == ""|
      \   call delete(expand("#"))|
      \ endif

" CtrlP ignores
let g:ctrlp_custom_ignore = '\v[\/]\.(git|hg|svn)$'
" let g:ctrlp_custom_ignore = {
"       \ 'dir':  '\v[\/]\.(git|hg|svn)$',
"       \ 'file': '\v\.(exe|so|dll)$',
"       \ 'link': 'some_bad_symbolic_links',
"       \ }
" 

" }}}1

" Section: Helper Functions {{{1
" -------------------------
"

function! SL(function)
  if exists('*'.a:function)
    return call(a:function,[])
  else
    return ''
  endif
endfunction

function! Synname()
  if exists("*synstack")
    return map(synstack(line('.'),col('.')),'synIDattr(v:val,"name")')
  else
    return synIDattr(synID(line('.'),col('.'),1),'name')
  endif
endfunction

function! Fancy()
  if &number
    if has("gui_running")
      let &columns=&columns-12
    endif
    windo set nonumber foldcolumn=0
    if exists("+cursorcolumn")
      set nocursorcolumn nocursorline
    endif
  else
    if has("gui_running")
      let &columns=&columns+12
    endif
    windo set number foldcolumn=4
    if exists("+cursorcolumn")
      set cursorline
    endif
  endif
endfunction

function! Run()
  let old_makeprg = &makeprg
  let old_errorformat = &errorformat
  try
    let cmd = matchstr(getline(1),'^#!\zs[^ ]*')
    if exists('b:run_command')
      exe b:run_command
    elseif cmd != '' && executable(cmd)
      wa
      let &makeprg = matchstr(getline(1),'^#\zs.*').' %'
      make
    elseif &ft == 'mail' || &ft == 'text' || &ft == 'help' || &ft == 'gitcommit'
      setlocal spell!
    elseif exists('b:rails_root') && exists(':Rake')
      wa
      Rake
    elseif &ft == 'cucumber'
      wa
      compiler cucumber
      make %
    elseif &ft == 'ruby'
      wa
      if executable(expand('%:p')) || getline(1) =~ '^#!'
        compiler ruby
        let &makeprg = 'ruby'
        make %
      elseif expand('%:t') =~ '_test\.rb$'
        compiler rubyunit
        let &makeprg = 'ruby'
        make %
      elseif expand('%:t') =~ '_spec\.rb$'
        compiler rspec
        let &makeprg = 'rspec'
        make %
      elseif &makeprg ==# 'bundle'
        make
      elseif executable('pry') && exists('b:rake_root')
        execute '!pry -I"'.b:rake_root.'/lib" -r"%:p"'
      elseif executable('pry')
        !pry -r"%:p"
      else
        !irb -r"%:p"
      endif
    elseif &ft == 'html' || &ft == 'xhtml' || &ft == 'php' || &ft == 'aspvbs' || &ft == 'aspperl'
      wa
      if !exists('b:url'
        call OpenURL(b:url)
      endif
    elseif &ft == 'vim'
      w
      unlet! g:loaded_{expand('%:t:r')}
      return 'source %'
    elseif &ft == 'sql'
      1,$DBExecRangeSQL
    elseif expand('%:e') == 'tex'
      wa
      exe "normal :!rubber -f %:r && xdvi %:r >/dev/null 2>/dev/null &\<CR>"
    elseif &ft == 'dot'
      let &makeprg = 'dotty'
      make %
    else
      wa
      if &makeprg =~ '%'
        make
      else
        make %
      endif
    endif
    return ''
  finally
    let &makeprg = old_makeprg
    let &errorformat = old_errorformat
  endtry
endfunction

function! MoveToPrevTab()
  "there is only one window
  if tabpagenr('$') == 1 && winnr('$') == 1
    return
  endif
  "preparing new window
  let l:tab_nr = tabpagenr('$')
  let l:cur_buf = bufnr('%')
  if tabpagenr() != 1
    close!
    if l:tab_nr == tabpagenr('$')
      tabprev
    endif
    sp
  else
    close!
    exe "0tabnew"
  endif
  "opening current buffer in new window
  exe "b".l:cur_buf
endfunc

function! MoveToNextTab()
  "there is only one window
  if tabpagenr('$') == 1 && winnr('$') == 1
    return
  endif
  "preparing new window
  let l:tab_nr = tabpagenr('$')
  let l:cur_buf = bufnr('%')
  if tabpagenr() < tab_nr
    close!
    if l:tab_nr == tabpagenr('$')
      tabnext
    endif
    sp
  else
    close!
    tabnew
  endif
  "opening current buffer in new window
  exe "b".l:cur_buf
endfunc

" }}}1
