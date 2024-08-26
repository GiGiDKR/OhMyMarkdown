# **Collection of Markdown files synced to Obsidian (Android) with a Termux script**

## How to sync Obsidian with Git on Android

### Setup

- Install [Termux – Apps on Google Play](https://play.google.com/store/apps/details?id=com.termux&hl=en_GB&gl=US)
- Open Termux, run `termux-change-repo`. Press the ↓ button and press spacebar to tick all repositories, then press enter to move to the next screen
- Press ↓, then spacebar to tick the "Mirrors hosted by Albatross", press enter
- Run `pkg install git -y`
- Run `termux-setup-storage`
- Run `cd storage/shared` (If you get permissions issues, refer to [this page](https://wiki.termux.com/wiki/Termux-setup-storage))
- Run `git config --global credential.helper store`
- Run `git config --global user.email "<your_email>"`
- Run `git config --global user.name "<The name you want on your commits>"`
- Run `git config --global pull.rebase true`
- Run `git clone <your repository>` and enter your login when prompted. You may need to create a [personal access token](https://github.com/settings/tokens) if you're using GitHub.
- Install and open [Obsidian](https://play.google.com/store/apps/details?id=md.obsidian&hl=en_GB&gl=US)
- Click "Open folder as vault", click on your phone name at the top to navigate to the top directory, and click on your git repository name. Then click "use this folder"
- With this setup so far, you will need to manually go into the folder in Termux and type `git pull`. If you'd like to create shortcuts to do this on your homescreen, see [this guide](https://renerocks.ai/blog/obsidian-encrypted-github-android/#shortcuts-for-committing-pushing-and-pulling)

### To enable auto-syncing

- Run `pkg install cronie termux-services`
- Restart Termux by typing `exit`.
- Run `sv-enable crond`
- Run `crontab -e` and enter `*/30 * * * * ~/sync_repo.sh` (This syncs every 30 minutes)
- Click the CTRL button, and type `x`. Type `y` and enter.
- Type `nano sync_repo.sh` and enter:

```bash
#!/bin/bash
cd ~/storage/shared/<your repository name>
git add .
git commit -m "Android Sync $(date)"
git pull
git push
```

(This is a very basic sync and will not handle things like merge conflicts)

- Click the CTRL button, and type `x`. Type `y` and enter.
- Run `chmod +x sync_repo.sh`
- Test your script by running it like so `./sync_repo.sh`

Assuming Android doesn't kill the background service, it will now sync automatically.

## Use with Termux Widget and have a desktop shortcut 
- In Termux type :
```
mkdir ~/.shortcuts
cp sync_repo.sh ~/.shortcuts
```
Add widget on Android desktop, select Termux Widget then one of the two available (a list of shortcuts available in the directory or a selection of one of the shortcuts).

## Limitations

- If Termux is closed in the background by Android, the cron service will stop updating your repository and you must open Termux again. Refer to instructions for your device model to disable the killing of certain background applications.
- This may negatively affect your devices battery life.

