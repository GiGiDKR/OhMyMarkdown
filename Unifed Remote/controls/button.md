# Bouton
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [alignement du texte](#alignement-du-texte)
	* [icône](#icône)
	* [échelle](#échelle)
	* [image](#image)
* [Style](#style)
* [Événements](#événements)
	* [ontap](#ontap)
	* [onhold](#onhold)
	* [ondown](#ondown)
	* [onup](#onup)



## Aperçu
Les boutons sont des contrôles simples qui peuvent être pressés.

````xml
<button text="appuyez sur moi!" ontap="foobar" />
````

````lua
actions.foobar = function ()
	print("vous avez appuyé sur un bouton!");
end
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).

````xml
<button id="my_btn" />
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<button visibility="gone" />
````



### texte
Définir le texte à afficher dans le bouton.

````xml
<button text="bonjour le monde" />
````



### alignement du texte
Définir l'alignement horizontal du texte en utilisant ``left`` ou ``center`` ou ``right``.

````xml
<button text="foo" textalign="right" />
````



### icône
Définir une icône de contrôle standard. Voir [liste des icônes](../res/icons.md).

````xml
<button icon="select" />
````


### image
Définir une image personnalisée à utiliser. Doit être un chemin absolu ou relatif au fichier de mise en page.

````xml
<button image="img.png" />
````



### échelle
Définit l'échelle utilisée pour les images. Valeurs : ``icon`` (par défaut), ``fill``, ``fit`` ou ``native``.

````xml
<button image="img.png" scale="fit" />
````

<img src="http://s3.amazonaws.com/unifiedremote-community-uploads/6774bef3-d6db-453f-8f10-16af2fdd3d29.png" width="200" />


## Style
Voir la page [style](../concepts/styling.md#style) pour plus de détails.



## Événements



### ontap
Se produit lorsque le bouton est tapé.

````xml
<button text="foo" ontap="foo_tapped" />
````

````lua
actions.foo_tapped = function ()
    ...
end
````



### onhold
Se produit lorsque le bouton est maintenu enfoncé.

````xml
<button text="bar" onhold="bar_held" />
````

````lua
actions.bar_held = function ()
    ...
end
````



### ondown
Se produit lorsque le bouton est pressé.

````xml
<button text="hello" ondown="hello_down" />
````

````lua
actions.hello_down = function ()
    ...
end
````



### onup
Se produit lorsque le bouton est relâché.

````xml
<button text="world" onup="world_up" />
````

````lua
actions.world_up = function ()
    ...
end
````


