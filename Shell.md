## Exemple

```yaml
# shell.dll - Configuration de bas
shell {
  # Activation des fonctionnalités
  enabled true

  # Configuration du menu contextuel
  context_menu {
    # Menu principal
    items [
      # Exemple 1: Menu simple
      {
        name: "Ouvrir avec Notepad"
        command: "notepad.exe"
        icon: "notepad"
        type: "file"
      }

      # Exemple 2: Sous-menu
      {
        name: "Outils développeur"
        type: "menu"
        items [
          {
            name: "Visual Studio Code"
            command: "code"
            icon: "%ProgramFiles%/Microsoft VS Code/Code.exe"
          }
          {
            name: "Git Bash"
            command: "C:/Program Files/Git/git-bash.exe"
            icon: "git"
          }
        ]
      }

      # Exemple 3: Menu conditionnel
      {
        name: "Compresser en ZIP"
        command: "powershell Compress-Archive -Path '${path}' -DestinationPath '${dir}/${name}.zip'"
        icon: "archive"
        visibility: "exists('${path}')"
      }
    ]
  }
}

```

Cette configuration de base illustre :

- Un menu simple pour ouvrir des fichiers avec Notepad
- Un sous-menu pour les outils de développement
- Un menu conditionnel pour la compression de fichiers

Les variables comme `${path}` et `${dir}` sont automatiquement remplacées par Shell.

## **Configuration Shell pour Windows**

## Configuration de base

```yaml
shell {
  # Configuration globale
  version = 0.1
  language = "fr-FR"

  # Menu contextuel principal
  context_menu {
    items = [
      # Menu simple
      {
        title = "Outils rapides"
        icon = "tools"
        items = [
          {
            title = "Ouvrir avec Notepad++"
            icon = "notepad++"
            command = "%ProgramFiles%/Notepad++/notepad++.exe \\\\"${sel_path}\\\\""
          }
        ]
      }
    ]
  }
}

```

## Menus avancés avec conditions

```yaml
shell {
  context_menu {
    items = [
      # Menu pour les fichiers images uniquement
      {
        title = "Outils image"
        icon = "image"
        where = "sel.file.ext.image"
        items = [
          {
            title = "Redimensionner"
            command = "magick convert \\\\"${sel_path}\\\\" -resize 50% \\\\"${sel_dir}/${sel_name}_resized.${sel_ext}\\\\""
          }
        ]
      }

      # Menu pour les développeurs
      {
        title = "Dev Tools"
        where = "sel.file.ext.code" # Fichiers de code uniquement
        items = [
          {
            title = "Git Status"
            icon = "git"
            command = "powershell -NoExit -Command \\\\"cd '${sel_dir}'; git status\\\\""
          }
        ]
      }
    ]
  }
}

```

## Styles et personnalisation

```yaml
shell {
  styles {
    # Style global
    "*" {
      font = "Segoe UI"
      size = 12
      color = "#202020"
    }

    # Style spécifique
    "dev_menu" {
      background = "#f0f0f0"
      margin = 2
      padding = 4
    }
  }

  # Utilisation des styles
  context_menu {
    items = [
      {
        title = "Menu stylisé"
        class = "dev_menu"
        items = [...]
      }
    ]
  }
}

```

## Variables et fonctions utiles

```yaml
shell {
  variables {
    apps = "%ProgramFiles%"
    tools = "%tools_path%"
  }

  functions {
    # Vérification d'existence de fichier
    check_file(path) {
      return io.file.exists(path)
    }
  }

  context_menu {
    items = [
      {
        title = "Lance l'application"
        where = "check_file('${apps}/myapp.exe')"
        command = "${apps}/myapp.exe"
      }
    ]
  }
}

```

## **Modification des éléments du menu contextuel Shell**

1. Modification des éléments existants
2. Suppression d'éléments
3. Désactivation d'éléments
4. Déplacement d'éléments
5. Exemples pratiques

## Configuration détaillée

```yaml
shell {
  modify {
    # 1. Modification des éléments existants
    "Open with" {
      # Modification du titre
      text = "Ouvrir avec..."
      # Ajout d'une icône
      icon = "open"
      # Modification de la position
      position = "bottom"
    }

    # 2. Suppression d'éléments
    "Send to" {
      mode = "remove"
    }

    # 3. Désactivation d'éléments
    "Share" {
      mode = "disable"
    }

    # 4. Déplacement d'éléments
    "Copy as path" {
      position = "top"
    }

    # 5. Modification avec conditions
    "Print" {
      where = "sel.file.ext.image" # Uniquement pour les images
      text = "Imprimer l'image"
      icon = "print"
    }

    # 6. Regroupement d'éléments
    "*" {
      where = "this.type.equals('share')"
      menu = "Partage"
      position = 10
    }
  }

  # Exemple complet de personnalisation
  modify_unknown {
    # Gestion des éléments inconnus
    mode = "hide" # options: show, hide, remove
  }

  # Modification des séparateurs
  modify_separator {
    # Personnalisation des séparateurs
    type = "separator"
    style = "single_line"
    size = 1
    color = "#808080"
  }
}

```

## Exemples d'utilisation avancée

```yaml
shell {
  modify {
    # Personnalisation du menu "Nouveau"
    "New" {
      text = "Créer"
      icon = "new"
      items = [
        {
          type = "separator"
          where = "index == 0"
        }
        {
          text = "Document texte"
          command = "notepad.exe"
          position = "top"
        }
      ]
    }

    # Modification des éléments Windows Defender
    "Scan with Microsoft Defender" {
      text = "Analyser avec Windows Defender"
      icon = "%SystemRoot%/System32/SecurityHealthHost.exe"
      position = -1 # Dernier élément
    }

    # Regroupement des options de compression
    "*" {
      where = "this.type.equals('compress')"
      menu = "Compression"
      icon = "archive"
      position = "bottom"
    }
  }
}

```

Ces exemples montrent comment :

- Modifier le texte et les icônes
- Déplacer ou supprimer des éléments
- Ajouter des conditions d'affichage
- Regrouper des éléments similaires
- Personnaliser l'apparence des séparateurs

Pour appliquer les modifications :

1. Mettre à jour le fichier `shell.dll`
2. Redémarrer l'Explorateur Windows

## **Création de nouveaux éléments dans Shell**

1. Structure de base pour nouveaux éléments
2. Types d'éléments différents
3. Exemples pratiques
4. Configuration avancée

## Configuration détaillée

```yaml
shell {
  # Ajout de nouveaux éléments au menu contextuel
  context_menu {
    items = [
      # 1. Menu simple
      {
        title = "Outils rapides"
        icon = "tools"
        items = [
          {
            title = "Ouvrir terminal ici"
            icon = "terminal"
            command = "wt.exe -d \\\\"${path}\\\\""
          }
        ]
      }

      # 2. Menu avec séparateur
      {
        type = "separator"
      }

      # 3. Menu avec sous-menus
      {
        title = "Développement"
        icon = "dev"
        items = [
          {
            title = "Git"
            icon = "git"
            items = [
              {
                title = "Status"
                command = "powershell -NoExit -Command \\\\"cd '${path}'; git status\\\\""
              }
              {
                title = "Pull"
                command = "powershell -NoExit -Command \\\\"cd '${path}'; git pull\\\\""
              }
            ]
          }
        ]
      }

      # 4. Menu conditionnel
      {
        title = "Images"
        where = "sel.file.ext.image"
        icon = "image"
        items = [
          {
            title = "Redimensionner"
            command = "magick convert \\\\"${sel_path}\\\\" -resize 50% \\\\"${sel_dir}/${sel_name}_resized.${sel_ext}\\\\""
          }
        ]
      }

      # 5. Menu avec raccourcis clavier
      {
        title = "Éditeur de texte"
        icon = "notepad"
        hotkey = "Ctrl+E"
        command = "notepad.exe \\\\"${sel_path}\\\\""
      }
    ]
  }
}

```

## Exemples avancés

```yaml
shell {
  context_menu {
    items = [
      # Menu dynamique
      {
        title = "Applications récentes"
        type = "menu"
        dynamic = true
        load = {
          # Charge la liste des applications récentes
          command = "powershell Get-Content \\\\"${env.APPDATA}/recent_apps.txt\\\\""
        }
      }

      # Menu avec styles personnalisés
      {
        title = "Actions rapides"
        class = "custom-menu"
        styles = {
          background = "#f0f0f0"
          padding = 8
          font = "Segoe UI"
          size = 12
        }
        items = [
          {
            title = "Copier le chemin"
            command = "echo \\\\"${sel_path}\\\\" | clip"
            icon = "copy"
          }
        ]
      }

      # Menu avec vérification de conditions
      {
        title = "Administration"
        visibility = "admin" # Visible uniquement en mode administrateur
        icon = "admin"
        items = [
          {
            title = "Services Windows"
            command = "services.msc"
          }
        ]
      }
    ]
  }
}

```

Pour activer ces nouveaux éléments :

1. Ajouter la configuration au fichier `shell.dll`
2. Redémarrer l'Explorateur Windows
3. Les nouveaux éléments apparaîtront dans le menu contextuel selon les conditions définies

Variables disponibles :

- `${path}` : Chemin complet
- `${sel_path}` : Chemin du fichier sélectionné
- `${sel_dir}` : Dossier du fichier sélectionné
- `${sel_name}` : Nom du fichier sans extension
- `${sel_ext}` : Extension du fichier

## **Configuration détaillée**

1. Propriétés de base
2. Propriétés d'interface
3. Propriétés de comportement
4. Exemples pratiques

