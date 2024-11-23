# Toucher
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [image](#image)
* [Style](#style)
* [Événements](#événements)
	* [ontap](#ontap)
	* [onhold](#onhold)
	* [ondoubletap](#ondoubletap)
	* [ondown](#ondown)
	* [onup](#onup)
	* [ontouchsize](#ontouchsize)
	* [ontouchstart](#ontouchstart)
	* [ontouchdelta](#ontouchdelta)
	* [ontouchabs](#ontouchabs)
	* [ontouchend](#ontouchend)
	* [onmultitap](#onmultitap)



## Aperçu
Le contrôle ``touch`` peut être utilisé pour recevoir des événements multi-touch.

````xml
<touch text="toucher ici!" ontouchabs="moved" />
````

````lua
actions.moved = function (id, x, y)
    print("point de toucher " .. id .. " à " .. x .. " " .. y);
end
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).

````xml
<touch id="my_touch" />
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<touch visibility="gone" />
````



### texte
Définir le texte à afficher en arrière-plan.

````xml
<touch text="bonjour le monde" />
````



### image
Définir l'image de fond.

````xml
<touch image="bg.png" />
````


## Style
Voir la page [style](../concepts/styling.md) pour plus de détails.



## Événements



### ontap
Se produit lorsque la zone de toucher est tapée.

````xml
<touch ontap="tapped" />
````

````lua
actions.tapped = function ()
    ...
end
````



### onhold
Se produit lorsque la zone de toucher est maintenue enfoncée.

````xml
<touch onhold="held" />
````

````lua
actions.held = function ()
    ...
end
````



### ondoubletap
Se produit lorsque la zone de toucher est double tapée.

````xml
<touch ondoubletap="double" />
````

````lua
actions.double = function ()
    ...
end
````



### ondown
Se produit lorsque le toucher commence.

````xml
<touch ondown="down" />
````

````lua
actions.down = function ()
    ...
end
````



### onup
Se produit lorsque le toucher se termine.

````xml
<touch onup="up" />
````

````lua
actions.up = function ()
    ...
end
````



### ontouchsize
Se produit lorsque la taille de la zone de toucher change.

````xml
<touch ontouchsize="touch_size" />
````

````lua
actions.touch_size = function (w, h, oldw, oldh)
    ...
end
````



### ontouchstart
Se produit lorsqu'un événement multi-touch commence (id est l'identifiant du pointeur).

````xml
<touch ontouchstart="touch_start" />
````

````lua
actions.touch_start = function (id, x, y)
    ...
end
````



### ontouchdelta
Se produit lors d'un mouvement multi-touch (id est l'identifiant du pointeur).

````xml
<touch ontouchdelta="touch_delta" />
````

````lua
actions.touch_delta = function (id, deltax, deltay)
    ...
end
````



### ontouchabs
Se produit lors d'un mouvement multi-touch (id est l'identifiant du pointeur).

````xml
<touch ontouchabs="touch_abs" />
````

````lua
actions.touch_abs = function (id, absx, absy)
    ...
end
````



### ontouchend
Se produit lorsqu'un événement multi-touch se termine (id est l'identifiant du pointeur).

````xml
<touch ontouchend="touch_end" />
````

````lua
actions.touch_end = function (id, x, y)
    ...
end
````



### onmultitap
Se produit lorsqu'un tap multi-touch se produit avec n doigts.

````xml
<touch onmultitap="multitap" />
````

````lua
actions.multitap = function (n)
    ...
end
````


