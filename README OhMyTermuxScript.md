# OhMyTermuxScript 🧊
**A collection of scripts for [Termux](https://github.com/termux/termux-app).**

> [!WARNING]
> This program is in Alpha version (see [Update log](https://github.com/GiGiDKR/OhMyTermuxScript/edit/main/README.md#update-log) for more information.

&nbsp;

### 🧊 Complete installation 

> [!IMPORTANT]
> To use a beautiful command line script execution interface, [gum](https://github.com/charmbracelet/gum) can be used with `-g` or `--gum` parameter added to the execution command. 

- From a clean install of Termux, paste the following code 
```bash
pkg update -y && pkg install git -y
git clone https://github.com/GiGiDKR/OhMyTermuxScript.git
cd OhMyTermuxScript && chmod +x ./*.sh
```
- Type `ls` to display the list of scripts, then type
```bash
./script_name.sh 
```

&nbsp;

### 🧊 Run a specific script 

- [Electron](https://github.com/electron/electron) Node.js
```bash
curl -sL https://raw.githubusercontent.com/GiGiDKR/OhMyTermuxScript/main/electron.sh -o electron.sh && chmod +x electron.sh && ./electron.sh --gum
```

- Create [Symbolic Link](https://en.wikipedia.org/wiki/Symbolic_link) to external user directories
```bash
curl -sL https://raw.githubusercontent.com/GiGiDKR/OhMyTermuxScript/main/usersymlink.sh -o usersymlink.sh && chmod +x usersymlink.sh && ./usersymlink.sh --gum
```

## 🧊 Additional parameters
- Uninstall
```bash
./script_name.sh -u
./script_name.sh --uninstall
```
- Using [gum](https://github.com/charmbracelet/gum) to magnify the command line interface
```bash
./script_name.sh -g
./script_name.sh --gum
```
> [!TIP]
> These settings can be combined.

## 💻 Update log
- Version 0.1.0 : Initial upload
- Version 0.2.0 : [OhMyTermux](https://github.com/GiGiDKR/OhMyTermux) integration

## ⏺️ To do
- [X] Integrate the ability to use [gum](https://github.com/charmbracelet/gum) into scripts
- [X] Integrate uninstallation with a run command parameter  
- [ ] Update README.md to include script-specific commands
- [ ] Upload other scripts after testing

