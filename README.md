# OhMyMarkdown 🔖
**A collection of Markdown files synchronized from Obsidian on Android with Termux.**

**My project [OhMyObsidian](https://github.com/GiGiDKR/OhMyObsidian) is an adaptation of [Obsidian-Android-Sync](https://github.com/DovieW/obsidian-android-sync) by [Dovie Weinstock](https://github.com/DovieW).**
> [!TIP]
> If you use it you can clone this repository into "Obsidian" directory :
> 
> ```bash
> cd $OBSIDIAN_DIR_PATH
> git clone https://github.com/GiGiDKR/OhMyMarkdown.git
> ```

## OhMyObsidian 📑

> [!NOTE]
> [French version of README.md](https://github.com/GiGiDKR/OhMyObsidian/blob/main/README-FR.md)

Easily sync your [Obsidian](https://github.com/obsidianmd/obsidian-releases) vaults on Android using Git (SSH) + [Termux](https://github.com/termux/termux-app).
Automation and shortcuts using [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.tasker) which works whether a vault is open or not to synchronize it. [^1]

To prevent conflicts, add the following lines to your **.gitignore** file in all your vaults that you'll be syncing using Git. If you notice a plugin has a file which is often in conflict, you'll want to add that as well (remember to un-track it with **`git rm --cached <file>`**):
```gitignore
/.obsidian/workspace.json
/.obsidian/workspace-mobile.json
/.obsidian/plugins/obsidian-git/data.json
/conflict-files-obsidian-git.md
```
To stop conflicts from happening with your note files, you can create a **.gitattributes** file in the root of your vaults with the following content. It will basically always accept both changes for **`.md`** files.
```gitattributes
*.md merge=union
```

### Termux setup
1. Install [F-Droid](https://f-droid.org/en/) or [Obtainium](https://github.com/ImranR98/Obtainium)
2. Install Termux from [F-Droid](https://f-droid.org/en/packages/com.termux/) or [Obtainium](https://github.com/termux/termux-app)

### Obsidian sync setup

> [!IMPORTANT]
> A full installation script is available ~~with optional use of [gum](https://github.com/charmbracelet/gum) to get a cleaner and beautiful scripting interface~~.
> To run it enter:
> ```bash
> curl -o $HOME/install.sh https://raw.githubusercontent.com/GiGiDKR/OhMyObsidian/main/install.sh && chmod +x $HOME/install.sh && $HOME/install.sh
> ```
> ~~🎀 Add `--gum` or `-g` at the end of the command to use the [gum](https://github.com/charmbracelet/gum) interface~~

#### Manual installation  

- **Optional** : To install / update packages you can select a particular repository to increase the speed of download : `termux-change-repo`

1. Run the following commands :
```bash
termux-setup-storage
```
```bash
pkg update && pkg upgrade -y && pkg install -y git openssh termux-api
```
```bash
mkdir -p /storage/emulated/0/Documents/Repository $HOME/OhMyObsidian
```
```bash
git clone https://github.com/GiGiDKR/OhMyObsidian.git ~/storage/shared/Documents/Repository/OhMyObsidian
```
> [!WARNING]
> Be aware that the next step will set [safe.directory](https://git-scm.com/docs/git-config/2.35.2#Documentation/git-config.txt-safedirectory) to '*'
   
2. Run the setup script :
```bash
cp "/storage/emulated/0/Documents/Repository/OhMyObsidian/setup" ~/OhMyObsidian/ && chmod +x "$HOME/OhMyObsidian/setup" && source "$HOME/OhMyObsidian/setup"
```
3. The above command copied an SSH public key to your clipboard (or was displayed to the screen), paste this into your Git host's SSH key authentication setting (eg [Github](https://github.com/settings/keys)). If you want to copy the SSH key again, run the **`setup`** script again.

4. In Termux, you should now be in the Obsidian directory (verify with **`pwd`**) where you can clone your Obsidian vaults. Try not to put any special characters in your vault name.

- Obsidian documentation in Markdown format is available in the [GitHub repository](https://github.com/obsidianmd/obsidian-help/tree/master/en).

> [!NOTE]
> - Sync all the vaults in Obsidian folder :
> **`sync`**
> - Get the status of the vault sync :
> **`status`** 
> - Open Obsidian from Termux : 
> **`open`**

> [!TIP]
> By default Git does not remember your credentials but it is possible to change this with a Credential Helper :
>
> Remember your credentials during a session :
> ```bash
> git config --global credential.helper cache
> ```
> Remember during 1 hour :
> ```bash
> git config --global credential.helper 'cache --timeout=3600'
> ```
> Remember permanently (less secure) :
> ```bash
> git config --global credential.helper store
> ```

## Tasker Setup [^1]


[Here's an image](https://bit.ly/40hLIyt) of what it looks like, once complete with shortcuts to some optional utility functions. Each vault will have it's own icon. This allows syncing to be more efficient as without it, all vaults will sync each time in a specific order. Instead of just the vault that you open being synced immediately. If you only use one vault or don't mind the inefficiency of waiting for the vault that you just opened to be updated, then you can use the default Obsidian app icon. Also, all vaults are synced once a day (defaults to 4am).

1. Install [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.tasker) from the Play Store.
2. Install [F-Droid](https://f-droid.org/en/).
3. Install [Termux:Tasker](https://f-droid.org/en/packages/com.termux.tasker/) and [Termux:API](https://f-droid.org/en/packages/com.termux.api/) from F-Droid or install from Obtainium : [Termux:Tasker](https://github.com/termux/termux-tasker) / [Termux:API](https://github.com/termux/termux-api))
2. Enable the Termux permission in the Android settings of the Tasker app.
3. Open the Obsidian app and add your vaults from the **`Obsidian`** folder.
4. If you're using the Obsidian Git plugin, you should disable it for this device. You can do this in the plugin settings.
5. Import the "Tasker project" into Tasker. Once you import it, I recommend you rearrange the tasks based on [this image](https://imgur.com/a/6Gj6aRj) for simplicity (to rearrange tasks, hold on a task, then drag). You can import the project in 2 ways. You can use this [TaskerNet link](https://taskernet.com/shares/?user=AS35m8n3cQwLQVpqM%2Fik6LZsANJ%2F8SkOXbatTM3JXxEQY4KYaxES06TbTgTRcO7ziHKZXfzQKT1B&id=Project%3AObsidian+Syncing), or you can import ([image](https://imgur.com/a/Fvyl8HF)) the .xml file from this repository. Once it's imported, there will be some prompts, I think one for giving Tasker "Usage Access" and one to enable all profiles. Accept all.
6. **Vault launch icons** - There are 2 example tasks (Vault1 and Vault2). Rename the task to the name of your vault (you can name it anything). Then in the task, you'll see a "Variable Set" action, change the value to the **name of the folder** which contains the repository for that vault.
7. Give Termux the "Display over other apps" permission.
8. Add the Vault launch icons as Tasker widgets (use the widget type that allows you to add them to folders) to the home screen. Also, add the 3 helper tasks as widgets (as needed): 
   1. Sync Vaults   - syncs all vaults
   2. Vaults Status - outputs the **`git fetch && git status`** of each vault
   3. Sync Log      - outputs the sync log.

All vaults will sync at 4am every day using a Tasker profile.

[^1]: Do not use for now : adaptation to come in v1.1

### Notes
- You should get a notification if a sync fails. This requires AutoNotification from the PlayStore. To disable this, disable the Sync Error Notification profile.
- The individual vault icons to open specific vaults can be a bit slow. I've tried different ways to open a vault. Faster ways had one of two problems. Either it would open the vault correctly, but then if you left the app, it would not appear in the recents list. Or, it would load the app, load the last vault used, then load the vault you wanted which ends up being slower then the current method. You can find almost all the methods I tried in the Open Vault task (they are disabled).
- If you prefer, you can have a popup menu (a scene or list dialog for example), to combine all the actions or vaults into one icon on your home screen.
- If this repository has new commits that you want, running the **`setup`** command should pull them down. After which, you may be prompted to run a command to update the setup script itself, if it was updated.

### Version history
- 1.0 : Initial version (adapted from [Obsidian-Android-Sync](https://github.com/DovieW/obsidian-android-sync))
- 1.0.1 : Added zsh-friendly configuration
- 1.0.2 : French translation 
- 1.0.3 : Added a automated [script](https://raw.githubusercontent.com/GiGiDKR/OhMyObsidian/main/install.sh)
- **1.1** : In development 
   -    [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.tasker) integration
   -    [Gum](https://github.com/charmbracelet/gum) integration