```yaml
shell {
  # 1. Propriétés de base
  version = "1.0"
  language = "fr-FR"
  root = "%APPDATA%/Shell"
  logging = true

  # 2. Propriétés d'interface
  theme {
    name = "modern"
    dark_mode = true
    colors {
      background = "#2D2D2D"
      text = "#FFFFFF"
      accent = "#007ACC"
    }
    fonts {
      default = "Segoe UI"
      size = 12
      weight = "normal"
    }
  }

  # 3. Propriétés de comportement
  behavior {
    # Délai d'affichage des sous-menus
    delay = 200

    # Position des nouveaux éléments
    position = "bottom"

    # Mode d'affichage
    mode = "default" # options: default, compact, extended

    # Activation des icônes
    show_icons = true

    # Taille maximale des menus
    max_items = 20
  }

  # 4. Exemples de propriétés avancées
  properties {
    # Personnalisation des menus
    menu {
      width = 300
      padding = 8
      margin = 2
      opacity = 0.95
      animation = true
    }

    # Configuration des icônes
    icons {
      size = 16
      theme = "system"
      cache = true
      path = "%PROGRAMFILES%/Common Files/Icons"
    }

    # Gestion des raccourcis
    hotkeys {
      enabled = true
      # Exemple de raccourci personnalisé
      custom = [
        {
          key = "Ctrl+Shift+E"
          command = "explorer.exe"
        }
      ]
    }
  }

  # 5. Propriétés conditionnelles
  conditions {
    # Affichage selon le type de fichier
    show_dev_tools = "sel.file.ext.code"
    show_image_tools = "sel.file.ext.image"
  }
}

```

## Propriétés importantes à noter :

- `version` : Version de la configuration
- `language` : Langue de l'interface
- `theme` : Personnalisation visuelle
- `behavior` : Comportement des menus
- `properties` : Propriétés avancées
- `conditions` : Règles d'affichage conditionnelles

## Variables système courantes

```yaml
shell {
  variables {
    # Chemins système
    system_root = "${env.SystemRoot}"           # C:\\\\Windows
    program_files = "${env.ProgramFiles}"       # C:\\\\Program Files
    app_data = "${env.APPDATA}"                # C:\\\\Users\\\\[User]\\\\AppData\\\\Roaming

    # Variables personnalisées
    tools_path = "%ProgramFiles%/Outils"
    temp_folder = "${env.TEMP}/Shell"
  }
}

```

## Manipulation de chaînes

```yaml
shell {
  context_menu {
    items = [
      # Exemple 1: Manipulation basique
      {
        title = "Nom du fichier: ${sel.name}"           # nom.txt
        title2 = "Extension: ${sel.ext}"                # txt
        title3 = "Chemin complet: ${sel.path}"          # C:\\\\...\\\\nom.txt
      }

      # Exemple 2: Fonctions de chaînes
      {
        title = "${string.upper(sel.name)}"             # NOM.TXT
        title2 = "${string.lower(sel.name)}"            # nom.txt
        title3 = "${string.length(sel.name)}"           # 7
      }

      # Exemple 3: Extraction et remplacement
      {
        title = "${string.substring(sel.name, 0, 3)}"   # nom
        title2 = "${string.replace(sel.name, '.', '_')}"# nom_txt
      }
    ]
  }
}

```

## Expressions conditionnelles

```yaml
shell {
  context_menu {
    items = [
      # Vérification d'extension
      {
        title = "Outils Image"
        visibility = "${sel.ext == 'png' || sel.ext == 'jpg'}"
      }

      # Vérification de chemin
      {
        title = "Actions système"
        visibility = "${string.startswith(sel.path, env.SystemRoot)}"
      }

      # Vérification multiple
      {
        title = "Actions spéciales"
        visibility = "${
          string.length(sel.name) > 5 &&
          sel.size < 1024000 &&
          string.contains(sel.path, 'Projects')
        }"
      }
    ]
  }
}

```

## Variables spéciales

```yaml
shell {
  context_menu {
    items = [
      # Variables de sélection
      {
        title = "Info fichier"
        command = "echo Fichier: ${sel.path}\\\\nTaille: ${sel.size}\\\\nDate: ${sel.date}"
      }

      # Variables d'environnement
      {
        title = "Ouvrir dossier utilisateur"
        command = "explorer.exe ${env.USERPROFILE}"
      }

      # Variables système
      {
        title = "Info système"
        command = "echo OS: ${sys.os}\\\\nVersion: ${sys.ver}\\\\nArch: ${sys.arch}"
      }
    ]
  }
}

```

## Expressions Numériques dans Shell

1. Opérations mathématiques de base
2. Fonctions numériques
3. Conversions et formatage
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations mathématiques
      {
        title = "Calculatrice"
        items = [
          {
            title = "Opérations basiques"
            command = "${
              var a = 10;
              var b = 5;
              msg.info('Calculs',
                'Addition: ' + (a + b) + '\\\\n' +
                'Soustraction: ' + (a - b) + '\\\\n' +
                'Multiplication: ' + (a * b) + '\\\\n' +
                'Division: ' + (a / b) + '\\\\n' +
                'Modulo: ' + (a % b)
              )
            }"
          },
          {
            title = "Puissance et racines"
            command = "${
              var x = 16;
              msg.info('Avancé',
                'Carré: ' + Math.pow(x, 2) + '\\\\n' +
                'Cube: ' + Math.pow(x, 3) + '\\\\n' +
                'Racine carrée: ' + Math.sqrt(x)
              )
            }"
          }
        ]
      },

      # 2. Fonctions mathématiques
      {
        title = "Fonctions Math"
        items = [
          {
            title = "Arrondis"
            command = "${
              var n = 3.14159;
              msg.info('Arrondis',
                'Round: ' + Math.round(n) + '\\\\n' +
                'Floor: ' + Math.floor(n) + '\\\\n' +
                'Ceil: ' + Math.ceil(n) + '\\\\n' +
                'Fixed(2): ' + n.toFixed(2)
              )
            }"
          },
          {
            title = "Min/Max"
            command = "${
              var nums = [1, 5, 3, 9, 2];
              msg.info('Extremes',
                'Minimum: ' + Math.min(...nums) + '\\\\n' +
                'Maximum: ' + Math.max(...nums)
              )
            }"
          }
        ]
      },

      # 3. Conversions
      {
        title = "Conversions"
        items = [
          {
            title = "Bases numériques"
            command = "${
              var dec = 255;
              msg.info('Conversions',
                'Décimal: ' + dec + '\\\\n' +
                'Hexadécimal: 0x' + dec.toString(16) + '\\\\n' +
                'Binaire: ' + dec.toString(2) + '\\\\n' +
                'Octal: ' + dec.toString(8)
              )
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Calcul taille fichier"
            command = "${
              var bytes = sel.size;
              var kb = bytes / 1024;
              var mb = kb / 1024;
              msg.info('Taille',
                'Bytes: ' + bytes + '\\\\n' +
                'KB: ' + kb.toFixed(2) + '\\\\n' +
                'MB: ' + mb.toFixed(2)
              )
            }"
          },
          {
            title = "Pourcentages"
            command = "${
              var total = 150;
              var value = 75;
              var percent = (value / total) * 100;
              msg.info('Pourcentage',
                value + ' sur ' + total + ' = ' +
                percent.toFixed(1) + '%'
              )
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions mathématiques principales :

- Opérateurs: `+`, `,` , `/`, `%`
- `Math.pow()` : Puissance
- `Math.sqrt()` : Racine carrée
- `Math.round()`, `Math.floor()`, `Math.ceil()`
- `Math.min()`, `Math.max()`
- `.toFixed()` : Formatage décimal
- `.toString(base)` : Conversion de base

## Opérateurs dans Shell

1. Opérateurs arithmétiques
2. Opérateurs de comparaison
3. Opérateurs logiques
4. Opérateurs d'assignation
5. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérateurs arithmétiques
      {
        title = "Calculs"
        items = [
          {
            title = "Arithmétique basique"
            command = "${
              var a = 10;
              var b = 3;
              msg.info('Opérations',
                'Addition: ' + (a + b) + '\\\\n' +
                'Soustraction: ' + (a - b) + '\\\\n' +
                'Multiplication: ' + (a * b) + '\\\\n' +
                'Division: ' + (a / b) + '\\\\n' +
                'Modulo: ' + (a % b) + '\\\\n' +
                'Incrément: ' + (++a) + '\\\\n' +
                'Décrément: ' + (--b)
              )
            }"
          }
        ]
      },

      # 2. Opérateurs de comparaison
      {
        title = "Comparaisons"
        items = [
          {
            title = "Tests"
            command = "${
              var x = 5;
              var y = 5;
              msg.info('Comparaisons',
                'Égal (==): ' + (x == y) + '\\\\n' +
                'Strictement égal (===): ' + (x === y) + '\\\\n' +
                'Différent (!=): ' + (x != 3) + '\\\\n' +
                'Supérieur (>): ' + (x > 4) + '\\\\n' +
                'Inférieur (<): ' + (x < 6) + '\\\\n' +
                'Supérieur ou égal (>=): ' + (x >= 5) + '\\\\n' +
                'Inférieur ou égal (<=): ' + (x <= 5)
              )
            }"
          }
        ]
      },

      # 3. Opérateurs logiques
      {
        title = "Logique"
        items = [
          {
            title = "Tests logiques"
            command = "${
              var a = true;
              var b = false;
              msg.info('Logique',
                'ET (&&): ' + (a && b) + '\\\\n' +
                'OU (||): ' + (a || b) + '\\\\n' +
                'NON (!): ' + (!a) + '\\\\n' +
                'Combiné: ' + (a && !b)
              )
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Vérification fichier"
            command = "${
              var size = sel.size;
              var isImage = sel.ext.image;
              var result =
                size > 0 && size < 1048576 && isImage ?
                'Image valide' :
                'Fichier non valide';
              msg.info('Vérification', result)
            }"
          },
          {
            title = "Calcul complexe"
            command = "${
              var value = sel.size;
              value += 1024;  // Addition
              value *= 2;     // Multiplication
              value /= 1024;  // Division
              msg.info('Résultat', value.toFixed(2) + ' KB')
            }"
          }
        ]
      }
    ]
  }
}

