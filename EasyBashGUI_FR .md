EasyBashGUI - documentation
===========================

Façon simplifiée de coder des dialogues d'interface graphique en bash ! - Documentation

- [Modes d'utilisation](#modes-dutilisation)
- [Installation](#installation)
    - [Utilisation rapide](#utilisation-rapide)
    - [Utilisation rapide pour développeurs](#utilisation-rapide-pour-développeurs)
- [Cadre EBG](#cadre-ebg)
    - [Exemples](#exemples)
- [Référence EBG](#référence-ebg)
    - [Notes](#notes)

## Modes d'utilisation

Vous pouvez l'utiliser comme module système ou comme module intégré pour un démarrage rapide !

## Installation

Veuillez consulter le document [install.md](install.md) pour toute méthode d'installation,
ou consultez simplement la section suivante pour une utilisation plus facile et modulaire :

#### Utilisation rapide

Supposons que vous ayez installé EBG sur le système, alors il n'y a que quelques étapes :

```bash
mkdir ~/Devel/newprj && cd ~/Devel/newprj

echo -e "source easybashgui\nmessage hola" > ~/Devel/easybashgui/newprogram

bash ~/Devel/easybashgui/newprogram
```

C'est tout !!!!! Facile ! Mais que faire si vous voulez tout intégré !? Sans installation ? 
Bien sûr, vous pouvez ! Consultez la section suivante :

#### Utilisation rapide pour développeurs

Mais que faire si nous voulons tout dans notre projet, en tant que développeurs ou 
en intégrant l'EBG ?, pour rendre notre programme indépendant de l'installation :

```bash
mkdir ~/Devel && cd ~/Devel && git clone https://github.com/BashGui/easybashgui

cd ~/Devel/easybashgui

ln -s lib/easybashlib easybashlib && ln -s lib/easybashgui.lib easybashgui.lib

echo -e "source src/easybashgui\nmessage hola" > ~/Devel/easybashgui/newprogram

bash ~/Devel/easybashgui/newprogram
```

C'est tout !!!!! Vous avez développé votre premier script GUI !

## Cadre EBG

EBG est entièrement modulaire, vous créez un nouveau script et vous sourcez simplement le point d'entrée :

* `easybashgui` un lanceur qui sera le point d'entrée sourcé dans vos scripts
* `easybashgui-debug` qui active certaines options de débogage gérées par le composant précédent
* `easybashgui.lib` qui gère les backends, appelé bibliothèque de widgets
* `easydialog-legacy` autonome pour créer des boîtes de dialogue externes (comme autrefois)
* `easybashlib` utilisé pour des fonctions optionnelles comme le nettoyage du répertoire de travail temporaire

- Documentation de l'index
    - [Le script EBG](#le-script-ebg)
    - [Support des widgets backend](#support-des-widgets-backend)
    - [Le supermode pour le widget backend](#le-supermode-pour-le-widget-backend)
    - [Utilisation système vs utilisation module utilisateur](#utilisation-système-vs-utilisation-module-utilisateur)
    - [Priorité des boîtes backend](#priorité-des-boîtes-backend)
    - [Mode fenêtre des boîtes](#mode-fenêtre-des-boîtes)
    - [Taille des fenêtres des boîtes](#taille-des-fenêtres-des-boîtes)
    - [Compatibilité du comportement des boîtes](#compatibilité-du-comportement-des-boîtes)
- [Exemples](#exemples)
    - [Boîtes de questions simples](#boîtes-de-questions-simples)
    - [Boîte de texte simple à partir de l'entrée standard](#boîte-de-texte-simple-à-partir-de-lentrée-standard)
    - [L'attente de réponse](#lattente-de-réponse)
    - [Sélection de répertoire simple](#sélection-de-répertoire-simple)
    - [Exemples d'entrée triplet](#exemples-dentrée-triplet)
    - [Barre de progression](#barre-de-progression)
    - [Jauge de niveau](#jauge-de-niveau)
    - [Sélection de menu](#sélection-de-menu)
    - [Choisir des éléments](#choisir-des-éléments)
    - [Un exemple plus complexe](#un-exemple-plus-complexe)
    - [Un exemple de notification](#un-exemple-de-notification)
- [Référence EBG](#référence-ebg)
    - [Flux](#flux)
    - [message](#message)
    - [ok_message](#ok_message)
    - [alert_message](#alert_message)
    - [question](#question)
    - [text](#text)
    - [wait_seconds (barre de progression)](#wait_seconds-barre-de-progression)
    - [progress (manière progressive)](#progress-manière-progressive)
    - [progress (manière régressive)](#progress-manière-régressive)
    - [wait_for](#wait_for)
    - [terminate_wait_for](#terminate_wait_for)
    - [fselect](#fselect)
    - [dselect](#dselect)
    - [input](#input)
    - [menu](#menu)
    - [tagged_menu](#tagged_menu)
    - [list](#list)
    - [adjust](#adjust)
    - [notify_message](#notify_message)
    - [notify_change](#notify_change)
    - [notify](#notify)
- [Notes](#notes)

#### Le script EBG

Le script qui implémentera l'EBG est toujours structuré en trois parties principales :

1. La variable `supermode` optionnelle et le point d'entrée sourcé obligatoire
2. Le code source que vous avez écrit qui doit être en langage `bash`
3. La phrase `clean_temp` optionnelle pour le mode utilisateur uniquement

```bash
#!/bin/bash
# partie 1 variables d'environnement et point d'entrée
export supermode="zenity"
export supertitle="Hola script v.0.0.1"
export supericon="system"
export supercontext="windows" #ou supercontext="terminal" (voir ci-dessous)
source /path/easybashgui #ou simplement : "source easybashgui" si vous l'avez installé ! ;)
#
# partie 2 .. code ici
message "hola"
#
# partie 3 les phrases finales ou la manipulation de sortie
echo $?
clean_temp
```

L'exemple le plus simple d'un script EBG est :

```bash
source ./easybashgui

message "hola"
```

#### Support des widgets backend

EBG implémente différentes boîtes de dialogue ! Vous n'avez pas à vous soucier de l'environnement dans lequel vous exécutez le script, car **EasyBashGUI** gérera cela de manière transparente, en fonction de la disponibilité des backends de widgets (frontends).

* Mode console (supercontext="terminal") :
  * gum
  * dialog
  * whiptail (non sélectionnable, juste en cas de repli)
* Mode graphique (supercontext="windows") :
  * yad
  * gtkdialog
  * kdialog
  * zenity
  * Xdialog

S'il n'y a pas de support dialog/cdialog installé. Consultez la section suivante sur `supermode` !

#### Le supermode pour le widget backend

Les backends pour les frontends (les widgets à utiliser pour afficher les boîtes) sont sélectionnables 
par la variable d'environnement `supermode`.

La variable d'environnement `supermode` est uniquement utilisée pour forcer ou sélectionner manuellement 
un widget spécifique, par exemple en utilisant `kdialog` sous un bureau GTK, ou par exemple 
en utilisant `zenity` sous un environnement KDE. 

Il n'y a pas de mode `whiptail` car il est utilisé uniquement en cas de repli ! lorsque dialog/cdialog 
est manquant, si whiptail est présent, utilisez simplement `supermode=dialog` pour !

#### Utilisation système vs utilisation module utilisateur

Si EBG n'est pas installé, vous devez avoir au moins tous les fichiers dans le même chemin
que votre script principal, si vous l'installez sur le système, vous n'avez pas à vous soucier
de cela !

Un programme/projet qui implémente EBG et n'utilise pas le même chemin que le script principal, 
peut placer le script et les fichiers EBG dans un autre chemin, mais la structure doit être dans la même 
[hiérarchie indiquée dans le guide d'installation section "Chemins d'installation".](install.md#install-paths) 

La méthode UTILISATEUR doit avoir le chemin complet vers le point d'entrée ou les fichiers doivent être dans le
même chemin que le script que vous avez créé :

```bash
#!/bin/bash
source ./easybashgui
# .. code ici
clean_temp
```

La méthode SYSTÈME a juste besoin du point d'entrée sans chemin et les fichiers doivent être dans les chemins système, le script que vous avez créé devrait ressembler à :

```bash
#!/bin/bash
source easybashgui
# .. code ici
```

La différence entre les modes est juste deux : d'abord vous avez noté que le point d'entrée source n'a pas de chemin (dans le mode UTILISATEUR c'est "`./`") et deuxièmement le mode SYSTÈME n'a pas besoin de nettoyer les fichiers temporaires (dans le mode UTILISATEUR c'est `clean_temp`).

Si easybashlib est présent et chargé avec succès, vous pouvez éviter la dernière phrase de `clean_temp` pour supprimer les fichiers temporaires ; sinon N'OUBLIEZ PAS d'écrire `clean_temp` à la fin de tous vos scripts... ;-)

#### Priorité des boîtes backend

Le support EBG pour les boîtes de dialogue backend dépend des programmes en cours d'exécution :

1. Si tous les backends requis sont disponibles ou au moins kdialog l'est.. l'EBG
   essaiera de vérifier si kdebin est en cours d'exécution et n'utilisera que kdialog.
2. Si seuls les basés sur GTK sont en cours d'exécution, l'EBG utilisera simplement yad (ou zenity), même si xdialog
   est disponible et qu'il n'y a pas de gestionnaires de bureau en cours d'exécution (seulement des gestionnaires de fenêtres ou similaires.. )

![](easybasguidialogs.jpeg)

#### Mode fenêtre des boîtes

La fenêtre backend peut être forcée en utilisant la variable d'environnement `supermode` pour
le programme backend de votre choix :

```bash
export supermode="kdialog"

source easybashgui

message "hola"
```

![](easybasguidialogs.jpeg)

#### Taille des fenêtres des boîtes

Toutes les fonctions de fenêtres prennent en charge les options `<-w|-width> [integer]` et `<-h|-height> [integer]` 
pour une taille de fenêtre personnalisée à l'exception de `notify_message` et des versions antérieures 
de kdialog !

```bash
source easybashgui

message -w 800 -h 100 "Hello World!"
```

![](easybashgui-example0.jpeg)

#### Compatibilité du comportement des boîtes

**IMPORTANT**: Chaque interface GUI a sa propre façon d'entrer de l'utilisateur,
alors que Yad peut avoir 3 boîtes de saisie de texte en même temps, au contraire, Zenity
ne peut en avoir qu'une à la fois, vous pouvez voir cela dans les exemples ci-dessous

![](easybashgui-example4.jpeg)

## Exemples

Vous devez créer les scripts en langage `bash`, EBG est codé en `bash`, dans ce document
Nous utiliserons bash pour illustrer les exemples d'utilisation :

1. Installez EBG ou sourcez les 3 fichiers minimum
2. Créez votre nouveau script de programme 
3. Sourcez le point d'entrée principal d'EBG (consultez les exemples suivants)
4. Mettez vos phrases de code en bash
5. Enregistrez et lancez le nouveau programme script

- Liste des exemples :
    - [Boîtes de questions simples](#boîtes-de-questions-simples)
    - [Boîte de texte simple à partir de l'entrée standard](#boîte-de-texte-simple-à-partir-de-lentrée-standard)
    - [L'attente de réponse](#lattente-de-réponse)
    - [Sélection de répertoire simple](#sélection-de-répertoire-simple)
    - [Exemples d'entrée triplet](#exemples-dentrée-triplet)
    - [Barre de progression](#barre-de-progression)
    - [Jauge de niveau](#jauge-de-niveau)
    - [Sélection de menu](#sélection-de-menu)
    - [Choisir des éléments](#choisir-des-éléments)
    - [Un exemple plus complexe](#un-exemple-plus-complexe)
    - [Un exemple de notification](#un-exemple-de-notification)

#### Boîtes de questions simples

Ce morceau de code lancera 3 dialogues, le premier est la question principale avec un
bouton "ok" par défaut pour une réponse positive, dans les boîtes backend limitées, il n'affichera qu'un
bouton "ok" unique et pour annuler, il suffit d'appuyer sur la touche "ESC".. Si la réponse négative 
(annuler) est détectée, il lancera une boîte de message d'alerte ou alors une boîte de réponse avec confirmation.

```bash
source easybashgui

question "Aimez-vous la musique country ?"
answer="${?}"
if [ ${answer} -eq 0 ]
    then
    ok_message "Vous l'aimez :)"
elif [ ${answer} -eq 1 ]
    then
    alert_message "Vous ne l'aimez pas :("
else
    ok_message "À bientôt"
    exit 0
fi
```

![](easybashgui-dialogs1.jpeg)

#### Boîte de texte simple à partir de l'entrée standard

Ce morceau de code lancera une boîte de texte à l'intérieur d'une fenêtre mais en utilisant des pipes 
pour être analysé vers STDIN et la fonction `text` :

```bash
source easybashgui

echo -e "Quel est votre nom ?\n\nMon nom est :\nVittorio" | text
```

![](easybashgui-example1.jpeg)

#### L'attente de réponse

Il crée une fenêtre avec un tel texte et rend le contrôle au programme principal... 
pendant ce temps, vous pouvez exécuter plus de commandes, tout ce temps, cette fenêtre avec 
barre de progression sera présente pendant que vos commandes suivantes seront exécutées, 
après tout ce travail, vous pouvez fermer avec une fonction spéciale spécifique :

```bash
source easybashgui

wait_for "Je dors 4 secondes... bonne nuit..."
sleep 4
terminate_wait_for
```

Prenez en considération que `terminate_wait_for` ne fermera (tuera) que 
la dernière fonction `wait_for` exécutée lancée, sinon vous devez passer en argument 
le PID spécifique de la fenêtre à fermer.

![](easybashgui-example2.gif)

#### Sélection de répertoire simple

Ce morceau de code permettra à l'utilisateur de choisir un chemin complet de fichier avec un dialogue
de choix de répertoire pour la sélection de fichier, la sortie standard affiche la sélection.

```bash
source easybashgui

fselect
file="$(0< "${dir_tmp}/${file_tmp}" )"
```

![](easybashgui-example3.jpeg)

#### Exemples d'entrée triplet

Cette double vérification de la même question, avec un bouton "ok" par défaut pour une réponse positive
réponse, dans les boîtes backend limitées n'affichera qu'un bouton "ok" unique
et pour annuler, il suffit d'appuyer sur la touche "ESC".. mais à n'importe quelle partie de l'exécution
l'annulation mettra fin à tout le programme.

La dernière boîte est la deuxième entrée supplémentaire, puis le script stockera toutes les variables
et affichera dans la sortie standard !

```bash
source easybashgui

input 1 "(écrivez ici l'adresse IP)"
input 1 "Veuillez écrire l'adresse IP" "192.168.1.1"
input 2 "Nom d'utilisateur" "root" "Adresse IP" "192.168.0.1"
input 3 "Nom d'utilisateur" "root" "Adresse IP" "192.168.0.1" "Répertoire de destination" "/tmp"
IFS=$'\n' ; choices=( $(0< "${dir_tmp}/${file_tmp}" ) ) ; IFS=$' \t\n'
user="${choices[0]}"
ip="${choices[1]}"
dir="${choices[2]}"
```

![](easybashgui-example4.jpeg)

#### Barre de progression

Vous pouvez canaliser le décompte de progression vers un texte d'une boîte :

```bash
source easybashgui

for i in 10 20 30 40 50 60 70 80 90 100
    do
    echo "${i}"
    sleep 1
done | progress "Ceci est un test de progression..."
```

![](easybashgui-example5.gif)

#### Jauge de niveau

Les jauges de niveau sont faciles à configurer, le résultat du choix sera affiché dans la sortie
standard :

```bash
source easybashgui

adjust "Veuillez régler le niveau de volume" 15 40 75
```

#### Sélection de menu

Les menus sont des processus complexes en interne mais faciles à utiliser pour vous, 
ce ne sont que des éléments et l'élément choisi sera dans le fichier temporaire ;

```bash
menu "Rouge" "Jaune" "Vert"
choice="$(0< "${dir_tmp}/${file_tmp}" )"
```

#### Choisir des éléments

Comme les menus mais permet de choisir plus d'un élément pour vous, 
ce ne sont que des éléments et les sélections seront dans le fichier temporaire ;

```bash
list "+Rouge" "-Jaune" "+Vert"
choice_list="$(0< "${dir_tmp}/${file_tmp}" )"
IFS=$'\n' ; choice_array=( $(0< "${dir_tmp}/${file_tmp}" ) ) ; IFS=$' \t\n'
```

#### Un exemple plus complexe : barre de progression par étapes

```bash
source easybashgui

women=( Angela Carla Michelle Noemi Urma Marisa Karina Anita Josephine Rachel )
for (( index=0 ; index < ${#women[@]} ; index++ )) 
    do
    today_prefered_woman="${women[${index}]}"
    kiss "${today_prefered_woman}"
    sleep 1
    #
    # Travail terminé !!
    # alors...
    echo "PROGRESS"
    #
done | progress "Ceci est un progrès _AMOUR_..." "${#women[@]}"
# si vous utilisez la chaîne "PROGRESS" dans STDIN (echo "PROGRESS") n'oubliez pas le deuxième argument de progress() ( "[nombre d'éléments]" )
```

#### Un exemple de notification

Ceci n'est possible qu'avec le backend Yad :

```bash
source easybashgui

notify -t "Bon tooltip:OK#Mauvais tooltip:MAUVAIS" -i "/usr/local/share/pixmaps/nm-signal-100.png#gtk-fullscreen" "Xclock" "xclock" "Xcalc" "xcalc"
#
while :
    do
    menu BON MAUVAIS
    answer=$(0< "${dir_tmp}/${file_tmp}" )
    #
    if [ "${answer}" = "BON" ]
        then
        notify_message --seconds 3 "Changé en \"bon\" ..."
        notify_change "bon"
    elif [ "${answer}" = "MAUVAIS" ]
        then
        notify_message -s 3 --icon "application-exit" "Changé en \"mauvais\" ..."
        notify_change -i "gtk-help" -t "Ce tooltip est mauvais" "mauvais"
    else
        exit
    fi
    #
done
```

## Référence EBG

Ceci est la documentation de la liste de référence pour la programmation

- Liste des fonctions :
    - [Flux](#flux)
    - [message](#message)
    - [ok_message](#ok_message)
    - [alert_message](#alert_message)
    - [question](#question)
    - [text](#text)
    - [wait_seconds (barre de progression)](#wait_seconds-barre-de-progression)
    - [progress (manière progressive)](#progress-manière-progressive)
    - [progress (manière régressive)](#progress-manière-régressive)
    - [wait_for](#wait_for)
    - [terminate_wait_for](#terminate_wait_for)
    - [fselect](#fselect)
    - [dselect](#dselect)
    - [input](#input)
    - [menu](#menu)
    - [tagged_menu](#tagged_menu)
    - [list](#list)
    - [adjust](#adjust)
    - [notify_message](#notify_message)
    - [notify_change](#notify_change)
    - [notify](#notify)

#### Flux

EBG utilise toujours STDIN et STDOUT en conjonction avec un répertoire/nom de fichier temporaire.

Les noms temporaires sont gérés via les variables `${dir_tmp}` et `${file_tmp}`

#### message

Le plus simple, c'est juste une fenêtre normale

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN : non
* STDOUT : 
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé
* STDERR : non

``` bash
message "[texte]"
```

#### ok_message

Identique à message mais prend en charge la réponse et signale la classe de question au gestionnaire de fenêtres

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN : non
* STDOUT : 
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé
* STDERR : non


``` bash
ok_message "[texte]"
```

#### alert_message

Identique à message mais prend en charge la réponse et signale la classe d'alerte au gestionnaire de fenêtres

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN : non
* STDOUT : 
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé
* STDERR : non


``` bash
alert_message "[texte]"
```

#### question

Identique à message mais offrira un bouton supplémentaire à l'utilisateur pour annuler, la seule différence 
est qu'il prend en charge la sortie vers à la fois SDTERR et le code de sortie :

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN : non
* STDOUT : 
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé
* STDERR :
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé

``` bash
question "[texte]"
```

#### text

Il offrira une couche de canevas à l'utilisateur pour écrire, à partir de l'entrée de l'utilisateur et 
peut également présenter un texte prédéfini à partir de STDIN, il prend en charge la sortie vers 
à la fois SDTERR et STDOUT et le code de sortie présentera le contenu :

* ARGUMENTS : non
* STDIN : peut être canalisé/redirigé pour un contenu prédéfini
    * entrée : l'utilisateur peut écrire
* STDOUT : 
    * (entrée) : le contenu de la boîte est écrit dans `${dir_tmp}`/`${file_tmp}`
* STDERR :
    * (entrée) : le contenu de l'entrée de la boîte sera sorti

``` bash
text <<< "<texte>"
```

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` nom de fichier aléatoire où le contenu a les valeurs une ligne par entrée
* Seulement pour kdialog, zenity, et Xdialog vous pouvez également éditer le texte à l'intérieur de la boîte

#### wait_seconds (barre de progression)

C'est une fonction utilitaire, similaire à `sleep`, mais affichera une 
barre de progression automatique avec une durée du nombre de secondes que vous lui passez :

* ARGUMENTS :
    * secondes : obligatoire, uniquement un entier
* STDIN : non
* STDOUT : 
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi
* STDERR :
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi

``` bash
wait_seconds <entier>
```

#### progress (manière progressive)

C'est une fonction utilitaire, similaire à `wait_seconds`, elle affichera une boîte avec 
une barre qui se remplira à la position du nombre en pourcentage, le nombre pour sélectionner la 
position en pourcentage est lu à partir de STDIN, le nombre peut être canalisé ou analysé à partir de :

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN :
    * entier : entier avec ou sans "%" qui indique combien remplira la barre
* STDOUT : 
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi
* STDERR :
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi

``` bash
(echo "10" ; sleep 1 ; echo "50" ; sleep 1 ; echo "100" ; sleep 1 ) | progress "Pourcentage..."
```

* Pour créer une séquence de progression, vous devez avoir plusieurs instructions avec différents 
nombres qui indiquent la progression

#### progress (manière régressive)

Similaire à `progress` mais en utilisant un indicateur de nombre d'éléments, il affichera une boîte avec 
une barre qui se remplira au nombre d'éléments à gauche, le nombre pour sélectionner la 
position en pourcentage est lu à partir de l'argument, le mot "PROGRESS" doit être canalisé ou analysé 
à partir de STDIN vers la fonction pour indiquer de remplir la barre de progression dans la boîte :

* ARGUMENTS :
    * texte : requis, doit être entre guillemets, uniquement des caractères alphanumériques
    * entier : requis, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN :
    * PROGRESS : doit être envoyé pour indiquer de remplir la barre
* STDOUT : 
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi
* STDERR :
    * code de sortie : 0 sauf s'il est annulé de manière externe, sera n'importe quoi

``` bash
(echo "PROGRESS" ; sleep 1 ; echo "PROGRESS" ; sleep 1 ) | progress "Étapes..." 2
```

#### wait_for

C'est une fonction utilitaire, similaire à `progress`, elle affichera une boîte avec 
une barre de progression dynamique et le texte que vous lui passez, la boîte ne se ferme jamais ni
ne se termine jamais, vous devriez faire quelque chose avec leur variable de contrôle `{wait_for__PID}`

* ARGUMENTS :
    * texte : optionnel, doit être entre guillemets, uniquement des caractères alphanumériques
* STDIN : non
* STDOUT : 
    * `wait_for__PID` : variable de contrôle utilisée pour tuer l'action/fonction
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé
* STDERR :
    * `wait_for__PID` : variable de contrôle utilisée pour tuer l'action/fonction
    * code de sortie : 1 annulé avec ESC, 0 le seul bouton est pressé

``` bash
wait_for "[texte]"
sleep 3
kill -9 ${wait_for__PID}
```

#### terminate_wait_for

C'est une fonction utilitaire, utile pour terminer le processus hérité en utilisant le 
dernier code de sortie ou la variable `{wait_for__PID}` de la fonction précédente :

* ARGUMENTS :
    * PID : optionnel, PID numérique du processus à terminer et capturer le résultat
* STDIN : non
* STDOUT : 
    * code de sortie : 1 si le PID n'est pas trouvé, 0 si le processus a été terminé
* STDERR :
    * code de sortie : 1 si le PID n'est pas trouvé, 0 si le processus a été terminé

``` bash
message "[texte]" && terminate_wait_for
```

Dans cet exemple, la sortie de `terminate_wait_for` est "1" car le PID de `message` a été 
terminé précédemment (bouton ok appuyé), et le PID n'est plus valide !

``` bash
wait_for "[texte]"
sleep 3
... plus de code
terminate_wait_for
```

Dans cet exemple, la sortie de `terminate_wait_for` est "0" car le PID de `wait_for` était 
actif, le PID est toujours valide et la sortie dans STDOUT qui est STDIN pour `terminate_wait_for`

#### fselect

Cette fonction permettra de choisir un fichier et vous permettra de l'utiliser dans les 
variables `${dir_tmp}`/`${file_tmp}` et STDERR pour vérifier le résultat de l'entrée

* ARGUMENTS :
    * chemin : optionnel, chemin de chaîne de l'endroit par défaut à suggérer pour le fichier
* STDIN : non
* STDOUT : 
    * chemin+fichier sélectionné : le chemin et le nom du fichier choisi sélectionné dans la boîte
* STDERR :
    * chemin+fichier sélectionné : le chemin et le nom du fichier choisi sélectionné dans la boîte

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a le chemin du fichier choisi

``` bash
fselect "[/chemin/vers/répertoire/[fichiersuggéré]]"
```

#### dselect

Cette fonction permettra de choisir un répertoire et vous permettra de l'utiliser dans les 
variables `${dir_tmp}`/`${file_tmp}` et STDERR pour vérifier le résultat de l'entrée

* ARGUMENTS :
    * chemin : optionnel, chemin de chaîne de l'endroit par défaut à suggérer pour le chemin à choisir
* STDIN : non
* STDOUT : 
    * chemin choisi : le chemin et le nom du répertoire choisi sélectionné dans la boîte
* STDERR :
    * chemin choisi : le chemin et le nom du répertoire choisi sélectionné dans la boîte

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a le chemin du répertoire choisi

``` bash
fselect "[/chemin/vers/répertoire/]"
```

#### input

Cette fonction affichera dans la même boîte une, deux et/ou trois entrées, en fonction 
des paramètres et peut être initialisée avec des valeurs par défaut comme suggestions, 
et vous permettra de l'utiliser dans les variables `${dir_tmp}`/`${file_tmp}` 
et STDERR pour vérifier le résultat de l'entrée

* ARGUMENTS :
    * entrées : requis, indique le nombre d'entrées, peut être 1, 2 ou 3
    * étiquette : requis, elle est répétée autant de fois que d'entrées indiquées
    * init : requis, suit l'étiquette et est optionnel uniquement si un cas d'entrée 
* STDIN : non
* STDOUT : 
    * valeurs : les valeurs d'entrée des étiquettes dans l'ordre, une ligne par valeur
* STDERR :
    * valeurs : les valeurs d'entrée des étiquettes dans l'ordre, une ligne par valeur

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a les valeurs une ligne par entrée

``` bash
input 1 "<étiquette> [valeur]"
```

Dans ce cas, il n'y a qu'une seule entrée et la valeur suggérée peut être optionnelle, mais pour :

``` bash
input 2 "<étiquette>" "<valeur>" "<étiquette2>" "<valeur2>"
```

Et aussi pour le cas de trois entrées :

``` bash
input 3 "<étiquette>" "<valeur>" "<étiquette2>" "<valeur2>" "<étiquette3>" "<valeur3>"
```

#### menu

Cette fonction affichera dans la même boîte un ou plusieurs éléments dans une liste, 
cette liste agira comme un menu de sélection et un seul élément peut être sélectionné, 
et vous permettra de l'utiliser dans les variables `${dir_tmp}`/`${file_tmp}` 
et STDERR pour vérifier le résultat de l'entrée

* ARGUMENTS :
    * élément(s) : éléments d'entrée à afficher dans la liste du menu, doivent être entre guillemets
* STDIN : non
* STDOUT : 
    * valeurs : affiche l'élément sélectionné
* STDERR :
    * valeurs : affiche l'élément sélectionné

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a les valeurs sélectionnées dans l'ordre

``` bash
menu "<élément1>" "[élément2]" .. "[élémentN-1]" "[élémentN]" 
```

#### tagged_menu

Comme les menus, affichera dans la même boîte un ou plusieurs éléments dans une liste, 
cette liste agira comme un menu de sélection et un seul élément peut être sélectionné, 
mais cette sélection d'élément aura une étiquette qui peut être utilisée dans le script !
et vous permettra de l'utiliser dans les variables `${dir_tmp}`/`${file_tmp}` 
et STDERR pour vérifier le résultat de l'entrée

* ARGUMENTS :
    * élément(s) : éléments d'entrée à afficher dans la liste du menu, doivent être entre guillemets
    * étiquette(s) : étiquettes qui seront affichées à la place des éléments
* STDIN : non
* STDOUT : 
    * valeurs : affiche l'élément sélectionné, pas l'étiquette
* STDERR :
    * valeurs : affiche l'élément sélectionné, pas l'étiquette

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a les valeurs sélectionnées dans l'ordre

``` bash
tagged_menu "<élément1>" "<étiquette1>" "[élément2]" "[étiquette2]" .. "[élémentN]" "[étiquetteN]"
```

#### list

Comme les menus, affiche dans la même boîte un ou plusieurs éléments dans une liste, 
cette liste agira comme un menu de sélection et plusieurs éléments peuvent être sélectionnés, 
et vous permettra de l'utiliser dans les variables `${dir_tmp}`/`${file_tmp}` 
et STDERR pour vérifier le résultat des sélections une ligne par élément sélectionné dans l'ordre :

* ARGUMENTS :
    * `<+|->` : préréglages, si "+" sera sélectionné et si "-" sera désélectionné
    * élément(s) : éléments d'entrée à afficher dans la liste du menu, doivent être entre guillemets
* STDIN : non
* STDOUT : 
    * valeurs : affiche les éléments sélectionnés une ligne par sélection
* STDERR :
    * valeurs : affiche les éléments sélectionnés une ligne par sélection

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a les valeurs sélectionnées dans l'ordre

``` bash
list "< <+|->élément1>" "[<+|->élément2]" .. "[<+|->élémentN-1]" "[<+|->élémentN]"
```

#### adjust

Cette fonction affichera une barre de curseur avec un sélecteur, la barre représente de 1 à 100  
et vous permettra de l'utiliser dans les variables `${dir_tmp}`/`${file_tmp}` et STDERR 
pour vérifier le résultat de la position du curseur :

* ARGUMENTS :
    * texte : étiquette à afficher sur le curseur
    * min : valeur minimale autorisée que le curseur ira à gauche
    * init : la valeur qui commencera le sélecteur sur le curseur lors de l'affichage
    * max : valeur maximale autorisée que le curseur ira à droite
* STDIN : non
* STDOUT : 
    * valeurs : affiche les éléments sélectionnés une ligne par sélection
* STDERR :
    * valeurs : affiche les éléments sélectionnés une ligne par sélection

Ces variables sont remplies lorsque l'action est terminée :

* `${dir_tmp}` est un répertoire de chemin aléatoire pour placer le fichier contenant le fichier suivant
* `${file_tmp}` un nom de fichier aléatoire où le contenu a les valeurs sélectionnées dans l'ordre

``` bash
ajust "[texte]" "[min]" "[init]" "[max]"
```


#### notify_message

Comme "message" mais sous forme de notification, permet de choisir l'icône à afficher :

* ARGUMENTS :
    * icône : optionnel, image à afficher dans la boîte à côté
    * texte : contenu à afficher dans la boîte
* STDIN : non
* STDOUT : 
    * PID : affiche le PID du processus en cours
* STDERR :
    * PID : affiche le PID du processus en cours

``` bash
notify_message [-i|--icon "<icône>"] [-s|--seconds "<secondes>"] "[texte]"
```

#### notify_change

Cette fonction est utilisée pour changer la notification de la barre d'état système de bureau d'un état (disons "bon" )
à l'autre état (disons : "mauvais" ) défini _précédemment par la fonction notify() _ (voir ci-dessous ); 
de plus, vous pouvez éventuellement changer à la volée même l'icône de la barre d'état système et son info-bulle :

* ARGUMENTS :
    * icône : optionnel, image à afficher dans la boîte à côté
    * texte : contenu à afficher dans la boîte
* STDIN : non
* STDOUT : 
    * PID : affiche le PID du processus en cours
* STDERR :
    * PID : affiche le PID du processus en cours

``` bash
notify_change [-i "<nouvelleicône>"] [-t "<nouvelleinfobulle>"] "[bon|mauvais]"
```

#### notify

Comme "message" mais maintenant sous forme de notification de la barre d'état système de bureau à afficher :

* ARGUMENTS :
    * commande bouton gauche : optionnel, programme sera lancé si clic droit
    * icône : chemin vers l'icône à afficher si donné, pour les types bon/mauvais
    * texte info-bulle : texte à afficher dans chaque cas
    * éléments de menu : éléments de menu à afficher lors de la sélection
* STDIN : non
* STDOUT : 
    * PID : affiche le PID du processus en cours
* STDERR :
    * PID : affiche le PID du processus en cours

``` bash
notify [-c "<commande>"] [-i "<icônebon|icônemauvais>"] [-t "<textebon|textemauvais>"] "<élément1>" "<commande1>" "[élément2]" "[commande2]" .. "[élémentN]" "[commandeN]"
```

## Notes

EasyBashGUI ne fonctionne pas avec le "dialog" original (ancien) qui est très limité ; si vous avez la première version "dialog" dans votre boîte, installez "cdialog" et alias ou liez "dialog" à cdialog.

Depuis la version 5.0.0, vous pouvez utiliser EasyBashGUI même si AUCUN backend WIDGET n'est installé (c'est-à-dire : pas de yad, pas de gtkdialog, pas de kdialog, pas de zenity, pas de Xdialog, pas de gum, pas de (c)dialog... doh!!!!! ). Pour utiliser "super bare" EBG, il suffit de supprimer la bibliothèque ".lib" de votre chemin, ou de définir la variable "supermode" sur "none" avant de sourcer easybashgui (par exemple : >export supermode="none" && source easybashgui && message "Hello world..." )

EasyBashGUI définit les déclarations de sortie gtkdialog comme variables via "eval". De cette façon, en théorie, cela pourrait être potentiellement dangereux ; néanmoins, jusqu'à présent, je ne connais pas d'alternative...
