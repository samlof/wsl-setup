## Setup for WSL with zsh and theme

# 1. Install WSL
https://docs.microsoft.com/en-us/windows/wsl/install-win10

Turn on hardware virtualization from bios if not turned on

Turn on needed Windows features
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
Restart

Download and install Linux kernel https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

Setup wsl2 `wsl --set-default-version 2`
Install Ubuntu from Microsoft Store

# 2. Setup Windows Terminal
Install from Microsoft store
Options and setup WSL as default

Jetbrains mono font from https://www.jetbrains.com/lp/mono/
Color theme Atom One dark to json file
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
    "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
    "hidden": false,
    "name": "Ubuntu",
    "source": "Windows.Terminal.Wsl",
    "fontFace": "JetBrains Mono",
    "colorScheme": "Atom One Dark",
},
```
In Windows Terminal Settings UI change starting directory with help of `explorer.exe .` in a wsl shell and change it as default profile
# 2. Install zsh
Install required programs and setup git autocrlf
```sh
sudo apt update
sudo apt install git zsh -y
git config --global core.autocrlf input

sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Change `~/.zshrc` theme to be "agnoster"
Change the prompt to be nicer `vi ~/.oh-my-zsh/themes/agnoster.zsh-theme` and line 92 to 
```
prompt_segment green black "%(!.%{%F{yellow}%}.)%n"
```
# 3. Install dev tools
Nodejs
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
nvm install --lts
```