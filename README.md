Question1:  
How to set ycm with c-family languages (YouCompleteMe)?  
of course it support python language, donnot worry  

Question2:  
How to add longlist (command: ll) to pdb for python2.7?  
 
Question1 solution:  
Reference: github.com/Valloric/YouCompleteMe#ubuntu-linux-x64  
  
Preparation:  
linux system,  
Vim is at least 7.4.1578  
cmake  
python2, python3  
  
  
Preface:  
If you feel it too complicated and trivial to compile a ycm binary with support for c-family languages, the following introduction may be the quickest way, otherwise to fetch the newest version, or just want to have a try, you could skip to step 1. Or to be a pure adventurer, please visit the official website https://github.com/Valloric/YouCompleteMe  
  
Instruction:  
  Just extract the prepared_ycm_llvm_6.0.0.tar.gz(download at https://pan.baidu.com/s/1KYOb1zmWHiLY4QruL_jqMQ key: 2pmn) into ~/.vim/bundle, optionally, partly, copy my .vimrc and .ycm_extra_conf.py if you like into ~ and your program root dir respectively, all done!  
  
Being here shows you are ready to comiple your own ycm, good.  
1.  
  
In your ~/.vimrc(if you donot have one, create one):  
  Assuming that you are using Vundle to manage your vim plug-ins  
  between "call vundle#begin()" and "call vundle#end()", insert:  
    Plugin 'Valloric/YouCompleteMe'  
  save and exit  
  
2.  
  
command in terminal:  
  vim  
  :PluginInstall  
  :q  
      
now, a dir called "YouCompleteMe" will be in your ~/.vim/bundle/  
  
update on 1.11.2018<br/>
when finishing the first two steps above, there is an alternative for the rest steps:<br/>
3a.<br/> 
cd ~/.vim/bundle/YouCompleteMe<br/>
./install.py --clangd-completer<br/> (note that before we used --clang-completer)
and do step 4...

3b.  
Download the upmost version of llvm pre-built binaries for clang at:  
http://releases.llvm.org/download.html  
then, extract it to whatever path you like (/path/to/clang), with "lib, bin, include etc." inside this path.  
  
command in terminal:  
  cd /path/to/another/dir   
  mkdir ycm_build  
  cd ycm_build  
  cmake -G "Unix Makefiles" -DPATH_TO_LLVM_ROOT=/path/to/clang . ~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp  
  cmake --build . --target ycm_core --config Release  
  (optional:)  
  cd ..  
  rm ycm_build -rf  
  rm /path/to/clang -rf  
  
4.  
Edit ~/.vimrc, insert the configuration about ycm:  
  
  " YouCompleteMe  

  set runtimepath+=~/.vim/bundle/YouCompleteMe  

  let g:ycm_collect_identifiers_from_tags_files = 1           " 开启 YCM 基于标签引擎  
  let g:ycm_collect_identifiers_from_comments_and_strings = 0 " 注释与字符串中的内容不用于补全  
  let g:syntastic_ignore_files=[".*\.py$"]  
  let g:ycm_seed_identifiers_with_syntax = 1                  " 语法关键字补全  
  let g:ycm_complete_in_comments = 1  
  let g:ycm_confirm_extra_conf = 0  
  let g:ycm_key_list_select_completion = ['<c-n>', '<Down>']  " 映射按键, 没有这个会拦截掉tab, 导致其他插件的tab不能用.  
  let g:ycm_key_list_previous_completion = ['<c-p>', '<Up>']  
  let g:ycm_complete_in_comments = 1                          " 在注释输入中也能补全  
  let g:ycm_complete_in_strings = 1                           " 在字符串输入中也能补全  
  let g:ycm_collect_identifiers_from_comments_and_strings = 0 " 注释和字符串中的文字不会被收入补全  
  " let g:ycm_global_ycm_extra_conf='~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm/.ycm_extra_conf.py'  
  let g:ycm_show_diagnostics_ui = 0                           " 禁用语法检查  
  let g:ycm_server_python_interpreter = 'python2'  
  let g:ycm_python_binary_path = 'python'  
  " let g:ycm_min_num_of_chars_for_completion=1                 " 从第1个键入字符就开始罗列匹配项  
  let g:ycm_show_diagnostics_ui = 1  
  inoremap <expr> <CR> pumvisible() ? "\<C-y>" : "\<CR>" |            " 回车即选中当前项  
  nnoremap <c-j> :YcmCompleter GoToDefinition<CR>    " 跳转到定义处  
  nnoremap <c-k> :YcmCompleter GoToDeclaration<CR>    " 跳转到声明处  
     
Edit or create your .ycm_extra_conf.py or just use mine, add it into your program root dir  
  
That all the whistles and bells, enjoy it!  

Question2 solution:  
replace pdb.py in python2's lib with this pdb.py<br/>  


