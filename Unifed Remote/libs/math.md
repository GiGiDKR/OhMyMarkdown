# Math
* [math](#math-1)
* [extensions](#extensions)
* [round](#math-round-x-)


## math
La bibliothèque ``math`` est une bibliothèque Lua standard. C'est une bibliothèque globale et n'a pas besoin d'être importée.

````lua
print(math.abs(-123));  -- 123
````

Consultez la [documentation officielle de Lua](http://www.lua.org/manual/5.1/) pour plus de détails.



## extensions

La bibliothèque ``math`` a été étendue avec quelques fonctions supplémentaires.



### math.round( x )
Arrondit la valeur ``x`` à l'entier le plus proche (arrondit 0.5 vers le haut).

````lua
print(math.round(1.25));  -- 1
print(math.round(1.5));	  -- 2
print(math.round(1.75));  -- 2
````

