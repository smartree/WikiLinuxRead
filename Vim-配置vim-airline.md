`vim-airline`是一个强化`vim`状态栏的插件，配置方法如下：

* 安装`vim-airline/fonts`字体，否则状态栏不会正常显示`>>`箭头（乱码）
* 安装`vim-airline`和`vim-airline/vim-airline-themes`插件，如果使用 Vundle 插件管理工具，直接添加`Bundle XX`即可
* 添加下面配置到`.vimrc`:
```vim
"" airline settings.
let g:airline_theme = 'simple'
let g:airline_powerline_fonts = 1

if !exists('g:airline_symbols')
  let g:airline_symbols = {}
endif

let g:airline_left_sep = ''
let g:airline_left_alt_sep = ''
let g:airline_right_sep = ''
let g:airline_right_alt_sep = ''
let g:airline_symbols.branch = ''
let g:airline_symbols.readonly = ''
let g:airline_symbols.linenr = ''
let g:airline#extensions#tabline#enabled = 1
```
   * 重启 vim会发现状态栏发生变化，但是箭头有可能不对齐，没有一个统一的解决方法([powerline/fonts#31](https://github.com/powerline/fonts/issues/31))。在 Mac (iterm2)机器上，箭头就没有对齐，解决方法：在 Iterm2设置`Non-ASCII`字体：在尝试了所有Powerline 字体，`13pt Meslo LG L DZ regular for Powerline`效果是最满意的。

还可以在`.vimrc`设置如下快捷键，控制`split panel`:

```vim
" panel navigators
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>

" map keys for vertical/horizontal split panel
nnoremap <leader>vs <C-w>v
nnoremap <leader>hs <C-w>s

" map keys for resize vertical/horizontal window:
nnoremap <silent> + :exe "resize " . (winheight(0) * 4/3)<CR>
nnoremap <silent> _ :exe "resize " . (winheight(0) * 3/4)<CR>
nnoremap <silent> > :exe "vertical resize " . (winwidth(0) * 4/3)<CR>
nnoremap <silent> < :exe "vertical resize " . (winwidth(0) * 3/4)<CR>
```