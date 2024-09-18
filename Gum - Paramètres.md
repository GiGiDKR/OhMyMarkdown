Corriger la syntaxe du fichier Markdown joint

Pour corriger la syntaxe du fichier Markdown joint, je vais examiner le contenu et apporter les modifications nécessaires pour améliorer sa structure et sa lisibilité. Voici la version corrigée :

# gum choose

### Paramètres principaux

- **--limit, -l** : Nombre maximum d'éléments à choisir (par défaut : 1)
- **--height** : Hauteur du menu (par défaut : 10)
- **--cursor** : Caractère du curseur (par défaut : "> ")
- **--header** : En-tête à afficher au-dessus des choix
- **--cursor-prefix** : Préfixe du curseur (par défaut : "")
- **--selected-prefix** : Préfixe pour les éléments sélectionnés (par défaut : "")
- **--unselected-prefix** : Préfixe pour les éléments non sélectionnés (par défaut : "")
- **--selected** : Indices pré-sélectionnés (séparés par des virgules)
- **--no-limit** : Désactive la limite de sélection

### Options de style

- **--item.fg** : Couleur du texte des éléments
- **--item.bg** : Couleur de fond des éléments
- **--selected.fg** : Couleur du texte des éléments sélectionnés
- **--selected.bg** : Couleur de fond des éléments sélectionnés
- **--cursor.fg** : Couleur du curseur
- **--cursor.bg** : Couleur de fond du curseur

### Utilisation

La commande "gum choose" permet de créer un menu de sélection interactif. Voici un exemple d'utilisation :

```bash
gum choose "Fraise" "Banane" "Cerise"
```

Cette commande affichera une liste de choix parmi lesquels l'utilisateur pourra sélectionner une option.

Vous pouvez personnaliser l'apparence et le comportement du menu en utilisant les différents paramètres mentionnés ci-dessus. Par exemple, pour permettre la sélection de plusieurs éléments avec une limite de 3, vous pouvez utiliser :

```bash
gum choose --limit 3 "Option 1" "Option 2" "Option 3" "Option 4"
```

N'oubliez pas que vous pouvez toujours utiliser la commande `gum choose --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum write

### Paramètres principaux

- **--placeholder** : Texte d'espace réservé à afficher lorsque l'entrée est vide
- **--prompt** : Invite à afficher avant l'entrée (par défaut : "> ")
- **--show-cursor** : Afficher le curseur
- **--show-line-numbers** : Afficher les numéros de ligne
- **--width** : Largeur de la zone de texte (par défaut : 50)
- **--height** : Hauteur de la zone de texte (par défaut : 1)
- **--header** : En-tête à afficher au-dessus de l'entrée
- **--char-limit** : Limite de caractères (par défaut : pas de limite)
- **--base** : Texte initial à éditer

### Options de style

- **--prompt.fg** : Couleur du texte de l'invite
- **--prompt.bg** : Couleur de fond de l'invite
- **--cursor.fg** : Couleur du curseur
- **--cursor.bg** : Couleur de fond du curseur
- **--text.fg** : Couleur du texte saisi
- **--text.bg** : Couleur de fond du texte saisi

### Utilisation

La commande "gum write" permet de créer une zone de saisie de texte interactive. Voici un exemple d'utilisation simple :

```bash
gum write
```

Cette commande affichera une zone de texte où l'utilisateur pourra saisir du texte. Vous pouvez personnaliser l'apparence et le comportement de la zone de saisie en utilisant les différents paramètres. Par exemple, pour créer une zone de saisie multilignes avec un en-tête et un texte d'espace réservé :

```bash
gum write --height 5 --width 40 --header "Entrez votre message" --placeholder "Tapez ici..."
```

Pour éditer un texte existant :

```bash
gum write --base "Texte initial à éditer"
```

N'oubliez pas que vous pouvez utiliser la commande `gum write --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum spin

### Paramètres principaux

- **--show-output** : Affiche la sortie de la commande exécutée
- **--spinner, -s** : Type de spinner à utiliser
- **--title** : Texte à afficher pendant l'exécution du spinner
- **--align, -a** : Alignement du spinner par rapport au titre

### Options de style pour le spinner

