命令模式下的快捷键:

* `:copen` 打开Quickfix窗口
* `:cclose` 关闭Quickfix窗口
* `:cn` 跳到下一个Error的所在行
* `:cp` 调到上一个Error的所在行

常用设置:

```
nnoremap <leader>q :call QuickfixToggle()<cr>

let g:quickfix_is_open = 0

function! QuickfixToggle()
    if g:quickfix_is_open
        cclose
        let g:quickfix_is_open = 0
    else
        copen
        let g:quickfix_is_open = 1
    endif
endfunction

nnoremap <leader>cn :cn<cr>
nnoremap <leader>cp :cp<cp>
```