```

Opérateurs principaux :

- Arithmétiques : `+`, `,` , `/`, `%`, `++`, `-`
- Comparaison : `==`, `===`, `!=`, `>`, `<`, `>=`, `<=`
- Logiques : `&&`, `||`, `!`
- Assignation : `=`, `+=`, `=`, `=`, `/=`, `%=`
- Ternaire : `condition ? valeurSiVrai : valeurSiFaux`

## Nommage et Variables

1. Règles de nommage
2. Types d'identifiants
3. Variables et portée
4. Exemples pratiques

```yaml
shell {
  # 1. Déclaration de variables
  variables {
    # Identifiants valides
    userName = "John"           # Camel case
    user_age = 25              # Snake case
    _private = "hidden"        # Commence par underscore
    $special = "value"         # Commence par $
    counter123 = 0             # Alphanumérique
  }

  context_menu {
    items = [
      # 2. Utilisation des identifiants
      {
        title = "Variables"
        items = [
          {
            title = "Info utilisateur"
            command = "${
              # Accès aux variables
              msg.info('User',
                'Nom: ' + userName + '\\\\n' +
                'Age: ' + user_age
              )
            }"
          }
        ]
      },

      # 3. Portée des variables
      {
        title = "Portée"
        items = [
          {
            title = "Variables locales"
            command = "${
              var localVar = 'local';    # Variable locale
              let tempVar = 'temp';      # Variable temporaire
              const CONSTANT = 'fixed';   # Constante

              msg.info('Portée',
                'Local: ' + localVar + '\\\\n' +
                'Temp: ' + tempVar + '\\\\n' +
                'Constant: ' + CONSTANT
              )
            }"
          }
        ]
      },

      # 4. Exemples avancés
      {
        title = "Applications"
        items = [
          {
            title = "Compteur"
            command = "${
              # Incrémenter variable
              counter123++;
              msg.info('Compteur', counter123)
            }"
          },
          {
            title = "Configuration"
            command = "${
              # Objet avec identifiants
              var config = {
                appName: 'MyApp',
                version: '1.0',
                isDebug: true
              };

              msg.info('Config',
                json.stringify(config, null, 2)
              )
            }"
          }
        ]
      }
    ]
  }
}

```

Règles principales pour les identifiants :

- Commencent par lettre, _ ou $
- Peuvent contenir lettres, chiffres, _
- Sensibles à la casse
- Pas de mots-clés réservés
- Conventions de nommage :
    - camelCase
    - snake_case
    - PascalCase
    - UPPER_CASE (constantes)

## **Fonctions Shell avec Exemples Détaillés**

1. Fonctions système
2. Fonctions de fichiers
3. Fonctions de chaînes
4. Fonctions personnalisées

```yaml
shell {
  # 1. Fonctions système
  context_menu {
    items = [
      {
        title = "Info Système"
        where = "${sys.is.win11}" # Vérifie Windows 11
        items = [
          {
            title = "OS: ${sys.os.name} ${sys.os.ver}"
            title2 = "Architecture: ${sys.os.arch}"
            command = "systeminfo"
          }
        ]
      }
    ]
  }

  # 2. Fonctions de fichiers
  functions {
    # Vérification de fichiers
    check_python() => {
      return io.file.exists("python.exe")
    }

    # Taille lisible
    readable_size(bytes) => {
      return bytes < 1024 ? "${bytes} B" :
             bytes < 1048576 ? "${(bytes/1024).toFixed(2)} KB" :
             "${(bytes/1048576).toFixed(2)} MB"
    }
  }

  # 3. Exemples d'utilisation
  context_menu {
    items = [
      # Manipulation de fichiers
      {
        title = "Actions fichier"
        where = "sel.file"
        items = [
          {
            title = "Taille: ${readable_size(sel.size)}"
            title2 = "Date: ${sel.date.format('dd/MM/yyyy')}"
          }
        ]
      }

      # Fonctions de chaînes
      {
        title = "Manipulations texte"
        items = [
          {
            title = "${string.upper(sel.name)}"
            title2 = "${string.replace(sel.name, '.', '_')}"
            title3 = "${string.substring(sel.path, 0, 10)}..."
          }
        ]
      }

      # Conditions complexes
      {
        title = "Vérifications avancées"
        where = "${
          io.file.exists(sel.path) &&
          sel.size > 0 &&
          string.endswith(sel.name, '.txt')
        }"
        command = "notepad.exe \\\\"${sel.path}\\\\""
      }
    ]
  }
}

```

Les fonctions peuvent être :

- Intégrées (système, fichiers, chaînes)
- Personnalisées (définies par l'utilisateur)
- Utilisées dans les conditions et commandes
- Combinées pour des opérations complexes

## Gestion des Applications

1. Vérification des applications
2. Obtention d'informations
3. Gestion des chemins
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Vérification des applications
      {
        title = "Vérification Apps"
        items = [
          {
            title = "Apps installées"
            command = "${
              var apps = [
                'notepad++',
                'chrome',
                'vscode'
              ];

              apps.foreach(app => {
                msg.info(app,
                  'Installé: ' + app.installed(app) + '\\\\n' +
                  'Existe: ' + app.exists(app) + '\\\\n' +
                  'Version: ' + app.version(app)
                )
              })
            }"
          }
        ]
      },

      # 2. Informations applications
      {
        title = "Info Applications"
        items = [
          {
            title = "Détails Chrome"
            where = "${app.exists('chrome')}"
            command = "${
              msg.info('Chrome',
                'Chemin: ' + app.path('chrome') + '\\\\n' +
                'Version: ' + app.version('chrome') + '\\\\n' +
                'Éditeur: ' + app.publisher('chrome')
              )
            }"
          },
          {
            title = "VS Code"
            where = "${app.installed('code')}"
            command = "${
              var code = {
                path: app.path('code'),
                version: app.version('code'),
                install: app.install.path('code')
              };
              msg.info('VS Code', json.stringify(code, null, 2))
            }"
          }
        ]
      },

      # 3. Lancement d'applications
      {
        title = "Lancer Apps"
        items = [
          {
            title = "Ouvrir avec..."
            command = "${
              var apps = app.list();
              var choice = input.select(
                'Choisir application',
                apps
              );
              if (choice) {
                process.start(app.path(choice), sel.path)
              }
            }"
          }
        ]
      },

      # 4. Applications par défaut
      {
        title = "Apps par défaut"
        items = [
          {
            title = "Ouvrir avec défaut"
            command = "${
              var defaultApp = app.associated(sel.ext);
              if (defaultApp) {
                process.start(app.path(defaultApp), sel.path)
              }
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions app principales :

- `app.exists()` : Vérifie existence
- `app.installed()` : Vérifie installation
- `app.version()` : Version
- `app.path()` : Chemin complet
- `app.publisher()` : Éditeur
- `app.list()` : Liste applications
- `app.associated()` : App par défaut
- `app.install.path()` : Dossier installation

## Gestion des Applications Windows Store

1. Vérification des applications UWP
2. Informations sur les packages
3. Manipulation des apps Store
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Vérification des apps UWP
      {
        title = "Apps Windows Store"
        items = [
          {
            title = "Vérifier installation"
            command = "${
              var apps = [
                'Microsoft.WindowsTerminal',
                'Microsoft.WindowsCalculator',
                'Microsoft.ScreenSketch'
              ];

              apps.foreach(app => {
                msg.info(app,
                  'Installé: ' + appx.installed(app) + '\\\\n' +
                  'Version: ' + appx.version(app) + '\\\\n' +
                  'Nom: ' + appx.name(app)
                )
              })
            }"
          }
        ]
      },

      # 2. Informations détaillées
      {
        title = "Détails package"
        items = [
          {
            title = "Windows Terminal"
            where = "${appx.exists('Microsoft.WindowsTerminal')}"
            command = "${
              var info = {
                name: appx.name('Microsoft.WindowsTerminal'),
                publisher: appx.publisher('Microsoft.WindowsTerminal'),
                version: appx.version('Microsoft.WindowsTerminal'),
                path: appx.path('Microsoft.WindowsTerminal'),
                family: appx.family('Microsoft.WindowsTerminal')
              };
              msg.info('Terminal', json.stringify(info, null, 2))
            }"
          }
        ]
      },

      # 3. Liste et recherche
      {
        title = "Gestion packages"
        items = [
          {
            title = "Packages installés"
            command = "${
              appx.packages().foreach(pkg => {
                if (pkg.name.startsWith('Microsoft')) {
                  msg.info(pkg.name,
                    'Version: ' + pkg.version
                  )
                }
              })
            }"
          },
          {
            title = "Rechercher package"
            command = "${
              var search = input.text('Rechercher package');
              if (search) {
                var found = appx.find(search);
                if (found) {
                  msg.info('Trouvé',
                    'Nom: ' + found.name + '\\\\n' +
                    'Version: ' + found.version
                  )
                }
              }
            }"
          }
        ]
      },

      # 4. Lancement d'applications
      {
        title = "Lancer apps Store"
        items = [
          {
            title = "Ouvrir Terminal"
            where = "${appx.exists('Microsoft.WindowsTerminal')}"
            command = "${
              process.start(
                appx.path('Microsoft.WindowsTerminal'),
                '-d \\\\"' + sel.path + '\\\\"'
              )
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions AppX principales :

- `appx.exists()` : Vérifie existence
- `appx.installed()` : Vérifie installation
- `appx.version()` : Version
- `appx.name()` : Nom affiché
- `appx.publisher()` : Éditeur
- `appx.path()` : Chemin exécutable
- `appx.family()` : Famille de package
- `appx.packages()` : Liste tous les packages
- `appx.find()` : Recherche package

## Exécution de commandes

1. Exécution de commandes simples
2. Options d'exécution
3. Gestion des résultats
4. Exemples pratiques avancés

```yaml
shell {
  context_menu {
    items = [
      # 1. Commandes simples
      {
        title = "Commandes basiques"
        items = [
          {
            title = "Exécuter cmd"
            command = "${
              command.run('cmd', '/c dir')
            }"
          },
          {
            title = "PowerShell"
            command = "${
              command.shell('Get-Process')
            }"
          }
        ]
      },

      # 2. Options d'exécution
      {
        title = "Exécution avancée"
        items = [
          {
            title = "Mode masqué"
            command = "${
              command.hidden('ipconfig /all')
            }"
          },
          {
            title = "Mode élevé (Admin)"
            command = "${
              command.elevated('netstat -ab')
            }"
          }
        ]
      },

      # 3. Gestion des résultats
      {
        title = "Résultats"
        items = [
          {
            title = "Capture sortie"
            command = "${
              var result = command.output('systeminfo');
              msg.info('Résultat', result)
            }"
          },
          {
            title = "Vérifier code retour"
            command = "${
              var code = command.run('ping localhost');
              msg.info('Code retour', code)
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Git status"
            command = "${
              command.workdir(
                sel.path,
                'git status'
              )
            }"
          },
          {
            title = "Compilation"
            command = "${
              var result = command.run({
                cmd: 'gcc',
                args: ['-o', 'app.exe', 'main.c'],
                dir: sel.path,
                window: 'hidden'
              });

              msg.info(
                result == 0 ? 'Succès' : 'Erreur',
                'Code: ' + result
              )
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions command principales :

- `command.run()` : Exécute une commande
- `command.shell()` : Exécute via shell
- `command.hidden()` : Exécute en mode masqué
- `command.elevated()` : Exécute en admin
- `command.output()` : Capture la sortie
- `command.workdir()` : Définit répertoire de travail

Options d'exécution :

- `cmd` : Commande à exécuter
- `args` : Arguments
- `dir` : Répertoire de travail
- `window` : Mode d'affichage
- `wait` : Attente fin d'exécution

## **Fonctions d'Identification (ID) dans Shell**

1. Fonctions d'identification de base
2. Vérifications avancées
3. Combinaisons pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Fonctions d'identification de base
      {
        title = "Vérifications ID"
        items = [
          {
            title = "Est administrateur"
            where = "${id.is.admin}"
            icon = "shield"
          },
          {
            title = "Mode développeur"
            where = "${id.is.developer}"
          },
          {
            title = "Utilisateur: ${id.username}"
            where = "${id.exists}"
          }
        ]
      },

      # 2. Vérifications avancées
      {
        title = "Sécurité"
        where = "${id.is.admin || id.is.system}"
        items = [
          {
            title = "ID Complet: ${id.fullname}"
            command = "whoami /all"
          },
          {
            title = "Domaine: ${id.domain}"
            where = "${id.is.domain}"
          }
        ]
      },

      # 3. Combinaisons pratiques
      {
        title = "Actions système"
        where = "${
          (id.is.admin && id.is.elevated) ||
          id.is.system
        }"
        items = [
          {
            title = "Services système"
            command = "services.msc"
            visibility = "${id.is.admin}"
          },
          {
            title = "Outils admin"
            where = "${
              id.is.elevated &&
              id.username == 'Administrator'
            }"
          }
        ]
      }
    ]
  }
}