- **--spinner.background** : Couleur de fond du spinner
- **--spinner.foreground** : Couleur du texte du spinner
- **--spinner.border** : Style de bordure du spinner
- **--spinner.border-background** : Couleur de fond de la bordure du spinner
- **--spinner.border-foreground** : Couleur de la bordure du spinner
- **--spinner.align** : Alignement du texte du spinner
- **--spinner.height** : Hauteur du texte du spinner
- **--spinner.width** : Largeur du texte du spinner
- **--spinner.margin** : Marge du texte du spinner
- **--spinner.padding** : Rembourrage du texte du spinner
- **--spinner.bold** : Texte en gras pour le spinner
- **--spinner.faint** : Texte atténué pour le spinner
- **--spinner.italic** : Texte en italique pour le spinner
- **--spinner.strikethrough** : Texte barré pour le spinner
- **--spinner.underline** : Texte souligné pour le spinner

### Options de style pour le titre

- **--title.background** : Couleur de fond du titre
- **--title.foreground** : Couleur du texte du titre
- **--title.border** : Style de bordure du titre
- **--title.border-background** : Couleur de fond de la bordure du titre
- **--title.border-foreground** : Couleur de la bordure du titre
- **--title.align** : Alignement du texte du titre
- **--title.height** : Hauteur du texte du titre
- **--title.width** : Largeur du texte du titre
- **--title.margin** : Marge du texte du titre
- **--title.padding** : Rembourrage du texte du titre
- **--title.bold** : Texte en gras pour le titre
- **--title.faint** : Texte atténué pour le titre
- **--title.italic** : Texte en italique pour le titre
- **--title.strikethrough** : Texte barré pour le titre
- **--title.underline** : Texte souligné pour le titre
Réformater en Markdown en affichant seulement en anglais les nom des types de spinner

Voici le reformatage en Markdown avec les noms des types de spinner en anglais uniquement :

## Types de spinners

- `line`
- `dot`
- `minidot`
- `jump`
- `pulse`
- `points`
- `globe`
- `moon`
- `monkey`
- `meter`
- `hamburger`
### Utilisation

La commande "gum spin" affiche un spinner pendant l'exécution d'une commande. Voici un exemple d'utilisation :

```bash
gum spin --title "Chargement en cours..." -- sleep 5
```

Cette commande affichera un spinner avec le titre "Chargement en cours..." pendant 5 secondes.

Vous pouvez personnaliser l'apparence du spinner et du titre en utilisant les différentes options de style mentionnées ci-dessus. Par exemple :

```bash
gum spin --spinner.foreground "blue" --title.bold --title "Traitement des données" -- longue_commande
```

N'oubliez pas que vous pouvez utiliser la commande `gum spin --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum filter

### Paramètres principaux

- **--placeholder** : Texte d'espace réservé à afficher lorsque l'entrée est vide
- **--prompt** : Invite à afficher avant l'entrée (par défaut : "> ")
- **--width** : Largeur de la zone de filtre (par défaut : largeur du terminal)
- **--height** : Hauteur de la zone de filtre (par défaut : hauteur du terminal)
- **--indicator** : Caractère indicateur pour l'élément sélectionné (par défaut : ">")
- **--limit** : Nombre maximum d'éléments à afficher
- **--reverse** : Inverser l'ordre des éléments
- **--sort** : Trier les éléments par ordre alphabétique
- **--fuzzy** : Utiliser la correspondance floue pour le filtrage
- **--header** : En-tête à afficher au-dessus de la liste

### Options de style

- **--text.foreground** : Couleur du texte
- **--text.background** : Couleur de fond du texte
- **--match.foreground** : Couleur du texte correspondant
- **--match.background** : Couleur de fond du texte correspondant
- **--prompt.foreground** : Couleur du texte de l'invite
- **--prompt.background** : Couleur de fond de l'invite
- **--cursor.foreground** : Couleur du curseur
- **--cursor.background** : Couleur de fond du curseur
- **--indicator.foreground** : Couleur de l'indicateur
- **--indicator.background** : Couleur de fond de l'indicateur
- **--indicator.border** : Style de bordure pour l'indicateur

### Utilisation

La commande "gum filter" permet de filtrer interactivement une liste d'éléments. Voici un exemple d'utilisation :

```bash
echo -e "pomme\nbanane\ncerise" | gum filter
```

Cette commande affichera une liste filtrable d'éléments où l'utilisateur pourra rechercher et sélectionner un élément. Vous pouvez personnaliser l'apparence et le comportement du filtre en utilisant les différents paramètres. Par exemple :

```bash
cat liste_items.txt | gum filter --limit 10 --fuzzy --header "Sélectionnez un élément :"
```

Cette commande affichera un maximum de 10 éléments, utilisera la correspondance floue et affichera un en-tête au-dessus de la liste.

N'oubliez pas que vous pouvez utiliser la commande `gum filter --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum confirm

### Paramètres principaux

