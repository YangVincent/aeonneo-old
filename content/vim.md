---
title: Vim Resources
---

* [Vim Scripting Cheatsheet](https://devhints.io/vimscript)
 
### Maintenance
* `~/.tmux/resurrect` stores the state files for resurrect and continuum
* `~/.vim/views/*` stores the states files for folds -- primarily vim

### Useful debugging tips:
* `:scriptnames` see every relevant file that has been called to reach current state
* `:verbose set background`find what file set a variable
* <a href="http://vi.stackexchange.com/questions/7722/how-to-debug-a-mapping" target="_blank">How to Debug a Mapping!</a>
* <a href="http://stackoverflow.com/questions/3495124/not-reading-vimrc" target="_blank">Finding what set a vim variable</a>
* `rm ~/.vim/view/*</code>` - delete saved view/fold settings (they may change settings).
* `vim --startuptime timecost.txt [file-to-open]` - see times on different aspects of load
* <a href="http://vimcolors.com/621/breezy/dark" target="_blank">Breezy VimColors</a>
* <a href="https://www.cs.swarthmore.edu/help/vim/variables.html" target="_blank">Checking Vim current variable values</a>
* <a href="http://blog.ezyang.com/2010/03/vim-textwidth/" target="_blank">Vim Textwidth</a>

#### Checking what actions are slowing vim down
* `:profile start profile.log`
* `:profile func *`
* At this point, do the slow actions
* <code>:profile pause</code>
* <code>noautocmd qall!</code>
* <a href="http://stackoverflow.com/questions/12213597/how-to-see-which-plugins-are-making-vim-slow" target="_blank">Source</a>
* <a href="http://stackoverflow.com/questions/20988343/alert-developer-tools-access-needs-to-take-control-of-another-process-for-debugg" target="_blank">This</a> helps with solving the developer tools access problem with Conque-GDB
* <a href="http://www.bestofvim.com" target="_blank">Best of Vim</a>

### Plugins
#### Plugin Managers
* Pathogen 
* Vundle - based off of Pathogen, manages installing and local storage, can do *everything* Pathogen can do
* <a href="http://vimawesome.com" target="_blank">Vim Awesome.com</a>
* <a href="https://github.com/vim-airline/vim-airline" target="_blank">Vim Airline</a>

### Folds
* `syntax` for most languages
* `indent` for Python and HTML

### ftplugin
* ftplugin allows you to specify more specific settings per file(type)
* `set` should be `setlocal` in these files, or these edge case settings will "leak" out.
* to force reload `ftplugin/*.vim` files, use `:set filetype={{extension}}`.

