
# Linux

## Search File Content Recursively

```shell
grep -rin "foo" .
find . -type f | xargs grep -in "PSQLException"
```

## More on `find`

To remove multiple files such as *.jpg or *.sh with one command find, use

```shell
find . -name "FILE-TO-FIND"-exec rm -rf {} \;
# or
find . -type f -name "FILE-TO-FIND" -exec rm -f {} \;
```

The only difference between above two syntax is that first command can remove directories as well where second command only removes files.

More Examples of find command

```shell
# Find all files having .bak (*.bak) extension in current directory and remove them:
find . -type f -name "*.bak" -exec rm -f {} \;

# Find all core files and remove them:
find / -name core -exec rm -f {} \;

# Find all *.bak files in current directory and removes them with confirmation from user:
find . -type f -name "*.bak" -exec rm -i {} \;

# Find string in files
find . | xargs grep 'string' -sl

# List directories containing executables
find . -name "*.exe" | grep -o '.*/' | sort | uniq
```

## Create symbolic links (symlink)

```shell
ln -s [source] [target{optional}]
ln -s <directory> <name>
ln -s /var/log/error.log /tmp/log.log
```

## Download files (wget)

Download a single file:

``` shell
wget http://...
wget ftp://...
wget -O output.file <url>
```

Use `wget` with password protected sites:

``` shell
wget --http-user=vivek --http-password=Secret <url>
wget http://username:password@host.acme.com/path/to/file.tar.gz
```

Use URLs from file:

```shell
wget -i /tmp/download.txt
```

## Network stats (netstat)

```shell
netstat -tulpen
netstat -taupen

# or
sudo lsof -n -iTCP:[PORT] | grep LISTEN
```

## List processes (ps)

```shell
ps aux | less
ps aux | grep ...
```

## Using mail

```shell
# Sending simple text
echo "This is my text" | mail -s "This is a subject" mwurster@hp.com

# Sending small file content
mail -s "mail with file content" mwurster@hp.com < /path/to/file.txt
```

### Extract tr.gz. file

To extract one or more members from an archive, enter:

```shell
tar -zxvf {file.tar.gz}
```

## Force DHCP to renew IP address

```shell
sudo dhclient -r
sudo dhclient
```

## Edit sudoers file

The `/etc/sudoers` file can only be edited with `visudo`.
You can set an alternative text editor:

```shell
sudo update-alternatives --config editor
```

Now open the `sudoers` file:

```shell
sudo visudo -f /etc/sudoers
```

In example, put `michael ALL=(ALL) NOPASSWD:ALL` at the end of the file in order to allow user `michael` to execute `sudo` commands without a password.

## Use sudo w/o entering a password

`vi /etc/sudoers`

For a single user:

```
superuser ALL=(ALL) NOPASSWD:ALL
```

For a group:

```
%supergroup ALL=(ALL) NOPASSWD:ALL
```

## Generate directory tree structure

```shell
find . -type d | sed -e "s/[^-][^\/]*\//  |/g" -e "s/|\([^ ]\)/|-\1/" > tree.txt
```

## ISO Mount

```shell
mkdir /mnt/isofile
mount -o loop -t iso9660 <file>.iso /mnt/isofile
umount /mnt/isofile
```

## Mount Windows Share

`smbfs` package must be installed.

```shell
mount -t cifs -o username=wurstmic,workgroup=emea //veno.deu.hp.com/d_drive$ /mnt/veno/
mount -t cifs -o username=share,workgroup=veno //veno.deu.hp.com/public /mnt/veno/
mount -t cifs -o username=administrator,workgroup=ia3 //ia3.mambo.net/c$ /mnt/ia3
```

## Red Hat Package Management

```shell
rpm -qa
rpm -qa | grep <package>
```

## [RHEL] Disable SELinux

Go to `/etc/selinux/config` and set `SELINUX` to `disabled`

## [RHEL] Disable IPv6

Append below lines in `/etc/sysctl.conf`:

```shell
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

To make the settings affective, execute `sysctl -p`

## Proxy Setup

`/etc/profile.d/10-proxy.sh`

``` 
proxy=http://web-proxy.bbn.hpecorp.net:8088

export http_proxy=$proxy
export https_proxy=$proxy
export ftp_proxy=$proxy

export HTTP_PROXY=$proxy
export HTTPS_PROXY=$proxy
export FTP_PROXY=$proxy

export HTTP_PROXY_REQUEST_FULLURI=false
export HTTPS_PROXY_REQUEST_FULLURI=false
```

`/etc/apt/apt.conf.d/95proxy`

```
Acquire::http::proxy "http://web-proxy.bbn.hpecorp.net:8088";
Acquire::https::proxy "http://web-proxy.bbn.hpecorp.net:8088";
Acquire::ftp::proxy "http://web-proxy.bbn.hpecorp.net:8088";
```

Node.js/npm proxy settings:

`npm config set proxy http://proxy.company.com:8080`
`npm config set https-proxy http://proxy.company.com:8080`

Composer proxy settings:

Use HTTP_PROXY variable in front of your command call:

```
HTTP_PROXY=<proxy> php composer.phar self-update
```