```

Variables importantes :

- `id.username` : Nom d'utilisateur actuel
- `id.domain` : Domaine Windows
- `id.is.admin` : Droits administrateur
- `id.is.elevated` : Processus élevé
- `id.is.system` : Compte système
- `id.is.developer` : Mode développeur activé

## **Fonctions IO dans Shell**

1. Fonctions de gestion de fichiers
2. Fonctions de gestion de dossiers
3. Opérations de lecture/écriture
4. Exemples pratiques combinés

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations sur les fichiers
      {
        title = "Gestion fichiers"
        items = [
          {
            title = "Vérifier existence"
            where = "${io.file.exists(sel.path)}"
            command = "echo Le fichier existe"
          },
          {
            title = "Taille: ${io.file.size(sel.path)}"
            where = "${io.file.size(sel.path) > 0}"
          },
          {
            title = "Attributs"
            where = "${!io.file.readonly(sel.path)}"
            items = [
              {
                title = "Rendre lecture seule"
                command = "${io.file.setreadonly(sel.path, true)}"
              }
            ]
          }
        ]
      },

      # 2. Opérations sur les dossiers
      {
        title = "Gestion dossiers"
        where = "${io.dir.exists(sel.path)}"
        items = [
          {
            title = "Liste fichiers"
            command = "${
              io.dir.files(sel.path, '*.txt').foreach(file => {
                io.file.copy(file, sel.path + '/backup/')
              })
            }"
          },
          {
            title = "Créer dossier"
            command = "${io.dir.create(sel.path + '/nouveau')}"
          }
        ]
      },

      # 3. Lecture/Écriture
      {
        title = "Opérations IO"
        items = [
          {
            title = "Lire contenu"
            command = "${
              var content = io.file.read(sel.path);
              io.file.write(sel.path + '.backup', content)
            }"
          },
          {
            title = "Ajouter texte"
            command = "${
              io.file.append(sel.path, '\\\\nNouvelle ligne')
            }"
          }
        ]
      },

      # 4. Exemples avancés
      {
        title = "Actions avancées"
        where = "${io.file.exists(sel.path)}"
        items = [
          {
            title = "Backup intelligent"
            command = "${
              var date = sys.date.now.format('yyyy-MM-dd');
              var backupDir = sel.dir + '/backup/' + date;
              io.dir.create(backupDir);
              io.file.copy(sel.path, backupDir + '/' + sel.name)
            }"
          },
          {
            title = "Analyse dossier"
            command = "${
              var total = 0;
              io.dir.files(sel.path).foreach(file => {
                total += io.file.size(file)
              });
              message('Taille totale: ' + total + ' octets')
            }"
          }
        ]
      }
    ]
  }
}

```

## **Fonctions Key dans Shell - Raccourcis clavier**

1. Définition des raccourcis simples
2. Combinaisons de touches
3. Raccourcis conditionnels
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Raccourcis simples
      {
        title = "Ouvrir avec Notepad"
        hotkey = "Ctrl+N"
        command = "notepad.exe \\\\"${sel.path}\\\\""
      },

      # 2. Combinaisons complexes
      {
        title = "Actions rapides"
        items = [
          {
            title = "Terminal (Alt+T)"
            hotkey = "Alt+T"
            command = "wt.exe -d \\\\"${sel.path}\\\\""
          },
          {
            title = "VS Code (Ctrl+Shift+C)"
            hotkey = "Ctrl+Shift+C"
            command = "code \\\\"${sel.path}\\\\""
          }
        ]
      },

      # 3. Raccourcis conditionnels
      {
        title = "Outils développeur"
        where = "${key.shift && key.ctrl}"
        items = [
          {
            title = "Git Status"
            hotkey = "Ctrl+Shift+G"
            command = "git status"
          }
        ]
      },

      # 4. Vérifications de touches
      {
        title = "Actions spéciales"
        items = [
          {
            title = "Mode debug"
            where = "${
              key.pressed('D') &&
              key.ctrl &&
              key.shift
            }"
            command = "devtools.exe"
          },
          {
            title = "Actions multiples"
            where = "${
              (key.alt && key.shift) ||
              (key.ctrl && key.pressed('M'))
            }"
            command = "multi-tool.exe"
          }
        ]
      }
    ]
  }

  # 5. Configuration globale des touches
  hotkeys {
    enabled = true
    commands = [
      {
        key = "Ctrl+Alt+T"
        command = "wt.exe"
      },
      {
        key = "Ctrl+Shift+E"
        command = "explorer.exe"
        when = "${sel.isdir}"
      }
    ]
  }
}

```

Touches disponibles :

- Modificateurs : `Ctrl`, `Alt`, `Shift`
- Touches spéciales : `F1-F12`, `Enter`, `Esc`
- Combinaisons : `Ctrl+Alt`, `Ctrl+Shift`
- Vérifications : `key.pressed()`, `key.ctrl`, `key.alt`

## **Fonctions Message (msg) dans Shell**

1. Messages simples
2. Messages personnalisés
3. Boîtes de dialogue
4. Messages conditionnels

```yaml
shell {
  context_menu {
    items = [
      # 1. Messages simples
      {
        title = "Notifications basiques"
        items = [
          {
            title = "Message info"
            command = "${msg.info('Information', 'Opération terminée')}"
          },
          {
            title = "Message erreur"
            command = "${msg.error('Erreur', 'Une erreur est survenue')}"
          },
          {
            title = "Message attention"
            command = "${msg.warning('Attention', 'Vérifiez vos données')}"
          }
        ]
      },

      # 2. Messages avec conditions
      {
        title = "Messages conditionnels"
        items = [
          {
            title = "Vérification taille"
            command = "${
              sel.size > 1048576 ?
                msg.warning('Fichier volumineux', 'Le fichier dépasse 1 Mo') :
                msg.info('Fichier OK', 'Taille correcte')
            }"
          }
        ]
      },

      # 3. Boîtes de dialogue
      {
        title = "Dialogues interactifs"
        items = [
          {
            title = "Confirmation"
            command = "${
              msg.question('Confirmation', 'Voulez-vous continuer?') ?
                msg.info('OK', 'Action confirmée') :
                msg.info('Annulé', 'Action annulée')
            }"
          },
          {
            title = "Choix multiple"
            command = "${
              var choix = msg.ask('Choisir une option',
                'Option 1|Option 2|Option 3');
              msg.info('Choix', 'Vous avez choisi: ' + choix)
            }"
          }
        ]
      },

      # 4. Messages avancés
      {
        title = "Messages avancés"
        items = [
          {
            title = "Message avec timeout"
            command = "${msg.show('Notification', 'Disparaît dans 3s', 3000)}"
          },
          {
            title = "Message avec icône"
            command = "${
              msg.custom({
                title: 'Message personnalisé',
                text: 'Texte avec icône',
                icon: 'info',
                buttons: 'ok|cancel'
              })
            }"
          }
        ]
      }
    ]
  }
}

