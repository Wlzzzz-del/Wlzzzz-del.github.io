---
title: 我的vim配置
date: 2020-10-18 08:51:49
tags: 工作
---
当你用过一次配置好的vim，你一辈子都不会想用ide编程
```
set t_co=256
set encoding=utf-8
set directory=.,$TEMP
let &t_ut=""
"修改缩进距离
set tabstop=2
"首个退格键返回上一行
set backspace=indent,eol,start

let &t_SI="\<Esc>]50;CursorShape=1\x7"
let &t_SR="\<Esc>]50;CursorShape=2\x7"
let &t_EI="\<Esc>]50;CursorShape=0\x7"

"vim下次打开返回上次编辑的位置
au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! G'\"" | endif


"leader键映射为空格
let mapleader=" "
syntax on
set number
set relativenumber
set cursorline
set wrap
set showcmd
set wildmenu
set ignorecase
set hlsearch
set incsearch
set smartcase
exec "nohlsearch"
noremap = nzz
noremap - Nzz
noremap j h
noremap k j
noremap i k
noremap n i
noremap N I
noremap I 5k
noremap K 5j
noremap J 5h
noremap L 5l
noremap <LEADER><CR> :nohlsearch<CR>
map S :w!<CR>
map s <nop>
map Q :q<CR>
"设置向右分屏
map sl :set splitright<CR>:vsplit<CR>
"设置向左分屏
map sj :set nosplitright<CR>:vsplit<CR>
"设置向上分屏
map si :set nosplitbelow<CR>:split<CR>
"设置向下分屏
map sk :set splitbelow<CR>:split<CR>
"刷新vimrc
map R :source $MYVIMRC<CR>
"分屏方向
map <LEADER>l <C-w>l
map <LEADER>i <C-w>k
map <LEADER>j <C-w>h
map <LEADER>k <C-w>j

"打开标签页
map tu :tabe<CR>
map tj :-tabnext<CR>
map tl :+tabnext<CR>


"切换分屏
map sv <C-w>t<C-w>H
map sh <C-w>t<C-w>K

"set paste
map <LEADER>sp :set paste<CR>
"markdownpreview
map md :MarkdownPreview<CR>


"方向键改为修改分屏大小
map <up> :res +5<CR>
map <down> :res -5<CR>
map <left> :vertical resize-5<CR>
map <right> :vertical resize+5<CR>
"插件
call plug#begin('~/.vim/plugged')
"状态栏
Plug 'vim-airline/vim-airline'
"主题
Plug 'connorholyday/vim-snazzy'
Plug 'arcticicestudio/nord-vim'
"选中的行高亮
Plug 'itchyny/lightline.vim'
"目录树导航
Plug 'scrooloose/nerdtree',{ 'on':'NERDTreeToggle'}
Plug 'Xuyuanp/nerdtree-git-plugin'
"python自动补全
"Plug 'davidhalter/jedi-vim'
"Plug 'klen/python-mode'
"可视化缩进
"Plug 'nathanaelkane/vim-indent-guides'
"括号匹配高亮
"Plug 'kien/rainbow_parentheses.vim'
" 标签导航
Plug 'majutsushi/tagbar',{ 'on': 'TagbarOpenAutoClose'}
" 错误检查
Plug 'W0rp/ale'
"自动补全
Plug 'Valloric/YouCompleteMe'
" Undo Tree
"Plug 'mbbill/undotree/'
" 其他的视觉增强
Plug 'nathanaelkane/vim-indent-guides'
" Git
Plug 'rhysd/conflict-marker.vim'
Plug 'tpope/vim-fugitive'
Plug 'mhinz/vim-signify'
Plug 'gisphm/vim-gitignore', { 'for': ['gitignore', 'vim-plug'] }
" HTML, CSS, JavaScript, PHP, JSON, etc.
Plug 'elzr/vim-json'
Plug 'hail2u/vim-css3-syntax'
Plug 'spf13/PIV', { 'for' :['php', 'vim-plug'] }
Plug 'gko/vim-coloresque', { 'for': ['vim-plug', 'php', 'html','javascript', 'css', 'less'] }
Plug 'pangloss/vim-javascript', { 'for' :['javascript', 'vim-plug'] }
Plug 'mattn/emmet-vim'
"
" " Python
Plug 'vim-scripts/indentpython.vim'
"
" " Markdown
"Plug 'iamcco/markdown-preview.nvim', { 'do': { -> mkdp#util#install_sync()}, 'for' :['markdown', 'vim-plug'] }
Plug 'iamcco/markdown-preview.nvim', {'do': 'cd app && yarn install' }
Plug 'dhruvasagar/vim-table-mode', { 'on': 'TableModeToggle' }
Plug 'vimwiki/vimwiki'
"
" " Bookmarks
Plug 'kshenoy/vim-signature'
"
" " Other useful utilities
Plug 'terryma/vim-multiple-cursors'
Plug 'junegunn/goyo.vim' " distraction free writing mode
Plug 'tpope/vim-surround' " type ysks' to wrap the word with '' or type cs'`
" to change 'word' to `word`
Plug 'godlygeek/tabular' " type ;Tabularize /= to align the =
Plug 'gcmt/wildfire.vim' " in Visual mode, type i' to select all text in '',
" or type i) i] i} ip
Plug 'scrooloose/nerdcommenter' " in <space>cc to comment a line
"
" " Dependencies
Plug 'MarcWeber/vim-addon-mw-utils'
Plug 'kana/vim-textobj-user'
Plug 'fadein/vim-FIGlet'
Plug 'vim-scripts/ctags.vim'
" 静态代码分析
"Plug 'scrooloose/syntastic'
" 文件搜索
"Plug 'kien/ctrlp.vim'

