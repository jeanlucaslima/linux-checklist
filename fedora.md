# Fedora

### Ensure system is up-to-date
```zsh
sudo dnf update```

### Install and configure git
```zsh
sudo dnf install git
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
git config --global push.default simple
git config --global credential.helper 'cache --timeout=3600' # desired cache timeout in seconds
git config --global core.editor vim # pick your favorite editor
```

### Install RPM Fusion repositories
1. Go to http://rpmfusion.org/Configuration
2. Download free + nonfree repos for matching Fedora version number
3. Click on them, and click install when it opens "Software" application

### Install Gnome Tweak Tool
```sudo dnf install gnome-tweak-tool```

### Install Fedy
```bash -c 'su -c "curl http://folkswithhats.org/fedy-installer -o fedy-installer && chmod +x fedy-installer && ./fedy-installer"'```