```

Types de messages disponibles :

- `msg.info()` : Information
- `msg.error()` : Erreur
- `msg.warning()` : Avertissement
- `msg.question()` : Question
- `msg.ask()` : Choix multiple
- `msg.show()` : Message temporaire
- `msg.custom()` : Message personnalisé

## **Manipulation des chemins**

1. Manipulation des chemins
2. Extraction d'informations
3. Vérification des chemins
4. Opérations avancées

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations basiques sur les chemins
      {
        title = "Manipulations chemins"
        items = [
          {
            title = "Nom fichier: ${path.name(sel.path)}"
            command = "echo ${path.name(sel.path)}"
          },
          {
            title = "Extension: ${path.ext(sel.path)}"
            command = "echo ${path.ext(sel.path)}"
          },
          {
            title = "Dossier parent: ${path.parent(sel.path)}"
            command = "explorer.exe \\\\"${path.parent(sel.path)}\\\\""
          }
        ]
      },

      # 2. Transformations de chemins
      {
        title = "Transformations"
        items = [
          {
            title = "Chemin absolu"
            command = "${path.full(sel.path)}"
          },
          {
            title = "Chemin relatif"
            command = "${path.relative(sel.path, env.USERPROFILE)}"
          },
          {
            title = "Normaliser chemin"
            command = "${path.normalize(sel.path)}"
          }
        ]
      },

      # 3. Vérifications avancées
      {
        title = "Vérifications"
        items = [
          {
            title = "Est un chemin absolu?"
            where = "${path.is.absolute(sel.path)}"
          },
          {
            title = "Est un chemin UNC?"
            where = "${path.is.unc(sel.path)}"
          },
          {
            title = "Est un lecteur?"
            where = "${path.is.drive(sel.path)}"
          }
        ]
      },

      # 4. Opérations complexes
      {
        title = "Opérations avancées"
        items = [
          {
            title = "Combiner chemins"
            command = "${
              var base = path.parent(sel.path);
              var nouveau = path.combine(base, 'nouveau_dossier');
              msg.info('Nouveau chemin', nouveau)
            }"
          },
          {
            title = "Analyser chemin"
            command = "${
              var info = {
                racine: path.root(sel.path),
                dossier: path.dir(sel.path),
                nom: path.name(sel.path),
                ext: path.ext(sel.path)
              };
              msg.info('Informations', json.stringify(info))
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions path disponibles :

- `path.name()` : Nom du fichier
- `path.ext()` : Extension
- `path.parent()` : Dossier parent
- `path.full()` : Chemin absolu
- `path.relative()` : Chemin relatif
- `path.normalize()` : Normalisation
- `path.combine()` : Combinaison
- `path.is.absolute()` : Vérification chemin absolu
- `path.is.unc()` : Vérification UNC
- `path.is.drive()` : Vérification lecteur

## **Gestion des processus**

1. Gestion des processus
2. Vérification des processus
3. Manipulation avancée
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Gestion basique des processus
      {
        title = "Processus"
        items = [
          {
            title = "Lister processus actifs"
            command = "${
              process.list().foreach(p => {
                msg.info('Processus', p.name + ' (PID: ' + p.id + ')')
              })
            }"
          },
          {
            title = "Processus actuel"
            command = "${
              var p = process.current();
              msg.info('Info processus',
                'Nom: ' + p.name +
                '\\\\nPID: ' + p.id +
                '\\\\nChemin: ' + p.path
              )
            }"
          }
        ]
      },

      # 2. Vérifications de processus
      {
        title = "Vérifications"
        items = [
          {
            title = "Notepad est-il en cours?"
            where = "${process.exists('notepad.exe')}"
            command = "${msg.info('Notepad', 'Notepad est en cours')}"
          },
          {
            title = "Chrome en cours?"
            where = "${process.running('chrome')}"
            command = "${
              var count = process.count('chrome');
              msg.info('Chrome', count + ' instances en cours')
            }"
          }
        ]
      },

      # 3. Actions sur les processus
      {
        title = "Actions"
        items = [
          {
            title = "Démarrer Notepad"
            command = "${
              process.start('notepad.exe', sel.path)
            }"
          },
          {
            title = "Terminer processus"
            command = "${
              process.kill('notepad.exe');
              msg.info('Terminé', 'Notepad a été fermé')
            }"
          }
        ]
      },

      # 4. Actions avancées
      {
        title = "Actions avancées"
        items = [
          {
            title = "Démarrer avec options"
            command = "${
              process.start({
                file: 'cmd.exe',
                args: '/k echo Bonjour',
                window: 'hidden',
                wait: false
              })
            }"
          },
          {
            title = "Processus système"
            command = "${
              var systeme = process.list().filter(p => p.system);
              msg.info('Processus système',
                'Nombre: ' + systeme.length)
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions process principales :

- `process.list()` : Liste des processus
- `process.current()` : Processus actuel
- `process.exists()` : Vérification existence
- `process.running()` : Vérification exécution
- `process.count()` : Nombre d'instances
- `process.start()` : Démarrer processus
- `process.kill()` : Terminer processus

## **Manipulation du registre Windows**

1. Lecture du registre
2. Écriture dans le registre
3. Vérifications et suppressions
4. Exemples pratiques avancés

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations de lecture
      {
        title = "Lecture Registre"
        items = [
          {
            title = "Lire une valeur"
            command = "${
              var winver = reg.read('HKLM\\\\\\\\SOFTWARE\\\\\\\\Microsoft\\\\\\\\Windows NT\\\\\\\\CurrentVersion\\\\\\\\ProductName');
              msg.info('Windows Version', winver)
            }"
          },
          {
            title = "Vérifier clé"
            where = "${
              reg.exists('HKCU\\\\\\\\Software\\\\\\\\Microsoft\\\\\\\\Windows\\\\\\\\CurrentVersion\\\\\\\\Explorer')
            }"
          }
        ]
      },

      # 2. Opérations d'écriture
      {
        title = "Écriture Registre"
        where = "${id.is.admin}"
        items = [
          {
            title = "Créer une clé"
            command = "${
              reg.create('HKCU\\\\\\\\Software\\\\\\\\MonApp');
              msg.info('Créé', 'Clé créée avec succès')
            }"
          },
          {
            title = "Définir une valeur"
            command = "${
              reg.write('HKCU\\\\\\\\Software\\\\\\\\MonApp', 'Version', '1.0');
              reg.write('HKCU\\\\\\\\Software\\\\\\\\MonApp', 'InstallDate', sys.date.now)
            }"
          }
        ]
      },

      # 3. Gestion avancée
      {
        title = "Opérations avancées"
        items = [
          {
            title = "Supprimer clé"
            command = "${
              reg.delete('HKCU\\\\\\\\Software\\\\\\\\MonApp');
              msg.info('Supprimé', 'Clé supprimée')
            }"
          },
          {
            title = "Copier clé"
            command = "${
              reg.copy(
                'HKCU\\\\\\\\Software\\\\\\\\MonApp',
                'HKCU\\\\\\\\Software\\\\\\\\MonApp.backup'
              )
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Utilitaires Registre"
        items = [
          {
            title = "Vérifier installation"
            command = "${
              var apps = reg.keys('HKLM\\\\\\\\SOFTWARE\\\\\\\\Microsoft\\\\\\\\Windows\\\\\\\\CurrentVersion\\\\\\\\Uninstall');
              apps.foreach(app => {
                var name = reg.read(app + '\\\\\\\\DisplayName');
                if (name) msg.info('App installée', name);
              })
            }"
          },
          {
            title = "Sauvegarder paramètres"
            command = "${
              var settings = {
                theme: reg.read('HKCU\\\\\\\\Software\\\\\\\\Microsoft\\\\\\\\Windows\\\\\\\\CurrentVersion\\\\\\\\Themes\\\\\\\\Personalize\\\\\\\\AppsUseLightTheme'),
                startup: reg.exists('HKCU\\\\\\\\Software\\\\\\\\Microsoft\\\\\\\\Windows\\\\\\\\CurrentVersion\\\\\\\\Run\\\\\\\\MonApp')
              };
              io.file.write('settings_backup.json', json.stringify(settings))
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions registry principales :

- `reg.read()` : Lire une valeur
- `reg.write()` : Écrire une valeur
- `reg.exists()` : Vérifier existence
- `reg.create()` : Créer une clé
- `reg.delete()` : Supprimer une clé/valeur
- `reg.copy()` : Copier une clé
- `reg.keys()` : Lister les sous-clés

## **Manipulation des éléments sélectionnés**

1. Propriétés de base de sélection
2. Opérations sur fichiers sélectionnés
3. Filtres et conditions
4. Exemples avancés

```yaml
shell {
  context_menu {
    items = [
      # 1. Propriétés basiques de sélection
      {
        title = "Info sélection"
        items = [
          {
            title = "Chemin: ${sel.path}"
            title2 = "Nom: ${sel.name}"
            title3 = "Extension: ${sel.ext}"
          },
          {
            title = "Taille: ${sel.size} octets"
            title2 = "Date modification: ${sel.date.modified}"
          }
        ]
      },

      # 2. Vérifications de type
      {
        title = "Type de sélection"
        items = [
          {
            title = "Fichier"
            where = "${sel.isfile}"
          },
          {
            title = "Dossier"
            where = "${sel.isdir}"
          },
          {
            title = "Lien symbolique"
            where = "${sel.islink}"
          }
        ]
      },

      # 3. Filtres par extension
      {
        title = "Filtres fichiers"
        items = [
          {
            title = "Images"
            where = "${sel.ext.image}"
            command = "explorer.exe \\\\"${sel.path}\\\\""
          },
          {
            title = "Documents"
            where = "${
              sel.ext.matches('doc|docx|pdf|txt')
            }"
          }
        ]
      },

      # 4. Opérations avancées
      {
        title = "Actions avancées"
        items = [
          {
            title = "Multi-sélection"
            command = "${
              sel.count > 1 ?
                msg.info('Sélection multiple', sel.count + ' éléments') :
                msg.info('Sélection unique', sel.path)
            }"
          },
          {
            title = "Analyse sélection"
            command = "${
              var info = {
                count: sel.count,
                totalSize: sel.files.reduce((sum, f) => sum + f.size, 0),
                types: sel.files.map(f => f.ext).join(', ')
              };
              msg.info('Analyse', json.stringify(info, null, 2))
            }"
          }
        ]
      }
    ]
  }
}

