# GROOVY AND GRAILS

## Install in Windows

Donwload framework grails from [URL](https://grails.org/download.html)
Unzip file in Directory Grails
Redirect from the IDE to the grails folder

## Install in MacOSX

### The Software Development Kit Manager
SDKMAN permite manejar GRAILS en sus distintas versiones, anteriormente era conocido como GVM

Install sdkman

```
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk version
```

Uninstall sdkman

```
tar zcvf ~/sdkman-backup_$(date +%F-%kh%M).tar.gz -C ~/ .sdkman
$ rm -rf ~/.sdkman
```

### Install GRAILS

List of available grails versions

```
sdk list grails
sdk current grails
```

Install the current version grails

```
sdk install grails
grails --version

```

Install an specific version grails

```
sdk install grails 2.3.8
grails --version

```

To activate a version of grails you have installed, simply call

```
sdk use grails 3.2.10
grails --version
```
### Uninstall Grails

Remove an installed version.

```
sdk uninstall grails 3.2.10
sdk list grails
```

### List of packages installed with sdk

```
sdk current
```