call plug#end()


colorscheme nord
let g:lightline={
\'colorscheme':'nord',
\}
"NERDTree
map tt :NERDTreeToggle<CR>
let NERDTreeMapOpenExpl = ""
let NERDTreeMapUpdir = ""
let NERDTreeMapUpdirKeepOpen = ""
let NERDTreeMapOpenSplit = ""
let NERDTreeOpenVSplit = ""
let NERDTreeMapActivateNode = "p"
let NERDTreeMapOpenInTab = "o"
let NERDTreeMapPreview = ""
let NERDTreeMapCloseDir = "n"
let NERDTreeMapChangeRoot = "y"
"
"
" " ==
" " == NERDTree-git
" " ==
let g:NERDTreeIndicatorMapCustom = {
     \ "Modified"  : "✹",
         \ "Staged"    : "✚",
             \ "Untracked" : "✭",
                 \ "Renamed"   : "➜",
                     \ "Unmerged"  : "═",
                         \ "Deleted"   : "✖",
                             \ "Dirty"     : "✗",
                                 \ "Clean"     : "✔︎",
                                     \ "Unknown"   : "?"
                                         \ }
"
"
"                                         " ===
"                                         " === You Complete ME
"                                         " ===
nnoremap gd :YcmCompleter GoToDefinitionElseDeclaration<CR>
nnoremap g/ :YcmCompleter GetDoc<CR>
nnoremap gt :YcmCompleter GetType<CR>
nnoremap gr :YcmCompleter GoToReferences<CR>
let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'
let g:ycm_confirm_extra_conf= 0 
let g:ycm_autoclose_preview_window_after_completion=0
let g:ycm_autoclose_preview_window_after_insertion=1
let g:ycm_use_clangd = 0
let g:ycm_python_interpreter_path = "/usr/lib/python3.8"
let g:ycm_python_binary_path = "/usr/bin/python3.8"


" ===
" === ale
" ===
let b:ale_linters = ['pylint']
let b:ale_fixers = ['autopep8','yapf']


" ===
" === Taglist
" ===
"map <silent> T:TagbarOpenAutoClose<CR>


