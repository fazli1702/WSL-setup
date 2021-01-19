# WSL setup

This is a manual for me on how to setup wsl and use zsh and p10k

reference: https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10  
video reference: https://www.youtube.com/watch?v=su0h5StEZ6A&t=431s

## WSL installation

Run powershell as admin and run the following command  

### Step 1: Enable WSL

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

### Step 2: Enable 'Virtual Machine Platform'

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### Step 3: Set WSL2 as default
```
wsl --set-default-version 2
```

Restart your machine.

The setup is now done.

Install linux distros on microsoft store.
Once donwload is done, run the following on powershell
```
wsl --list --verbose 
```
Your linux disrubition should be displayed on screen similar to the following
```
  NAME            STATE           VERSION
* Ubuntu-20.04    Running         2
  kali-linux      Stopped         2
```

## Setup ZSH with OhMyZSH and powerlevel10k

## Install zsh
Run the following on your wsl terminal
```
sudo apt install zsh
```

Change default shell to zsh
```
chsh -s $(which zsh)
```

Restart your terminal

To verify your shell, enter the following
```
echo $SHELL
```
The output should display `/usr/bin/zsh`

## Install Oh My Zsh
https://github.com/ohmyzsh/ohmyzsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Install powerlevel10k
https://github.com/romkatv/powerlevel10k#oh-my-zsh
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`

## Install Fonts
Install any fonts from nerdfonts https://www.nerdfonts.com/  
I installed FiraCode Nerd Font  
Add `POWERLEVEL9K_MODE="nerdfont-complete"` in `~/.zshrc` below `ZSH_THEME`  

To add the font in windows terminal, add in `settings.json` in the profile
```
"fontFace": FiraCode Nerd Font
```

## Install plugins

### zsh-syntax-highlighting
https://github.com/zsh-users/zsh-syntax-highlighting

install by running the following command
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```
enable syntax highlighting on shell
```
source ./zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

### zsh-autosuggestions 
https://github.com/zsh-users/zsh-autosuggestions

install by running the following command
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):
```
plugins=(git zsh-autosuggestions)
```

Enable plugin
```
source ~/.zshrc
```

## Configure
Run `p10k configure` to configure the shell.