# Basculer
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [alignement du texte](#alignement-du-texte)
	* [icône](#icône)
	* [image](#image)
	* [checked](#checked)
* [Style](#style)
* [Événements](#événements)
	* [onchange](#onchange)
	* [ontap](#ontap)
	* [onhold](#onhold)
	* [ondown](#ondown)
	* [onup](#onup)



## Aperçu
Les bascules sont des boutons qui peuvent avoir deux états (activé ou désactivé).

````xml
<toggle text="change me!" checked="true" onchange="foobar" />
````

````lua
actions.changed = function (checked)
    print("vous avez changé l'état de la bascule à " .. checked);
end
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md).

````xml
<toggle id="my_toggle" />
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<toggle visibility="gone" />
````



### texte
Définir le texte à afficher.

````xml
<toggle text="hello world" />
````



### alignement du texte
Définir l'alignement horizontal du texte en utilisant ``left`` ou ``center`` ou ``right``.

````xml
<toggle text="foo" textalign="right" />
````



### icône
Définir une icône de contrôle standard. Voir [liste des icônes](../res/icons.md) des icônes disponibles.

````xml
<toggle icon="select" />
````



### image
Définir une image personnalisée à utiliser. Doit être un chemin relatif au fichier de mise en page.

````xml
<toggle image="img.png" />
````



### checked
Définir si la bascule est activée (``true``) ou désactivée (``false``).

````xml
<toggle checked="true" />
````



## Style
Voir la page [style](../concepts/styling.md) pour plus de détails.



## Événements



### onchange
Se produit lorsque la bascule change d'état.

````xml
<toggle onchange="changed" />
````

````lua
actions.changed = function (checked)
    ...
end
````



### ontap
Se produit lorsque le contrôle est tapé.

````xml
<toggle text="foo" ontap="foo_tapped" />
````

````lua
actions.foo_tapped = function ()
    ...
end
````



### onhold
Se produit lorsque le contrôle est maintenu enfoncé.

````xml
<toggle text="bar" onhold="bar_held" />
````

````lua
actions.bar_held = function ()
    ...
end
````



### ondown
Se produit lorsque le contrôle est pressé.

````xml
<toggle text="hello" ondown="hello_down" />
````

````lua
actions.hello_down = function ()
    ...
end
````



### onup
Se produit lorsque le contrôle est relâché.

````xml
<toggle text="world" onup="world_up" />
````

````lua
actions.world_up = function ()
    ...
end
````