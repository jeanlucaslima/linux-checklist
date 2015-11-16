# Fedora

### Make sure system is up-to-date

- [ ] Run ```sudo dnf update```

### git
```zsh
sudo dnf install git
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
git config --global push.default simple
git config --global credential.helper 'cache --timeout=3600' # desired cache timeout in seconds
git config --global core.editor vim # pick your favorite editor
```

###