" ===
" === MarkdownPreview
" ===
let g:mkdp_auto_start = 0
let g:mkdp_auto_close = 1
let g:mkdp_refresh_slow = 0
let g:mkdp_command_for_global = 0
let g:mkdp_open_to_the_world = 0
let g:mkdp_open_ip = ''
let g:mkdp_browser = 'firefox'
let g:mkdp_echo_preview_url = 0
let g:mkdp_browserfunc = ''
let g:mkdp_preview_options = {
    \ 'mkit': {},
    \ 'katex': {},
    \ 'uml': {},
    \ 'maid': {},
    \'disable_sync_scroll':0,
    \'sync_scroll_type':'middle',
    \'hide_yaml_meta':1
		\ }
let g:mkdp_markdown_css = ''
let g:mkdp_highlight_css = ''
let g:mkdp_port = ''
let g:mkdp_page_title = '「${name}」'


"===
"===
"vim-table-mode
"===
map <LEADER>tm :TableModeToggle<CR>

"===
"===
"Python-syntax
"====
let g:python_highlight_all = 1
let g:python_slow_sync = 0
"===
"=== vim-indent-guide
"===
let g:indent_guides_guide_size = 1
let g:indent_guides_start_level = 2
let g:indent_guides_enable_on_vim_startup = 1
let g:indent_guides_color_change_percent = 1
silent! unmap <LEADER>ig
autocmd WinEnter * silent! unmap <LEADER>ig


"===
"===Goyo
"===
map <LEADER>gy :Goyo<CR>


"===
"===vim-signiture
"===
let g:SignatureMap= {
        \'Leader':"m",
        \'PlaceNextMark': "m,",
        \'ToggleMarkAtLine':"m.",
        \'PurgeMarksAtLine':"dm-",
        \'DeleteMark':"dm",
        \'PurgeMarks':"dm/",
        \'PurgeMarkers':"dm?",
				\'GotoNextLineAlpha':"m<LEADER>",
        \'GotoPrevLineAlpha': "",
       \ 'GotoNextSpotAlpha'  :  "m<LEADER>",
       \ 'GotoPrevSpotAlpha'  :  "",
       \ 'GotoNextLineByPos'  :  "",
       \ 'GotoPrevLineByPos'  :  "",
       \ 'GotoNextSpotByPos'  :  "mn",
       \ 'GotoPrevSpotByPos'  :  "mp",
       \ 'GotoNextMarker'     :  "",
       \ 'GotoPrevMarker'     :  "",
       \ 'GotoNextMarkerAny'  :  "",
       \ 'GotoPrevMarkerAny'  :  "",
       \ 'ListLocalMarks'     :  "m/",
       \ 'ListLocalMarkers'   :  "m?"
       \ }


 "===
 " === Undotree
 " ===
 let g:undotree_DiffAutoOpen = 0
" map L :UndotreeToggle<CR>

" pythonmode
"let g:pymode_paths = ["/usr/lib/python3.8"]
"let g:pymode_python = "python3"
"c-run

map <F5> : call CompileRunGcc()<CR>
func! CompileRunGcc()
	exec "w"
	if &filetype == 'c'
		exec "!g++ % -o %<"
		exec "!time ./%<"
	elseif &filetype == 'cpp'
		exec "!g++ % -o %<"
		exec "!time ./%<"
	elseif &filetype == 'java' 
		exec "!javac %" 
		exec "!time java %<"
	elseif &filetype == 'sh'
		:!time bash %
	elseif &filetype == 'python'
		exec "!time python2.7 %"
    elseif &filetype == 'html'
        exec "!firefox % &"
    elseif &filetype == 'go'
        exec "!go build %<"
        exec "!time go run %"
    elseif &filetype == 'mkd'
        exec "!~/.vim/markdown.pl % > %.html &"
        exec "!firefox %.html &"
	endif
endfunc
```