```

Propriétés sel principales :

- `sel.path` : Chemin complet
- `sel.name` : Nom du fichier
- `sel.ext` : Extension
- `sel.size` : Taille
- `sel.date` : Dates (created, modified, accessed)
- `sel.isfile` : Est un fichier
- `sel.isdir` : Est un dossier
- `sel.count` : Nombre d'éléments sélectionnés
- `sel.files` : Liste des fichiers sélectionnés

## **Manipulation des chaînes**

1. Opérations basiques sur les chaînes
2. Recherche et remplacement
3. Formatage et conversion
4. Exemples pratiques avancés

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations basiques
      {
        title = "Manipulations chaînes"
        items = [
          {
            title = "Longueur: ${str.length(sel.name)}"
            command = "${
              var texte = sel.name;
              msg.info('Chaîne',
                'Longueur: ' + str.length(texte) + '\\\\n' +
                'Majuscules: ' + str.upper(texte) + '\\\\n' +
                'Minuscules: ' + str.lower(texte)
              )
            }"
          },
          {
            title = "Extraction"
            command = "${
              var nom = sel.name;
              msg.info('Extractions',
                'Début: ' + str.substring(nom, 0, 3) + '\\\\n' +
                'Fin: ' + str.substring(nom, -3) + '\\\\n' +
                'Milieu: ' + str.substring(nom, 2, 5)
              )
            }"
          }
        ]
      },

      # 2. Recherche et remplacement
      {
        title = "Recherche"
        items = [
          {
            title = "Opérations de recherche"
            command = "${
              var texte = sel.name;
              var recherche = 'test';
              msg.info('Recherche',
                'Contient: ' + str.contains(texte, recherche) + '\\\\n' +
                'Position: ' + str.index(texte, recherche) + '\\\\n' +
                'Remplacé: ' + str.replace(texte, recherche, 'DEMO')
              )
            }"
          },
          {
            title = "Vérifications"
            command = "${
              var nom = sel.name;
              msg.info('Vérifications',
                'Commence par: ' + str.startswith(nom, 'test') + '\\\\n' +
                'Termine par: ' + str.endswith(nom, '.txt') + '\\\\n' +
                'Est vide: ' + str.empty(nom)
              )
            }"
          }
        ]
      },

      # 3. Formatage
      {
        title = "Formatage"
        items = [
          {
            title = "Nettoyage"
            command = "${
              var texte = sel.name;
              msg.info('Nettoyage',
                'Sans espaces: ' + str.trim(texte) + '\\\\n' +
                'Sans accents: ' + str.normalize(texte) + '\\\\n' +
                'Capitalisé: ' + str.capitalize(texte)
              )
            }"
          },
          {
            title = "Format personnalisé"
            command = "${
              var format = 'Fichier: {0} - Taille: {1}';
              var resultat = str.format(format, sel.name, sel.size);
              msg.info('Format', resultat)
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions string principales :

- `str.length()` : Longueur
- `str.upper()` : Majuscules
- `str.lower()` : Minuscules
- `str.substring()` : Extraction
- `str.contains()` : Recherche
- `str.replace()` : Remplacement
- `str.startswith()` : Vérification début
- `str.endswith()` : Vérification fin
- `str.trim()` : Suppression espaces
- `str.format()` : Formatage

## **Interactions système**

1. Informations système
2. Date et heure
3. Variables d'environnement
4. Opérations système

```yaml
shell {
  context_menu {
    items = [
      # 1. Informations système
      {
        title = "Info Système"
        items = [
          {
            title = "OS: ${sys.os.name} ${sys.os.ver}"
            title2 = "Architecture: ${sys.os.arch}"
            title3 = "Build: ${sys.os.build}"
          },
          {
            title = "Mémoire"
            command = "${
              msg.info('Mémoire',
                'Total: ' + sys.memory.total + '\\\\n' +
                'Disponible: ' + sys.memory.available + '\\\\n' +
                'Utilisée: ' + sys.memory.used
              )
            }"
          }
        ]
      },

      # 2. Date et Heure
      {
        title = "Date/Heure"
        items = [
          {
            title = "${sys.date.now.format('dd/MM/yyyy HH:mm:ss')}"
            command = "${
              var date = sys.date.now;
              msg.info('Date',
                'Jour: ' + date.day + '\\\\n' +
                'Mois: ' + date.month + '\\\\n' +
                'Année: ' + date.year + '\\\\n' +
                'Heure: ' + date.hour + ':' + date.minute
              )
            }"
          },
          {
            title = "Calculs date"
            command = "${
              var date = sys.date.now;
              var hier = date.addDays(-1);
              var demain = date.addDays(1);
              msg.info('Dates',
                'Hier: ' + hier.format('dd/MM') + '\\\\n' +
                'Demain: ' + demain.format('dd/MM')
              )
            }"
          }
        ]
      },

      # 3. Variables environnement
      {
        title = "Variables Système"
        items = [
          {
            title = "Chemins système"
            command = "${
              msg.info('Chemins',
                'Windows: ' + sys.env.windir + '\\\\n' +
                'System32: ' + sys.env.SystemRoot + '\\\\\\\\System32' + '\\\\n' +
                'Temp: ' + sys.env.TEMP
              )
            }"
          },
          {
            title = "Variables utilisateur"
            command = "${
              msg.info('Utilisateur',
                'Profil: ' + sys.env.USERPROFILE + '\\\\n' +
                'Documents: ' + sys.env.USERPROFILE + '\\\\\\\\Documents' + '\\\\n' +
                'Bureau: ' + sys.env.USERPROFILE + '\\\\\\\\Desktop'
              )
            }"
          }
        ]
      },

      # 4. Opérations système
      {
        title = "Actions système"
        items = [
          {
            title = "Informations CPU"
            command = "${
              msg.info('CPU',
                'Processeurs: ' + sys.cpu.count + '\\\\n' +
                'Architecture: ' + sys.cpu.arch + '\\\\n' +
                'Utilisation: ' + sys.cpu.usage + '%'
              )
            }"
          },
          {
            title = "État système"
            command = "${
              msg.info('État',
                'Uptime: ' + sys.uptime + '\\\\n' +
                'Version Windows: ' + sys.os.ver + '\\\\n' +
                'Langue: ' + sys.locale
              )
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions système principales :

- `sys.os` : Informations OS
- `sys.date` : Date et heure
- `sys.env` : Variables d'environnement
- `sys.cpu` : Informations CPU
- `sys.memory` : État mémoire
- `sys.uptime` : Temps depuis démarrage
- `sys.locale` : Paramètres régionaux

## **Références contextuelles**

1. Utilisation basique de this
2. Propriétés d'éléments
3. Manipulation avancée
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Utilisation basique
      {
        title = "Propriétés de base"
        items = [
          {
            title = "Info élément"
            command = "${
              msg.info('Élément actuel',
                'Titre: ' + this.title + '\\\\n' +
                'Type: ' + this.type + '\\\\n' +
                'Position: ' + this.pos
              )
            }"
          },
          {
            title = "État actuel"
            command = "${
              msg.info('État',
                'Activé: ' + this.enabled + '\\\\n' +
                'Visible: ' + this.visible + '\\\\n' +
                'Sélectionné: ' + this.selected
              )
            }"
          }
        ]
      },

      # 2. Propriétés d'éléments
      {
        title = "Manipulation éléments"
        items = [
          {
            title = "Modifier propriétés"
            command = "${
              this.title = 'Nouveau titre';
              this.icon = 'new';
              this.enabled = true;
              msg.info('Modifié', 'Propriétés mises à jour')
            }"
          },
          {
            title = "Style dynamique"
            command = "${
              this.background = '#f0f0f0';
              this.foreground = '#000000';
              this.font.size = 12;
            }"
          }
        ]
      },

      # 3. Conditions et vérifications
      {
        title = "Vérifications"
        items = [
          {
            title = "Test type"
            where = "${this.type == 'item'}"
            command = "${
              msg.info('Type',
                'Est menu: ' + this.is.menu + '\\\\n' +
                'Est séparateur: ' + this.is.separator
              )
            }"
          },
          {
            title = "Position relative"
            command = "${
              msg.info('Position',
                'Index: ' + this.index + '\\\\n' +
                'Premier: ' + this.is.first + '\\\\n' +
                'Dernier: ' + this.is.last
              )
            }"
          }
        ]
      },

      # 4. Manipulation avancée
      {
        title = "Actions avancées"
        items = [
          {
            title = "Gestion parent/enfants"
            command = "${
              var info = {
                hasParent: this.parent != null,
                childCount: this.items.length,
                depth: this.level
              };
              msg.info('Structure', json.stringify(info))
            }"
          },
          {
            title = "Modification dynamique"
            command = "${
              if (this.is.menu) {
                this.items.add({
                  title: 'Nouvel élément',
                  command: 'echo Ajouté dynamiquement'
                });
              }
            }"
          }
        ]
      }
    ]
  }
}

