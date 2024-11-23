# Texte
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [alignement du texte](#alignement-du-texte)
	* [icône](#icône)
	* [image](#image)
* [Style](#style)
* [Événements](#événements)
	* [onchange](#onchange)
	* [ondone](#ondone)


## Aperçu
Le contrôle ``text`` est utilisé pour éditer la saisie de texte.

````xml
<text hint="enter value" onchange="update" />
````

````lua
actions.update = function (text)

end
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).

````xml
<text id="my_txt" />
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<text visibility="gone" />
````



### texte
Définir le texte actuel à afficher.

````xml
<text text="hello world" />
````



### alignement du texte
Définir l'alignement horizontal du texte en utilisant ``left`` ou ``center`` ou ``right``.

````xml
<text textalign="right" />
````



### hint
Définir l'indice de l'espace réservé (texte à afficher lorsqu'il est vide).

````xml
<text hint="enter here" />
````



### multiline
Définir si le contrôle accepte ou non la saisie multilignes (par défaut ``false``).

````xml
<text multiline="true" />
````



## Style
Voir la page [style](../concepts/styling.md#style) pour plus de détails.



## Événements



### onchange
Se produit lorsque le texte change.

````xml
<text onchange="changed" />
````

````lua
actions.changed = function (text)
    ...
end
````



### ondone
Se produit lorsque l'édition se termine.

````xml
<text ondone="done" />
````

````lua
actions.done = function (text)
    ...
end
````


