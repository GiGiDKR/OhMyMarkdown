# Étiquette
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
	* [ontap](#ontap)
	* [onhold](#onhold)
	* [ondown](#ondown)
	* [onup](#onup)



## Aperçu
Les étiquettes affichent du texte mais peuvent également être pressées.

````xml
<label text="appuyez sur moi!" ontap="foobar" />
````

````lua
actions.foobar = function ()
    print("vous avez appuyé sur une étiquette!");
end
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).

````xml
<label id="my_lbl" text="foo" />
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<label visibility="gone" />
````



### texte
Définir le texte à afficher.

````xml
<label text="bonjour le monde" />
````



### alignement du texte
Définir l'alignement horizontal du texte en utilisant ``left`` ou ``center`` ou ``right``.

````xml
<label text="foo" textalign="right" />
````


### icône
Définir une icône de contrôle standard. Voir [liste des icônes](../res/icons.md) des icônes disponibles.

````xml
<button icon="select" />
````



### image
Définir une image personnalisée à utiliser. Doit être un chemin absolu ou relatif au fichier de mise en page.

````xml
<button image="img.png" />
````



## Style
Voir la page [style](../concepts/styling.md) pour plus de détails.



## Événements



### ontap
Se produit lorsque le contrôle est tapé.

````xml
<label text="foo" ontap="foo_tapped" />
````

````lua
actions.foo_tapped = function ()
    ...
end
````



### onhold
Se produit lorsque le contrôle est maintenu enfoncé.

````xml
<label text="bar" onhold="bar_held" />
````

````lua
actions.bar_held = function ()
    ...
end
````



### ondown
Se produit lorsque le contrôle est pressé.

````xml
<label text="hello" ondown="hello_down" />
````

````lua
actions.hello_down = function ()
    ...
end
````



### onup
Se produit lorsque le contrôle est relâché.

````xml
<label text="world" onup="world_up" />
````

````lua
actions.world_up = function ()
    ...
end
````