```

Propriétés this principales :

- `this.title` : Titre de l'élément
- `this.type` : Type d'élément
- `this.enabled` : État activé/désactivé
- `this.visible` : Visibilité
- `this.selected` : État de sélection
- `this.index` : Position dans le menu
- `this.parent` : Élément parent
- `this.items` : Éléments enfants
- `this.level` : Niveau de profondeur
- `this.is.*` : Vérifications d'état

## **Gestion des utilisateurs**

1. Informations utilisateur
2. Vérifications des privilèges
3. Gestion des groupes
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Informations utilisateur de base
      {
        title = "Info Utilisateur"
        items = [
          {
            title = "Identité"
            command = "${
              msg.info('Utilisateur',
                'Nom: ' + user.name + '\\\\n' +
                'Domaine: ' + user.domain + '\\\\n' +
                'Complet: ' + user.fullname
              )
            }"
          },
          {
            title = "Profil"
            command = "${
              msg.info('Profil',
                'Dossier: ' + user.profile + '\\\\n' +
                'Documents: ' + user.documents + '\\\\n' +
                'Bureau: ' + user.desktop
              )
            }"
          }
        ]
      },

      # 2. Vérifications de privilèges
      {
        title = "Privilèges"
        items = [
          {
            title = "État Admin"
            command = "${
              msg.info('Droits',
                'Admin: ' + user.is.admin + '\\\\n' +
                'Élevé: ' + user.is.elevated + '\\\\n' +
                'Système: ' + user.is.system
              )
            }"
          },
          {
            title = "Actions Admin"
            where = "${user.is.admin}"
            items = [
              {
                title = "Ouvrir services"
                command = "services.msc"
              }
            ]
          }
        ]
      },

      # 3. Gestion des groupes
      {
        title = "Groupes"
        items = [
          {
            title = "Vérifier groupe"
            command = "${
              msg.info('Groupes',
                'Administrateurs: ' + user.in.group('Administrators') + '\\\\n' +
                'Utilisateurs: ' + user.in.group('Users') + '\\\\n' +
                'Remote Desktop: ' + user.in.group('Remote Desktop Users')
              )
            }"
          }
        ]
      },

      # 4. Chemins utilisateur
      {
        title = "Dossiers utilisateur"
        items = [
          {
            title = "Applications"
            command = "${
              var paths = {
                appData: user.appdata,
                local: user.localappdata,
                temp: user.temp
              };
              msg.info('Chemins', json.stringify(paths, null, 2))
            }"
          },
          {
            title = "Dossiers spéciaux"
            command = "${
              var folders = {
                downloads: user.downloads,
                pictures: user.pictures,
                music: user.music,
                videos: user.videos
              };
              msg.info('Dossiers', json.stringify(folders, null, 2))
            }"
          }
        ]
      }
    ]
  }
}

```

Propriétés user principales :

- `user.name` : Nom d'utilisateur
- `user.domain` : Domaine
- `user.fullname` : Nom complet
- `user.profile` : Dossier profil
- `user.is.admin` : Est administrateur
- `user.is.elevated` : A des droits élevés
- `user.in.group()` : Appartenance à un groupe
- Chemins spéciaux :
    - `user.desktop`
    - `user.documents`
    - `user.downloads`
    - `user.appdata`
    - `user.localappdata`
    - `user.temp`

## **Gestion des fenêtres**

1. Manipulation des fenêtres
2. États et propriétés
3. Actions sur les fenêtres
4. Exemples avancés

