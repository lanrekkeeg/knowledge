
# Ubuntu

## Common Packages to Install

```shell
sudo add-apt-repository --yes ppa:webupd8team/java
sudo add-apt-repository --yes ppa:webupd8team/atom
sudo add-apt-repository --yes ppa:webupd8team/sublime-text-3
sudo apt-get update

sudo apt-get install git curl vim build-essential meld sublime-text atom \
  oracle-java7-installer dropbox ruby-full python-pip rhc
sudo apt-get install apache2 libapache2-mod-php5 php5 php5-mysql mysql-server \
  php5-cli php-apc php5-intl php5-xdebug phpmyadmin php5-curl phpunit mysql-workbench

sudo a2enmod rewrite
sudo mkdir -p /var/run/apache2
sudo chown -R www-data /var/run/apache2
```

## Chrome Browser

```shell
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list'
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```

## Install Source Code Pro Font

> <https://github.com/adobe-fonts/source-code-pro>

**Local Installation:**

```shell
mkdir -p ~/.fonts/scp
cp SourceCodePro-*.otf ~/.fonts/scp
fc-cache -f -v
```

**System-wide Installation:**

```shell
sudo mkdir -p /usr/share/fonts/opentype/scp
sudo cp SourceCodePro-*.otf /usr/share/fonts/opentype/scp
fc-cache -f -v
```

## Install GNOME Extensions

> Go to <https://extensions.gnome.org> and use Firefox to install it.

* Simple Dock
* Sound Output Device Chooser

## Install LaTeX

```shell
sudo apt-get install texlive-full
```

## Install Ubuntu Themes

```shell
sudo add-apt-repository --yes ppa:noobslab/themes
sudo add-apt-repository --yes ppa:ravefinity-project/ppa
sudo apt-get update
sudo apt-get install ceti-theme vibrancy-colors
```

## Install Linux Kernel Headers

```shell
sudo apt-get install linux-headers-$(uname -r)
```

## Install .deb file on Ubuntu

```shell
sudo dpkg -i DEB_PACKAGE
```

If the package got some dependencies:

```shell
sudo apt-get update
sudo apt-get install -f
sudo dpkg -i DEB_PACKAGE
```
