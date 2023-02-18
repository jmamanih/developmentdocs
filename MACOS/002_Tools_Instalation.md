# MAC OS X Tools Instalation

## Install iTerm

Download iterm from url
https://www.iterm2.com/downloads.html


## Install Homebrew
xcode preinstall

```
xcode-select --install

```
install homebrew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew -v
```

After installing and as suggested in the command line, to check for any issues with the install run:

```
brew doctor
```

To search for an application:

```
brew search
```

To install
```
brew install <application-name>
```

To list all apps installed by Homebrew

```
brew list
```

To remove an installed application

```
brew remove <application-name>
```

To see what else you can do

```
man brew
```

## Custom terminal
[Install Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)


```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

```
brew doctor
```

```
echo 'export PATH="/usr/local/sbin:$PATH"' >> ~/.zrc
```

```
brew doctor
```

```
brew prune
```

close terminal

## Install tmux
Terminal multiplexer

```
brew install tmux
tmux
exit
```

## Install Git

```
brew install git

```

### Git ssh

Error:

```
Enter passphrase for key '/Users/juanfer/.ssh/id_rsa':
```

Solution:

```
ssh-add ~/.ssh/id_rsa
```

# How to Stop DS_Store File Creation on Network Volumes in Mac OS X

Delete .DS_Store files

```
cd project_folder

rm -rf `find . -type f -name .DS_Store`

```

To enable this setting

```
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
sudo shutdown -r now

```

To reset this setting to the default value

```
defaults delete com.apple.desktopservices DSDontWriteNetworkStores
sudo shutdown -r now

```

# Postman

Authentication Token jwt

Open Postman

Headers:

Content-Type        application/json
Authorization       Bearer eyJ0eXAiOiJKV1QiLCJhb ....

                    -> Get Bearer token: Open navigate chrome, F12,
                                        Application, Storage, Local Storage, Key xxx_token, copy Value

# Delete files from the trash or recycle

```
Enter windows and delete hidden file .trash
```