```yaml
shell {
  context_menu {
    items = [
      # 1. Manipulation des fenêtres
      {
        title = "Gestion fenêtres"
        items = [
          {
            title = "Info fenêtre active"
            command = "${
              msg.info('Fenêtre',
                'Titre: ' + window.active.title + '\\\\n' +
                'Classe: ' + window.active.class + '\\\\n' +
                'Process: ' + window.active.process
              )
            }"
          },
          {
            title = "Dimensions"
            command = "${
              var win = window.active;
              msg.info('Dimensions',
                'X: ' + win.x + '\\\\n' +
                'Y: ' + win.y + '\\\\n' +
                'Largeur: ' + win.width + '\\\\n' +
                'Hauteur: ' + win.height
              )
            }"
          }
        ]
      },

      # 2. États des fenêtres
      {
        title = "État fenêtre"
        items = [
          {
            title = "Vérifier état"
            command = "${
              var win = window.active;
              msg.info('État',
                'Visible: ' + win.visible + '\\\\n' +
                'Minimisée: ' + win.minimized + '\\\\n' +
                'Maximisée: ' + win.maximized + '\\\\n' +
                'Premier plan: ' + win.foreground
              )
            }"
          }
        ]
      },

      # 3. Actions sur les fenêtres
      {
        title = "Actions fenêtre"
        items = [
          {
            title = "Manipulation"
            items = [
              {
                title = "Minimiser"
                command = "${window.active.minimize()}"
              },
              {
                title = "Maximiser"
                command = "${window.active.maximize()}"
              },
              {
                title = "Restaurer"
                command = "${window.active.restore()}"
              },
              {
                title = "Fermer"
                command = "${window.active.close()}"
              }
            ]
          },
          {
            title = "Position/Taille"
            command = "${
              var win = window.active;
              win.move(0, 0);
              win.resize(800, 600);
            }"
          }
        ]
      },

      # 4. Exemples avancés
      {
        title = "Actions avancées"
        items = [
          {
            title = "Liste fenêtres"
            command = "${
              window.list().foreach(win => {
                if (win.visible)
                  msg.info('Fenêtre', win.title)
              })
            }"
          },
          {
            title = "Organiser fenêtres"
            command = "${
              var wins = window.list();
              var x = 0;
              wins.foreach(win => {
                if (win.visible) {
                  win.move(x, 0);
                  win.resize(800, 600);
                  x += 820;
                }
              })
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions window principales :

- `window.active` : Fenêtre active
- `window.list()` : Liste des fenêtres
- Propriétés :
    - `title` : Titre
    - `class` : Classe
    - `process` : Processus
    - `x`, `y` : Position
    - `width`, `height` : Dimensions
    - `visible`, `minimized`, `maximized` : États
- Actions :
    - `minimize()` : Minimiser
    - `maximize()` : Maximiser
    - `restore()` : Restaurer
    - `close()` : Fermer
    - `move()` : Déplacer
    - `resize()` : Redimensionner

## **Gestion du presse-papiers**

1. Opérations basiques de copier/coller
2. Manipulation du contenu
3. Vérifications du presse-papiers
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Opérations basiques
      {
        title = "Presse-papiers"
        items = [
          {
            title = "Copier chemin"
            command = "${clipboard.copy(sel.path)}"
          },
          {
            title = "Coller contenu"
            command = "${
              var texte = clipboard.text;
              msg.info('Contenu', texte)
            }"
          }
        ]
      },

      # 2. Manipulation avancée
      {
        title = "Manipulations"
        items = [
          {
            title = "Format personnalisé"
            command = "${
              var chemin = sel.path;
              var format = 'Fichier: {0}\\\\nTaille: {1}';
              clipboard.copy(
                str.format(format, chemin, sel.size)
              )
            }"
          },
          {
            title = "Multi-lignes"
            command = "${
              clipboard.copy([
                'Ligne 1',
                'Ligne 2',
                'Ligne 3'
              ].join('\\\\n'))
            }"
          }
        ]
      },

      # 3. Vérifications
      {
        title = "Vérifications"
        items = [
          {
            title = "Contient texte?"
            command = "${
              msg.info('Presse-papiers',
                'Vide: ' + clipboard.empty + '\\\\n' +
                'Contient texte: ' + clipboard.has.text + '\\\\n' +
                'Contient fichiers: ' + clipboard.has.files
              )
            }"
          },
          {
            title = "Liste fichiers"
            where = "${clipboard.has.files}"
            command = "${
              var files = clipboard.files;
              files.foreach(f =>
                msg.info('Fichier', f)
              )
            }"
          }
        ]
      },

      # 4. Actions pratiques
      {
        title = "Actions avancées"
        items = [
          {
            title = "Copier avec format"
            command = "${
              if (sel.isfile) {
                var info = {
                  path: sel.path,
                  size: sel.size,
                  date: sel.date.modified
                };
                clipboard.copy(json.stringify(info, null, 2))
              }
            }"
          },
          {
            title = "Traitement texte"
            command = "${
              var texte = clipboard.text;
              if (!clipboard.empty) {
                texte = str.trim(texte);
                texte = str.upper(texte);
                clipboard.copy(texte);
                msg.info('Modifié', 'Texte transformé')
              }
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions clipboard principales :

- `clipboard.copy()` : Copier dans le presse-papiers
- `clipboard.text` : Obtenir le texte
- `clipboard.files` : Liste des fichiers
- `clipboard.empty` : Vérifier si vide
- `clipboard.has.text` : Contient du texte
- `clipboard.has.files` : Contient des fichiers

## **Interaction utilisateur**

1. Saisies utilisateur basiques
2. Dialogues d'entrée avancés
3. Validation des entrées
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Saisies basiques
      {
        title = "Entrées utilisateur"
        items = [
          {
            title = "Saisie simple"
            command = "${
              var nom = input.text('Votre nom');
              msg.info('Bonjour', 'Bienvenue ' + nom)
            }"
          },
          {
            title = "Saisie avec valeur par défaut"
            command = "${
              var valeur = input.text('Entrez une valeur', 'défaut');
              msg.info('Saisi', valeur)
            }"
          }
        ]
      },

      # 2. Dialogues avancés
      {
        title = "Dialogues"
        items = [
          {
            title = "Choix multiple"
            command = "${
              var choix = input.select(
                'Choisissez une option',
                ['Option 1', 'Option 2', 'Option 3']
              );
              msg.info('Sélection', choix)
            }"
          },
          {
            title = "Confirmation"
            command = "${
              if (input.confirm('Êtes-vous sûr?')) {
                msg.info('Confirmé', 'Action validée')
              }
            }"
          }
        ]
      },

      # 3. Validation d'entrées
      {
        title = "Validation"
        items = [
          {
            title = "Saisie avec validation"
            command = "${
              var numero;
              do {
                numero = input.text('Entrez un nombre');
              } while (!str.isnumber(numero));
              msg.info('Valide', 'Nombre saisi: ' + numero)
            }"
          },
          {
            title = "Saisie obligatoire"
            command = "${
              var texte = input.text('Champ requis');
              if (str.empty(texte)) {
                msg.error('Erreur', 'Saisie obligatoire');
                return;
              }
              msg.info('OK', 'Saisi: ' + texte)
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Renommer fichier"
            command = "${
              var nouveau = input.text(
                'Nouveau nom',
                sel.name
              );
              if (!str.empty(nouveau)) {
                io.file.rename(sel.path, sel.dir + '/' + nouveau)
              }
            }"
          },
          {
            title = "Configuration"
            command = "${
              var config = {
                nom: input.text('Nom du projet'),
                type: input.select('Type', ['Web', 'Desktop', 'Mobile']),
                debug: input.confirm('Mode debug?')
              };
              msg.info('Config', json.stringify(config, null, 2))
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions input principales :

- `input.text()` : Saisie de texte
- `input.select()` : Sélection dans une liste
- `input.confirm()` : Dialogue de confirmation
- Options :
    - Valeur par défaut
    - Validation
    - Messages personnalisés

## **Gestion des fichiers de configuration**

1. Lecture de fichiers INI
2. Écriture dans fichiers INI
3. Manipulation des sections
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Lecture INI
      {
        title = "Lecture INI"
        items = [
          {
            title = "Lire valeur"
            command = "${
              var config = 'config.ini';
              var valeur = ini.read(config, 'Section', 'Clé');
              msg.info('Lecture', valeur)
            }"
          },
          {
            title = "Lire section"
            command = "${
              var sections = ini.sections('config.ini');
              sections.foreach(section => {
                msg.info('Section', section)
              })
            }"
          }
        ]
      },

      # 2. Écriture INI
      {
        title = "Écriture INI"
        items = [
          {
            title = "Écrire valeur"
            command = "${
              ini.write('config.ini', 'App', 'Version', '1.0');
              ini.write('config.ini', 'App', 'Date', sys.date.now)
            }"
          },
          {
            title = "Créer section"
            command = "${
              ini.write('config.ini', 'NewSection', 'Key1', 'Value1');
              ini.write('config.ini', 'NewSection', 'Key2', 'Value2')
            }"
          }
        ]
      },

      # 3. Manipulation avancée
      {
        title = "Opérations avancées"
        items = [
          {
            title = "Vérifier existence"
            command = "${
              var hasSection = ini.exists('config.ini', 'Section');
              var hasKey = ini.exists('config.ini', 'Section', 'Key');
              msg.info('Vérification',
                'Section existe: ' + hasSection + '\\\\n' +
                'Clé existe: ' + hasKey
              )
            }"
          },
          {
            title = "Supprimer entrées"
            command = "${
              ini.delete('config.ini', 'Section', 'Key');
              ini.delete('config.ini', 'Section')
            }"
          }
        ]
      },

      # 4. Exemples pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Gérer configuration"
            command = "${
              // Sauvegarder préférences
              var config = {
                theme: 'dark',
                language: 'fr',
                autoSave: true
              };

              Object.keys(config).foreach(key => {
                ini.write('app.ini', 'Settings', key, config[key])
              });

              // Lire configuration
              var savedConfig = {};
              ini.keys('app.ini', 'Settings').foreach(key => {
                savedConfig[key] = ini.read('app.ini', 'Settings', key)
              });

              msg.info('Config', json.stringify(savedConfig, null, 2))
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions INI principales :

- `ini.read()` : Lire une valeur
- `ini.write()` : Écrire une valeur
- `ini.sections()` : Lister les sections
- `ini.keys()` : Lister les clés
- `ini.exists()` : Vérifier existence
- `ini.delete()` : Supprimer entrée/section

## **Expressions régulières**

1. Recherche avec regex
2. Remplacement avec regex
3. Validation avec regex
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Recherche regex
      {
        title = "Recherche Regex"
        items = [
          {
            title = "Recherche simple"
            command = "${
              var texte = sel.name;
              var pattern = '^[a-z]+\\\\\\\\d+';
              var match = regex.match(texte, pattern);
              msg.info('Recherche',
                'Correspond: ' + match.success + '\\\\n' +
                'Trouvé: ' + match.value
              )
            }"
          },
          {
            title = "Recherche globale"
            command = "${
              var texte = sel.name;
              var matches = regex.matches(texte, '\\\\\\\\w+');
              matches.foreach(m => {
                msg.info('Trouvé', m.value)
              })
            }"
          }
        ]
      },

      # 2. Remplacement regex
      {
        title = "Remplacement"
        items = [
          {
            title = "Remplacer motif"
            command = "${
              var texte = sel.name;
              var nouveau = regex.replace(
                texte,
                '\\\\\\\\d+',
                'NUM'
              );
              msg.info('Remplacé', nouveau)
            }"
          },
          {
            title = "Remplacement multiple"
            command = "${
              var texte = sel.name;
              var nouveau = regex.replace(
                texte,
                '[^a-zA-Z]',
                '_',
                'g'
              );
              msg.info('Nettoyé', nouveau)
            }"
          }
        ]
      },

      # 3. Validation regex
      {
        title = "Validation"
        items = [
          {
            title = "Vérifier format"
            command = "${
              var patterns = {
                email: '^[\\\\\\\\w.-]+@[\\\\\\\\w.-]+\\\\\\\\.\\\\\\\\w+$',
                date: '^\\\\\\\\d{4}-\\\\\\\\d{2}-\\\\\\\\d{2}$',
                phone: '^\\\\\\\\+?\\\\\\\\d{10,}$'
              };

              var texte = input.text('Texte à vérifier');
              Object.keys(patterns).foreach(type => {
                var valid = regex.test(texte, patterns[type]);
                msg.info(type, 'Valide: ' + valid)
              })
            }"
          }
        ]
      },

      # 4. Applications pratiques
      {
        title = "Applications"
        items = [
          {
            title = "Extraire infos"
            command = "${
              var nom = sel.name;
              var pattern = '(\\\\\\\\w+)_(\\\\\\\\d{4})(\\\\\\\\..+)$';
              var match = regex.match(nom, pattern);

              if (match.success) {
                msg.info('Extraction',
                  'Base: ' + match.groups[1] + '\\\\n' +
                  'Année: ' + match.groups[2] + '\\\\n' +
                  'Extension: ' + match.groups[3]
                )
              }
            }"
          },
          {
            title = "Renommer fichiers"
            command = "${
              sel.files.foreach(file => {
                var nouveau = regex.replace(
                  file.name,
                  '\\\\\\\\s+',
                  '_'
                );
                io.file.rename(file.path, file.dir + '/' + nouveau)
              })
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions regex principales :

- `regex.match()` : Première correspondance
- `regex.matches()` : Toutes les correspondances
- `regex.replace()` : Remplacement
- `regex.test()` : Test de validation
- Options :
    - `g` : Global
    - `i` : Insensible à la casse
    - `m` : Multilignes

## **Manipulation d'images**

1. Lecture d'informations sur les images
2. Manipulation d'images
3. Vérifications de format
4. Exemples pratiques

```yaml
shell {
  context_menu {
    items = [
      # 1. Informations image
      {
        title = "Info Image"
        where = "${sel.file.ext.image}"
        items = [
          {
            title = "Propriétés image"
            command = "${
              var info = image.info(sel.path);
              msg.info('Image',
                'Largeur: ' + info.width + '\\\\n' +
                'Hauteur: ' + info.height + '\\\\n' +
                'Format: ' + info.format + '\\\\n' +
                'BPP: ' + info.bpp
              )
            }"
          },
          {
            title = "Dimensions"
            command = "${
              var dim = image.size(sel.path);
              msg.info('Dimensions',
                dim.width + ' x ' + dim.height
              )
            }"
          }
        ]
      },

      # 2. Manipulation d'images
      {
        title = "Actions image"
        where = "${sel.file.ext.image}"
        items = [
          {
            title = "Redimensionner"
            command = "${
              var size = image.size(sel.path);
              var newWidth = size.width / 2;
              var newHeight = size.height / 2;

              image.resize(
                sel.path,
                sel.dir + '/resized_' + sel.name,
                newWidth,
                newHeight
              )
            }"
          },
          {
            title = "Rotation"
            command = "${
              image.rotate(
                sel.path,
                sel.dir + '/rotated_' + sel.name,
                90
              )
            }"
          }
        ]
      },

      # 3. Vérifications format
      {
        title = "Vérifications"
        items = [
          {
            title = "Est une image?"
            command = "${
              msg.info('Vérification',
                'Image: ' + image.is.valid(sel.path) + '\\\\n' +
                'PNG: ' + image.is.png(sel.path) + '\\\\n' +
                'JPG: ' + image.is.jpg(sel.path)
              )
            }"
          },
          {
            title = "Qualité"
            where = "${image.is.jpg(sel.path)}"
            command = "${
              var quality = image.quality(sel.path);
              msg.info('Qualité JPEG', quality + '%')
            }"
          }
        ]
      },

      # 4. Traitement par lot
      {
        title = "Traitement multiple"
        where = "${sel.count > 1}"
        items = [
          {
            title = "Redimensionner tout"
            command = "${
              sel.files.foreach(file => {
                if (image.is.valid(file.path)) {
                  var size = image.size(file.path);
                  image.resize(
                    file.path,
                    file.dir + '/thumb_' + file.name,
                    size.width * 0.5,
                    size.height * 0.5
                  )
                }
              })
            }"
          }
        ]
      }
    ]
  }
}

```

Fonctions image principales :

- `image.info()` : Information complète
- `image.size()` : Dimensions
- `image.resize()` : Redimensionner
- `image.rotate()` : Rotation
- `image.is.valid()` : Vérifier format
- `image.is.png()`, `image.is.jpg()` : Vérifier type spécifique
- `image.quality()` : Qualité JPEG