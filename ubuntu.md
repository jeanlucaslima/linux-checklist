# Ubuntu
Obs: This was tested for Ubuntu 14.04.

## Summary
- [Tips](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#tips)
  - [Backing up and restoring packages and settings](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#how-to-backup-and-restore-settings-and-list-of-installed-packages)
- [General](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#general)
  - [basics and utilities](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#basics--utilities)
  - [htop](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#htop)
  - [git](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#git)
  - [zsh & oh-my-zsh](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#zsh-and-oh-my-zsh)
  - [docker](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#docker)
  - [Watchman](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#watchman)
- [Languages and Development Frameworks](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#languages-and-development-frameworks)
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
- [Editors and IDEs](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#editors-and-ides)
  - [vim](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#vim)
  - [Sublime Text 3](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#sublime-text-3-64-bits)
  - [Atom](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#atom)

## Tips

### How to backup and restore settings and list of installed packages
Backup
```sh
dpkg --get-selections > ~/Package.list
sudo cp -R /etc/apt/sources.list* ~/
sudo apt-key exportall > ~/Repo.keys
rsync --progress /home/`whoami` /path/to/user/profile/backup/here
```
Restore
```sh
rsync --progress /path/to/user/profile/backup/here /home/`whoami`
sudo apt-key add ~/Repo.keys
sudo cp -R ~/sources.list* /etc/apt/
sudo apt-get update
sudo apt-get install dselect
sudo dpkg --set-selections < ~/Package.list
sudo dselect
```

[Source](http://askubuntu.com/a/99151).

Thanks [@EnLabWalt](https://github.com/EnLabWalt) for the tip.

## General
General utilities for to use Ubuntu. 

### basics & utilities
First steps and general update:

- Run ```sudo apt-get update```
- Install basics ``` sudo apt-get install wget curl build-essential ```
- Install applications to deal with general files like zip, tar, rar:``` sudo apt-get install unace unrar zip unzip p7zip-full p7zip-rar sharutils rar uudeview mpack arj cabextract file-roller ``` 
- Laptop tools to save battery and some tweaks ``` sudo apt-get install laptop-mode-tools ``` 

### Unity Tweak Tool
![Screenshot Unity Tweak Tool](http://screenshots.ubuntu.com/screenshots/u/unity-tweak-tool/10014_large.png)

It can be installed from the Ubuntu Software Center, by searching “Unity tweak tool” and install it. Or you can [click here](https://apps.ubuntu.com/cat/applications/unity-tweak-tool/).

### htop
htop is an interactive process viewer for Linux. It is much more friendly than top.

![Screenshot htop](http://hisham.hm/htop/htop_graph.gif)

```sh
sudo apt-get install htop
```

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

To effectively change the terminal shell, you have to go to the menu Edit -> Profiles -> choose default -> click Edit button -> on new window go to tab "Title and Command" and add "/usr/bin/zsh" to "Run a custom command", example:

![Screenshot ZSH](http://i.imgur.com/y5hvbKC.png)

You can see my zsh file ```~/.zshrc``` [clicking here](https://github.com/jeanleonino/dotfiles/blob/master/.zshrc).

### ImageMagick
```zsh
sudo apt-get install imagemagick --fix-missing -y
```

### Gimp
GIMP is an image manipulation software, alternative to Photoshop and handful for editions. 
```sh
sudo apt-get install gimp gimp-data gimp-plugin-registry gimp-data-extras
```

### Google Chrome
Check [this](http://www.tecmint.com/install-google-chrome-in-debian-ubuntu-linux-mint/) tutorial.

### docker
Installation
```sh
sudo apt-get install linux-image-extra-`uname -r`
sudo apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | sudo tee /etc/apt/sources.list.d/docker.list
sudo apt-get update
sudo apt-get install docker-engine
```

Enable forwarding with the Uncomplicated Firewall (defafult):
```sh
sudo nano /etc/default/ufw # or other editor
```
And replace ```DEFAULT_FORWARD_POLICY="DROP"``` with ```DEFAULT_FORWARD_POLICY="ACCEPT"``` and restart the firewall:
```sh
sudo ufw reload
```

More instructions available on [Docker website](https://docs.docker.com/engine/installation/ubuntulinux/).
Consider adding the docker plugin to oh-my-zsh.


### Watchman
Facebook Watchman exists to watch files and record when they change. It can also trigger actions (such as rebuilding assets) 
when matching files change.

Pre-requisites
```sh
sudo apt-get install autoconf autotools-dev
```

Installation
```sh
git clone https://github.com/facebook/watchman.git ~/.local/
cd ~/.local/watchman
git checkout v4.1.0  # the latest stable release
./autogen.sh
./configure
make
sudo make install
```

### PhantomJS
```sh
git clone --recurse-submodules git://github.com/ariya/phantomjs.git ~/.local/
cd ~/.local/phantomjs 
./build.py
```

Warning: this may take **several** minutes. In my case, took 50 minutes. 


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
nvm install 5.3.0 # change for your version
nvm use v5.3.0
nvm alias default v5.3.0
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
rbenv install 2.2.4
rbenv global 2.2.4
rbenv local 2.2.4
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

## Editors and IDEs
Some common editors for developers.

### vim
Install vim
```sh
sudo apt-get install vim
```
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

### Sublime Text 3 64 bits

Manually

```sh
wget http://c758482.r82.cf2.rackcdn.com/sublime-text_build-3083_amd64.deb ~/ # or check link at http://www.sublimetext.com/3
sudo dpkg -i sublime-text_build-3083_amd64.deb 
```

Through Package Manager

```sh
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer
```

Install Package Control
Check [packagecontrol.io](https://packagecontrol.io/installation)

### Atom

Manual

```sh
wget https://atom.io/download/deb
sudo dpkg -i atom-amd64.deb
```

From Source

Dependencies include at Node.js, [click here to install if you don't have](https://github.com/jeanleonino/linux-checklist/blob/master/ubuntu.md#nvm), also install:

```sh
sudo apt-get install build-essential git libgnome-keyring-dev fakeroot
```

Installing

```sh
# clone the repository
git clone https://github.com/atom/atom
cd atom
# checkout the latest release
git fetch -p
git checkout $(git describe --tags `git rev-list --tags --max-count=1`)
# building Atom
script/build
# installing to /usr/local/bin
sudo script/grunt install
```

If you have more questions on how to build Atom from source, check [the Atom official guide](https://github.com/atom/atom/blob/master/docs/build-instructions/linux.md). 


[gvm_github]: https://github.com/moovweb/gvm
