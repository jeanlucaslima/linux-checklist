# Ubuntu
Obs: This was tested for Ubuntu 14.04.

## Summary

- [git](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#git)
- [zsh & oh-my-zsh](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#zsh-and-oh-my-zsh)
- [python](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#python)
- [nvm - node version manager](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#nvm)
- [rbenv](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#rbenv)
- [PostgreSQL](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#postgres)
- [ImageMagick](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#imagemagick)
- [MongoDB](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#mongodb)
- [Golang](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#go)
- [gvm - go version manager](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#gvm-go-version-manager)
- [erlang](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#erlang)
- [elixir](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#elixir)
- [phoenix](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#phoenix-framework)
- [vim](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#vim)

## General
General utilities for to use Ubuntu. 

### basics & utilities
- [ ] Run ```sudo apt-get update```
- [ ] Install basics ``` sudo apt-get install wget curl vim build-essential htop ```

### git
```zsh
sudo apt-get install git
``` 

If you are a developer, these configurations are interesting: 
```zsh
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
git config --global push.default simple
git config --global credential.helper 'cache --timeout=3600' # desired cache timeout in seconds
git config --global core.editor vim # pick your favorite editor
```

### zsh and oh-my-zsh
```zsh
sudo apt-get install zsh
sudo chsh -s /usr/bin/zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
### ImageMagick
```zsh
sudo apt-get install imagemagick --fix-missing
```

TBA: chrome, atom, emacs

## Languages and Development Frameworks

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
npm install -g jshint
npm install -g grunt-cli
npm install -g gulp-cli
```

### ember
```zsh
npm install -g phantomjs2
npm install -g bower
npm install -g ember-cli
```

### rbenv
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

### MongoDB
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

### erlang
```zsh
sudo apt-get update
sudo apt-get install erlang erlang-doc
```

### elixir
```zsh
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && sudo dpkg -i erlang-solutions_1.0_all.deb
sudo apt-get update
sudo apt-get install elixir
```

It is interesting to install Hex. Hex is necessary to get a Phoenix app running (by installing dependencies) and to install any extra dependencies we might need along the way.

```zsh
mix local.hex 
```

### phoenix framework
```zsh
mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.0.3/phoenix_new-1.0.3.ez
```

It is also recommended to install ```inotify-tools```, that is a C library that acts as filesystem watcher, thus helping with live reloading. To install:

```zsh
sudo apt-get install inotify-tools
```

You may want to check more info about Phoenix framework install here: http://www.phoenixframework.org/docs/installation

### vim
Install Vundle to manage vim dependencies:
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

There are many ways to set up your own ```~/.vimrc``` file, [click here](https://github.com/jeanleonino/dotfiles/blob/master/.vimrc) to check mine. 

If you use that configuration file, just follow these instructions right after:

Inside vim, install all vim Vundle plugins:
```
:PluginInstall
```

~restart vim~

[gvm_github]: https://github.com/moovweb/gvm