- **[]** : Texte de l'invite à afficher (argument optionnel)
- **--affirmative** : Texte pour l'option affirmative (par défaut : "Oui")
- **--negative** : Texte pour l'option négative (par défaut : "Non")
- **--default** : Réponse par défaut (true/false)
- **--timeout** : Délai d'expiration en secondes

### Options de style

- **--prompt.foreground** : Couleur du texte de l'invite
- **--prompt.background** : Couleur de fond de l'invite
- **--prompt.border** : Style de bordure pour l'invite
- **--selected.foreground** : Couleur du texte de l'option sélectionnée
- **--selected.background** : Couleur de fond de l'option sélectionnée
- **--unselected.foreground** : Couleur du texte de l'option non sélectionnée
- **--unselected.background** : Couleur de fond de l'option non sélectionnée

### Utilisation

La commande "gum confirm" permet de demander une confirmation à l'utilisateur. Voici un exemple d'utilisation simple :

```bash
gum confirm "Êtes-vous sûr de vouloir continuer ?"
```

Cette commande affichera une invite de confirmation avec les options "Oui" et "Non". Vous pouvez personnaliser le comportement et l'apparence de la confirmation en utilisant les différents paramètres. Par exemple :

```bash
gum confirm --affirmative "Continuer" --negative "Annuler" --default=false "Voulez-vous procéder à l'opération ?"
```

Cette commande personnalise le texte des options et définit la réponse par défaut sur "Non".

Le résultat de la commande "gum confirm" peut être utilisé dans des scripts pour conditionner l'exécution d'autres commandes. Par exemple :

```bash
if gum confirm "Supprimer le fichier ?"; then
    rm fichier.txt
else
    echo "Opération annulée"
fi
```

N'oubliez pas que vous pouvez utiliser la commande `gum confirm --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum input

### Paramètres principaux

- **--placeholder** : Texte d'espace réservé à afficher lorsque l'entrée est vide
- **--prompt** : Invite à afficher avant l'entrée
- **--width** : Largeur de la zone de saisie
- **--header** : En-tête à afficher au-dessus de l'entrée
- **--password** : Masquer l'entrée (pour les mots de passe)
- **--char-limit** : Limite de caractères pour l'entrée
- **--value** : Valeur initiale de l'entrée

### Options de style

- **--prompt.foreground** : Couleur du texte de l'invite
- **--prompt.background** : Couleur de fond de l'invite
- **--cursor.foreground** : Couleur du curseur
- **--cursor.background** : Couleur de fond du curseur

### Utilisation

La commande "gum input" permet de demander une entrée à l'utilisateur. Voici quelques exemples d'utilisation :

```bash
# Demande simple d'entrée
gum input > reponse.txt

# Demande de mot de passe (entrée masquée)
gum input --password > mot_de_passe.txt

# Personnalisation de l'invite
domain_input=$(gum input --placeholder "test.fomm.au")
```

Vous pouvez personnaliser l'apparence et le comportement de l'entrée en utilisant les différents paramètres. Par exemple :

```bash
gum input --width 40 --header "Entrez votre nom" --placeholder "John Doe"
```

Cette commande affichera une zone de saisie de 40 caractères de large avec un en-tête et un texte d'espace réservé.

N'oubliez pas que vous pouvez utiliser la commande `gum input --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum file

### Paramètres principaux

- **--all, -a** : Afficher les fichiers cachés
- **--cursor** : Caractère du curseur (par défaut : ">")
- **--height** : Hauteur maximale de la liste (par défaut : 10)
- **--width** : Largeur maximale de la liste
- **--header** : Texte d'en-tête à afficher au-dessus de la
liste
- **--placeholder** : Texte d'espace réservé à afficher lorsque l'entrée est vide
- **--prompt** : Invite à afficher avant l'entrée (par défaut : "> ")
- **--file** : Sélectionner uniquement les fichiers
- **--directory** : Sélectionner uniquement les répertoires
- **--limit** : Nombre maximum d'éléments à sélectionner

## Options de style

- **--cursor.foreground** : Couleur du curseur
- **--cursor.background** : Couleur de fond du curseur
- **--selected.foreground** : Couleur du texte sélectionné
- **--selected.background** : Couleur de fond du texte sélectionné
- **--unselected.foreground** : Couleur du texte non sélectionné
- **--unselected.background** : Couleur de fond du texte non sélectionné

## Utilisation

La commande "gum file" permet de naviguer et de sélectionner des fichiers ou des répertoires de manière interactive. Voici quelques exemples d'utilisation :

```bash
# Sélectionner un fichier
fichier_selectionne=$(gum file)

# Sélectionner un répertoire
repertoire_selectionne=$(gum file --directory)

# Sélectionner plusieurs fichiers
fichiers_selectionnes=$(gum file --limit 3)
```

