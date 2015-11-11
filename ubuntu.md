# Ubuntu
Obs: This was tested for Ubuntu 14.04.

### basics & utilities

- [ ] Run ```sudo apt-get update```
- [ ] Install basics ``` sudo apt-get install wget curl vim build-essential htop ```

### zsh and oh-my-zsh
```zsh
sudo apt-get install zsh
sudo chsh -s /usr/bin/zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### git
```zsh
sudo apt-get install git
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
git config --global push.default simple
git config --global credential.helper 'cache --timeout=3600' # desired cache timeout in seconds
git config --global core.editor vim # pick your favorite editor
```

### python
```zsh
sudo apt-get install python-pip python-dev python-setuptools pylint python-software-properties -y
```

### nvm
```zsh
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
vim ~/.zshrc #Add nvm plugin to oh-my-zsh
nvm ls-remote # pick your favorite version
nvm install 0.12.7 # change for your version
nvm use 0.12.7
nvm alias default 0.12.7
```

Interesting packages:
```zsh
npm install -g ember-cli
npm install -g phantomjs2
npm install -g bower
npm install -g jshint
npm install -g grunt-cli
npm install -g gulp-cli
```

##rbenv
Install dependencies:
```zsh
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```
Install from git:
```zsh
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
```
Add rbenv plugin to zsh to make it work smooth:
```zsh
vim ~/.zshrc
```
Add "rbenv" to oh-my-zsh plugin list.

```zsh
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```
~restart terminal~

You check if rbenv is working with ```type rbenv```. Now installing the new version and making it run locally.

```zsh
rbenv install 2.2.3
rbenv global 2.2.3
rbenv local 2.2.3
ruby -v
```

### postgres
```zsh
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.3 libpq-dev
```

Creating first user:
```zsh
sudo -u postgres createuser chris -s

# If you would like to set a password for the user, you can do the following
sudo -u postgres psql
postgres=# \password chris
```

## ImageMagick
```zsh
sudo apt-get install imagemagick --fix-missing
```

## MongoDB
```zsh
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

### Go
```zsh
sudo apt-get install golang
```

### gvm (Go Version Manager)
```zsh
zsh < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
gvm install go1.4
gvm use go1.4
gvm install go1.5  # You'll need a prior version of Go installed in order to bootstrap the installation of Go 1.5+
```

[More Info][gvm_github]

### vim

Install Vundle to manage vim dependencies:
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

Setup ~/.vimrc:
```
" Vundle setup
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'git://github.com/gmarik/Vundle.vim.git'
Plugin 'git://github.com/terryma/vim-multiple-cursors'
Plugin 'git://github.com/itchyny/lightline.vim'
Plugin 'git://github.com/sjl/gundo.vim.git'
Plugin 'git://github.com/kevinw/pyflakes-vim.git'
Plugin 'git://github.com/mxw/vim-jsx.git'
Plugin 'git://github.com/nanotech/jellybeans.vim.git'
call vundle#end()
filetype plugin indent on

" General Settings
colorscheme jellybeans      " JellyBeans colorscheme
set smartcase               " Case insensitive search for lower case characters
set hls                     " Highlight search
set number                  " Show line numbers
set fo=tcq                  " FormatOption - (textwidth, comments, allow gq)
set ts=4                    " TabStop - tab is shown with 4 columns
set sw=4                    " ShiftWidth - 4 space identation
set sts=4                   " SoftTabStop Number of spaces a tab counts
set ai                      " AutoIndenting
set wrapmargin=2            " WrapMargin wraps text before reaching 2 columns away from window border
set ruler                   " Show cursor position (lower left side)
set tildeop                 " ~ behaves like and operator
set expandtab               " Use correct number of spaces on tabbing with > <
set visualbell              " Do not beep (bell) when an error occurs
set shell=/bin/bash         " Which shell will be used on shell command
set showcmd                 " Show commands on the last line
set textwidth=79            " Wrap text in 79 columns
set colorcolumn=79          " Highlight the 79th column
set mouse=n                 " Enables use of the mouse
set incsearch               " Show where a matched pattern is
set title                   " Show file that is been edited
set encoding=utf-8          " Encoding
set termencoding=utf-8      " Terminal encoding
set laststatus=2            " Always display status line
syntax on                   " Enable syntax highlighting
let mapleader=' '           " Set which key is the map leader
set t_Co=256                " Use 256 colors

" Highlight trailling whitespaces
set list listchars=tab:\|_,trail:$
set listchars=tab:>\ ,trail:-,extends:>,precedes:<,nbsp:+
highlight SpecialKey ctermfg=Red ctermbg=Yellow guibg=Yellow
autocmd BufEnter *.diff highlight SpecialKey ctermfg=red ctermbg=red guibg=black
highlight clear SpellBad
highlight link SpellBad ErrorMsg

" Remove trailling whitespaces when saving
autocmd BufWritePre *.* :%s/\s\+$//e

" Makefile (tabs only)
autocmd BufEnter {Makefile,makefile}* set noexpandtab
autocmd BufEnter {Makefile,makefile}* set nolist

" PostgreSQL editor
autocmd BufEnter psql.edit* set syntax=sql
autocmd BufEnter psql.edit* set nolist

" CSS
autocmd BufEnter *.css* set sts=2
autocmd BufEnter *.css* set ts=2
autocmd BufEnter *.css* set sw=2
autocmd BufEnter *.css* set wrap

" LESS
autocmd BufEnter *.less* set syntax=css
autocmd BufEnter *.less* set sts=2
autocmd BufEnter *.less* set ts=2
autocmd BufEnter *.less* set sw=2
autocmd BufEnter *.less* set wrap

" JSON
autocmd BufEnter *.json set sts=2
autocmd BufEnter *.json set ts=2
autocmd BufEnter *.json set sw=2
autocmd BufEnter *.json set wrap

" Javascript
autocmd BufEnter *.js set sts=2
autocmd BufEnter *.js set ts=2
autocmd BufEnter *.js set sw=2
autocmd BufEnter *.js set wrap

" Javascript
autocmd BufEnter *.jsx set sts=2
autocmd BufEnter *.jsx set ts=2
autocmd BufEnter *.jsx set sw=2
autocmd BufEnter *.jsx set wrap

" HTML
autocmd BufEnter *.html* set sts=2
autocmd BufEnter *.html* set ts=2
autocmd BufEnter *.html* set sw=2
autocmd BufEnter *.html* set nowrap

" SHTML
autocmd BufEnter *.shtml* set sts=2
autocmd BufEnter *.shtml* set ts=2
autocmd BufEnter *.shtml* set sw=2
autocmd BufEnter *.shtml* set nowrap

" Handlebars
autocmd BufEnter *.hbs* set syntax=html
autocmd BufEnter *.hbs* set sts=2
autocmd BufEnter *.hbs* set ts=2
autocmd BufEnter *.hbs* set sw=2
autocmd BufEnter *.hbs* set nowrap

" Gundo Mapping
nnoremap <F9> :GundoToggle<CR>

" Enable sudow
cnoremap sudow w !sudo tee % >/dev/null
```
~restart vim~

Install all vim Vundle plugins:
```
:PluginInstall
```

[gvm_github]: https://github.com/moovweb/gvm
