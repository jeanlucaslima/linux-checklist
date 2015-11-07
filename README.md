# Fresh New Linux install

### basics & utilities

Set terminal profile preferences:

* The end command restarts console
* color scheme / background

```
sudo apt-get update
sudo apt-get install wget curl vim build-essential git htop
```

### zsh
```
sudo apt-get install zsh
sudo chsh -s /usr/bin/zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### git
```
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
git config --global push.default simple
git config --global credential.helper 'cache --timeout=3600' # desired cache timeout in seconds
```

### python
```
sudo apt-get python-pip python-dev python-setuptools pylint python-software-properties -y
```

### nvm
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
Add nvm plugin to oh-my-zsh
nvm ls-remote # pick your favorite version
ñvm install 0.12.7 # change for your version
nvm use 0.12.7
nvm alias default 0.12.7
```

Interesting packages:
```
npm install -g ember-cli
npm install -g phantomjs2
npm install -g bower
npm install -g jshint
npm install -g grunt-cli
npm install -g gulp-cli
```

#rbenv
Install dependencies:
```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```

```
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
```
Add rbenv plugin to zsh to make it work smooth:
```
vim ~/.zshrc
```
Add "rbenv" to oh-my-zsh plugin list. TODO: create setion how to install plugin

```
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```
~restart terminal~

You check if rbenv is working with ```type rbenv```. Now installing the new version and making it run locally.

```
rbenv install 2.2.3
rbenv global 2.2.3
rbenv local 2.2.3
ruby -v
```

### postgres
```
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.3 libpq-dev
```

Creating first user:
```
sudo -u postgres createuser chris -s

# If you would like to set a password for the user, you can do the following
sudo -u postgres psql
postgres=# \password chris
```

## Contributing
Just send a PR :-)

## Authors

* @jeanleonino