Vous pouvez personnaliser l'apparence et le comportement de la sélection de fichiers en utilisant les différents paramètres. Par exemple :

```bash
gum file --all --header "Sélectionnez un fichier :" --height 15 --cursor "→"
```

Cette commande affichera une liste de fichiers (y compris les fichiers cachés) avec un en-tête personnalisé, une hauteur maximale de 15 lignes et un curseur personnalisé.

N'oubliez pas que vous pouvez utiliser la commande `gum file --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum table

### Paramètres principaux

- **--columns, -c** : Noms des colonnes
- **--widths, -w** : Largeurs des colonnes
- **--height** : Hauteur de la table
- **--file, -f** : Chemin du fichier d'entrée
- **--separator** : Séparateur de colonnes pour l'entrée (par défaut : ",")
- **--header** : Traiter la première ligne comme l'en-tête
- **--pad** : Ajouter un espace de remplissage entre les colonnes

### Options de style

- **--border** : Style de bordure (par exemple : "rounded", "double", "none")
- **--border-foreground** : Couleur de la bordure
- **--border-background** : Couleur de fond de la bordure
- **--header.foreground** : Couleur du texte de l'en-tête
- **--header.background** : Couleur de fond de l'en-tête
- **--row.foreground** : Couleur du texte des lignes
- **--row.background** : Couleur de fond des lignes

### Utilisation

La commande "gum table" permet d'afficher des données tabulaires de manière formatée dans le terminal. Voici quelques exemples d'utilisation :

```bash
# Afficher un fichier CSV comme une table
gum table < data.csv

# Spécifier les noms et largeurs des colonnes
echo "Alice,25\nBob,30" | gum table --columns "Nom,Âge" --widths 10,5

# Utiliser un séparateur personnalisé
echo "Alice;25\nBob;30" | gum table --separator ";"
```

Vous pouvez personnaliser l'apparence de la table en utilisant les différentes options de style. Par exemple :

```bash
gum table --border rounded --header --border-foreground 212 < data.csv
```

Cette commande affichera une table avec des bordures arrondies, traitera la première ligne comme un en-tête et utilisera une couleur spécifique pour les bordures.

"gum table" est particulièrement utile pour présenter des données CSV de manière élégante dans la ligne de commande. Vous pouvez l'utiliser pour formater la sortie d'autres commandes, comme dans cet exemple :

```bash
az sql mi list | jq -r '.[] | [.name, .resourceGroup, .location] | @csv' | gum table --columns "Name,Resource Group,Location" --separator ","
```

N'oubliez pas que vous pouvez toujours utiliser la commande `gum table --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.

# gum style

### Paramètres principaux

- **--foreground, -f** : Couleur du texte
- **--background, -b** : Couleur de fond
- **--border** : Style de bordure (par exemple : "rounded", "double", "none")
- **--border-foreground** : Couleur de la bordure
- **--border-background** : Couleur de fond de la bordure
- **--padding** : Rembourrage autour du texte
- **--margin** : Marge autour du texte
- **--align** : Alignement du texte (gauche, centre, droite)
- **--width** : Largeur du texte
- **--height** : Hauteur du texte

### Options de style de texte

- **--bold** : Texte en gras
- **--italic** : Texte en italique
- **--strikethrough** : Texte barré
- **--underline** : Texte souligné
- **--faint** : Texte atténué

### Utilisation

La commande "gum style" permet de formater et de styliser du texte dans le terminal. Voici quelques exemples d'utilisation :

```bash
# Texte coloré
echo "Texte en rouge" | gum style --foreground 212

# Texte avec bordure
echo "Texte encadré" | gum style --border double --padding "1 2"

# Texte stylisé
echo "Texte important" | gum style --bold --italic --underline

# Combinaison de styles
echo "Titre" | gum style --foreground 212 --background 236 --border rounded --align center --width 20
```

Vous pouvez combiner plusieurs options pour créer des styles personnalisés. Par exemple :

```bash
echo "Message d'erreur" | gum style --foreground 196 --background 52 --border thick --padding "1 2" --bold
```

Cette commande affichera un message d'erreur en rouge sur fond sombre, avec une bordure épaisse et en gras.

"gum style" est particulièrement utile pour améliorer la lisibilité et l'esthétique des sorties de script. Vous pouvez l'utiliser pour mettre en évidence des informations importantes ou pour créer des interfaces utilisateur en ligne de commande plus attrayantes.

N'oubliez pas que vous pouvez toujours utiliser la commande `gum style --help` pour obtenir une liste complète des options disponibles directement dans votre terminal.