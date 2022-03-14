# Setup for WSL with zsh and theme

![Image of Terminal](https://i.imgur.com/UzIgi6t.png)

1. [Install WSL](#1-install-wsl)
2. [Setup Windows Terminal](#2-setup-windows-terminal)
3. [Oh My Zsh](#3-install-oh-my-zsh)
4. [Install dev tools](#4-install-dev-tools)

# 1. Install WSL

https://docs.microsoft.com/en-us/windows/wsl/install-win10

Turn on hardware virtualization from bios if not turned on

Turn on needed Windows features. Run following in administrator Powershell

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Restart pc

Download and install Linux kernel https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

Setup wsl2 `wsl --set-default-version 2`

Install Ubuntu from Microsoft Store

# 2. Setup Windows Terminal

Install Windows Terminal from Microsoft Store

Install Jetbrains mono font from https://www.jetbrains.com/lp/mono/

Color theme Atom One dark to json file. Open json file from Windows Terminal settings.

```json
{
  "name": "Atom One Dark",
  "background": "#282C34",
  "black": "#000000",
  "blue": "#61AFEF",
  "brightBlack": "#5C6370",
  "brightBlue": "#61AFEF",
  "brightCyan": "#56B6C2",
  "brightGreen": "#98C379",
  "brightPurple": "#C678DD",
  "brightRed": "#E06C75",
  "brightWhite": "#FFFFFF",
  "brightYellow": "#D19A66",
  "cursorColor": "#FFFFFF",
  "cyan": "#56B6C2",
  "foreground": "#CCCCCC",
  "green": "#98C379",
  "purple": "#C678DD",
  "red": "#E06C75",
  "selectionBackground": "#FFFFFF",
  "white": "#ABB2BF",
  "yellow": "#D19A66"
}
```

Change font, color scheme for wsl config

```json
{
    "guid": "<your guid>",
    "hidden": false,
    "name": "Ubuntu",
    "source": "Windows.Terminal.Wsl",
    "fontFace": "JetBrains Mono",
    "colorScheme": "Atom One Dark",
},
```

In Windows Terminal Settings UI change startup profile to wsl and wsl starting directory with help of `explorer.exe .` in a wsl shell and change it as default profile

# 3. Install Oh My Zsh

Install git zsh and ohmyzsh

```sh
sudo apt update
sudo apt install git zsh -y

sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Change `~/.zshrc` theme to be "agnoster"

Change the prompt to be nicer `vi ~/.oh-my-zsh/themes/agnoster.zsh-theme` and line 92 to

```sh
prompt_segment green black "%(!.%{%F{yellow}%}.)%n"
```

### Zsh plugins

Syntax highlight

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/zsh-syntax-highlighting
```

Auto suggestions

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
```

Then edit `~/.zshrc`

```sh
plugins=(
    git
    npm
    z
)
# Source files for cloned plugins
source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh

```

# 4. Install dev tools

Nodejs with nvm

```sh
curl -o- "https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh" | bash
nvm install --lts
```

Setup git autocrlf

```sh
git config --global core.autocrlf input
```

Java, build-essential, python-as-python3, ffmpeg

```sh
sudo apt update
sudo apt install ffmpeg build-essential python-is-python3 default-jre
```

### Docker. No need since using through Docker Desktop for Windows. Have to enable from that one

```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
# Should print 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88

# Run rest after confirming fingerprint
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo service docker start
```
