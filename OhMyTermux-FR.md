# OhMyTermux 🧊

**Installation automatisée et personnalisée de [Termux](https://github.com/termux) : packages, shell, plugins, prompts, polices et thèmes sélectionnables.**

#### Installation optionnelle de :
- **[OhMyTermuxXFCE](https://github.com/GiGiDKR/OhMyTermux/edit/main/README-FR.md#-xfce-and-debian-)** : Une distribution proot [Debian](https://www.debian.org/) personnalisée avec un bureau [XFCE](https://www.xfce.org/) et un [App-Installer](https://github.com/GiGiDKR/App-Installer) afin d'obtenir des logiciels non-disponible avec le gestionnaire de paquets.

- **[OhMyTermuxScript](https://github.com/GiGiDKR/OhMyTermuxScript)** : Une collection de scripts exécutables depuis le script principal ou ultérieurement. [^1]

- **[OhMyObsidian](https://github.com/GiGiDKR/OhMyObsidian)** : Synchroniser Obsidian sur Android en utilisant Termux et Git. [^1]

> [!IMPORTANT]
> Ce projet est en développement actif mais pour faciliter la progression, la langue française est privilégiée pour fournir l'interface utilisateur CLI.
> 
> Plusieurs langues seront disponibles dans une version à venir.
> 
> Une version Anglaise de ce texte est [disponible](OhMyTermux.md).

## Installation

> [!TIP]
> **[Gum](https://github.com/charmbracelet/gum)** permet une utilisation simplifiée des scripts CLI comme la sélection multiple avec Espace.
> 
> Il est recommandé de l'utiliser en ajoutant le paramètre `--gum` ou `-g` à la commande.

🧊 Pour installer **OhMyTermux** avec **[Gum](https://github.com/charmbracelet/gum)**

```bash
curl -sL https://raw.githubusercontent.com/GiGiDKR/OhMyTermux/main/install.sh -o install.sh && chmod +x install.sh && ./install.sh --gum
```

Ou sans

```bash
curl -sL https://raw.githubusercontent.com/GiGiDKR/OhMyTermux/main/install.sh -o install.sh && chmod +x install.sh && ./install.sh
```

## À propos de ce programme

🧊 **Packages installés par défaut :**

- [wget](https://github.com/mirror/wget)
- [curl](https://github.com/curl/curl)
- [git](https://github.com/git/git)
- [zsh](https://github.com/zsh-users/zsh)
- [unzip](https://en.m.wikipedia.org/wiki/ZIP_(file_format))

🧊 **Packages sélectionnables individuellement :**

- [nala](https://github.com/volitank/nala)
- [eza](https://github.com/eza-community/eza)
- [lsd](https://github.com/lsd-rs/lsd)
- [logo-ls](https://github.com/Yash-Handa/logo-ls)
- [bat](https://github.com/sharkdp/bat)
- [lf](https://github.com/gokcehan/lf)
- [fzf](https://github.com/junegunn/fzf)
- [glow](https://github.com/charmbracelet/glow)
- [python](https://github.com/python)
- [micro](https://github.com/zyedidia/micro)
- [vim](https://github.com/vim/vim)
- [neovim](https://github.com/neovim/neovim)
- [lazygit](https://github.com/jesseduffield/lazygit)
- [open-ssh](https://www.openssh.com/)

🧊 **Sélection du shell :**

- [Bash](https://git.savannah.gnu.org/cgit/bash.git/)
- [ZSH](https://www.zsh.org/)
- [Fish](https://github.com/fish-shell/fish-shell)

🧊 **Configuration ZSH :**

- [Oh-My-Zsh](https://github.com/ohmyzsh/ohmyzsh)
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- [zsh-completions](https://github.com/zsh-users/zsh-completions)
- [zsh-you-should-use](https://github.com/MichaelAquilina/zsh-you-should-use)
- [zsh-abbr](https://github.com/olets/zsh-abbr)
- [zsh-alias-finder](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/alias-finder)

🧊 **Configuration Fish [^1] :**

- ~~[Oh-My-Fish](https://github.com/oh-my-fish/oh-my-fish)~~
- ~~[Fisher](https://github.com/jorgebucaran/fisher)~~
- ~~[Pure](https://github.com/pure-fish/pure)~~
- ~~[Fishline](https://github.com/0rax/fishline)~~
- ~~[Virtualfish](https://github.com/justinmayer/virtualfish)~~
- ~~[Fish Abbreviation Tips](https://github.com/gazorby/fish-abbreviation-tips)~~
- ~~[Bang-Bang](https://github.com/oh-my-fish/plugin-bang-bang)~~
- ~~[Fish You Should Use](https://github.com/paysonwallach/fish-you-should-use)~~
- ~~[Catppuccin for Fish](https://github.com/catppuccin/fish)~~

🧊 **Configuration de l'affichage Termux :**

- [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts)
- [Color Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes)
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

🧊 **Configuration utile de Termux :**

- Alias personnalisés
- Lien symbolique vers les répertoires utilisateur du stockage interne [^1]

🧊 **Scripts utiles [OhMyTermuxScript](https://github.com/GiGiDKR/OhMyTermuxScript)** [^1] :

- Sélecteur de thèmes
- Installateur de Nerd Fonts
- App-Installer (VSCode, PyCharm, Obsidian...) [^2]
- Bureau XFCE4 natif de Termux sur Termux-X11 [^3]
- Oh-My-Zsh [^2]
- Oh-My-Posh [^1]
- Electron Node.js
- XDRP (Termux natif ou proot-distro)

[^1]: À venir dans la version 1.1 avec l'intégration complète de OhMyTermuxScript
[^2]: Intégration optionnelle dans le script principal
[^3]: En développement (pas encore de date de sortie)

# 🔥 **XFCE et Debian :**

Configure un bureau XFCE et une installation proot Debian.

Cette configuration utilise Termux-X11, le serveur termux-x11 sera installé et vous serez invité à autoriser Termux à installer l'APK.

Vous n'avez qu'à choisir votre nom d'utilisateur et suivre les instructions.

> [!IMPORTANT]
> L'installation nécessite 4 Go

## Démarrer le bureau

Vous recevrez une notification pour autoriser les installations depuis termux, cela ouvrira l'APK pour l'application Android Termux-X11. Bien que vous n'ayez pas besoin d'autoriser les installations depuis termux, vous devrez tout de même l'installer manuellement en utilisant un explorateur de fichiers et en trouvant l'APK dans votre dossier de téléchargements.

Utilisez la commande ```start``` pour initier une session Termux-X11.

Cela démarrera le serveur termux-x11, le bureau XFCE4 et ouvrira l'application Termux-X11 directement sur le bureau.

Pour entrer dans l'installation proot Debian depuis le terminal, utilisez la commande ```debian```

Notez également que vous n'avez pas besoin de définir l'affichage dans le proot Debian car il est déjà configuré. Cela signifie que vous pouvez utiliser le terminal pour démarrer n'importe quelle application GUI et elle se lancera.

## Proot Debian

Pour entrer dans le proot, utilisez la commande ```debian```, à partir de là, vous pouvez installer des logiciels supplémentaires avec apt et utiliser cp2menu dans termux pour copier les éléments de menu dans le menu xfce de termux.

Deux scripts sont également disponibles pour cette configuration :

```prun``` En exécutant cela suivi d'une commande que vous souhaitez exécuter depuis l'installation proot Debian, vous pourrez exécuter des choses depuis le terminal termux sans exécuter ```debian``` pour entrer dans le proot lui-même.

```cp2menu``` En exécutant cela, une fenêtre s'ouvrira vous permettant de copier des fichiers .desktop depuis le proot Debian dans le menu "démarrer" de termux xfce afin que vous n'ayez pas besoin de les lancer depuis le terminal. Un lanceur est disponible dans la section du menu Système.

> [!CAUTION]
> Processus terminé (signal 9) - appuyez sur Entrée
> 
> Installez LADB depuis [Playstore](https://play.google.com/store/apps/details?id=com.draco.ladb) ou depuis [GitHub](https://github.com/hyperio546/ladb-builds/releases).
> 
> Connectez-vous au WIFI.
> 
> En écran partagé, ayez d'un côté LADB et de l'autre les paramètres développeur.
> 
> Dans les paramètres développeur, activez le débogage sans fil puis cliquez dessus pour obtenir le numéro de port, puis cliquez sur appareiller l'appareil pour obtenir le code d'appariement.
> 
> Entrez ces deux valeurs dans LADB.
> 
> Une fois connecté, exécutez cette commande :
> 
> ```adb shell "/system/bin/device_config put activity_manager max_phantom_processes 2147483647"```

## 💻 Historique des versions

- Version 1.0.0 :
  - Téléchargement initial
- Version 1.0.1 :
  - Modifications de l'interface en ligne de commande
  - Installation de [OhMyTermuxScript](https://github.com/GiGiDKR/OhMyTermuxScript) [^1]
- Version 1.0.2 :
  ~~- Intégration de [OhMyObsidian](https://github.com/GiGiDKR/OhMyObsidian)~~ (Retour arrière)
- Version 1.0.3 :
  - Optimisation du système d'alias selon la sélection de paquets et de shell
- Version 1.0.4 :
  - Ajout de paquets sélectionnables à la liste
- Version 1.1 :
  - En développement

## 📖 À faire

- [X] Installation de [OhMyTermuxScript](https://github.com/GiGiDKR/OhMyTermuxScript)
- [ ] Execution de [OhMyTermuxScript](https://github.com/GiGiDKR/OhMyTermuxScript)
- [ ] Intégration de [OhMyObsidian](https://github.com/GiGiDKR/OhMyObsidian)
- [ ] Intégrer la configuration Fish (Plugins, Prompts, Alias)
- [ ] Ajouter plus de packages sélectionnables et de modules Python
- [ ] Intégrer dans le script principal la sélection de thèmes (Schémas de couleurs)
- [ ] Séparer l'installation XFCE / Debian pour exécuter XFCE natif de Termux
- [ ] Ajouter des options pour Debian (Thèmes, Polices, Fonds d'écran)