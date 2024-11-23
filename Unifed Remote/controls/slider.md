# Curseur
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [progression](#progression)
	* [progressionmax](#progressionmax)
* [Style](#style)
* [Événements](#événements)
	* [onchange](#onchange)
	* [ondone](#ondone)
	* [ondown](#ondown)
	* [onup](#onup)

## Aperçu
Les curseurs peuvent être utilisés pour afficher ou obtenir une progression.

````xml
<slider text="position" progress="50" progressmax="100" onchange="update" />
````

````lua
actions.update = function (progress)
    print("la progression a été changée à " .. progress);
end
````

## Propriétés

### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md).

````xml
<slider id="my_slider" text="foo" />
````

### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<slider visibility="gone" />
````

### texte
Définir le texte supplémentaire à afficher dans le curseur.

````xml
<slider text="bonjour le monde" progress="50" progressmax="100" />
````

affichera :

bonjour le monde - 50%

Si vous ne spécifiez pas de ``texte``, seul le pourcentage sera affiché :

50%

### progression
Définir la valeur de progression actuelle du curseur.

````xml
<slider progress="99" />
````

### progressionmax
Définir la valeur de progression maximale du curseur (par défaut ``100``).

````xml
<slider progressmax="200" />
````

## Style
Voir la page [style](./styling.md) pour plus de détails.

## Événements

### onchange
Se produit lorsque la progression du curseur change.

````xml
<slider onchange="changing" />
````

````lua
actions.changing = function (value)
    ...
end
````

### ondone
Se produit lorsque le curseur a fini de changer de valeur.

````xml
<slider ondone="finish" />
````

````lua
actions.finish = function (value)
    ...
end
````

### ondown
Se produit lorsque le curseur est pressé (c'est-à-dire commence à glisser).

````xml
<slider ondown="start" />
````

````lua
actions.start = function (value)
    ...
end
````

### onup
Se produit lorsque le curseur est relâché (c'est-à-dire arrête de glisser).

````xml
<slider onup="stop" />
````

````lua
actions.stop = function (value)
    ...
end
````


