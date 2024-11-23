# Souris
* [mouse](#mouse-1)
* [click](#mouseclick-button-)
* [moveto](#mousemoveto-x-y-)
* [moveby](#mousemoveby-x-y-)
* [moveraw](#mousemoveraw-x-y-)
* [double](#mousedouble-button-)
* [down](#mousedown-button-)
* [up](#mouseup-button-)
* [vscroll](#mousevscroll-amount-)
* [hscroll](#mousehscroll-amount-)
* [position](#mouseposition)



## mouse
La bibliothèque souris fournit des actions pour simuler des entrées de souris. Consultez la [liste des boutons](/res/buttons.md).

````lua
local ms = libs.mouse;
````



### mouse.click( [button] )
Effectue un clic simple (bouton gauche par défaut).

````lua
ms.click();
ms.click("right");
````



### mouse.moveto( x, y )
Déplace le curseur de la souris à l'emplacement spécifié (coordonnées de l'écran).

````lua
ms.moveto(100, 200);
````



### mouse.moveby( dx, dy )
Déplace le curseur de la souris de la quantité spécifiée (coordonnées de l'écran).

````lua
ms.moveby(50, -50);
````



### mouse.moveraw( dx, dy )
Déplace le curseur de la souris de la quantité spécifiée (entrée brute).

````lua
ms.moveraw(-10, 5);
````



### mouse.double( [button] )
Effectue un double clic (bouton gauche par défaut).

````lua
ms.double();
ms.double("right");
````



### mouse.down( [button] )
Appuie sur le bouton de la souris jusqu'à ce que ``mouse.up`` soit appelé (bouton gauche par défaut).

````lua
ms.down();
ms.down("right");
````



### mouse.up( [button] )
Relâche le bouton de la souris (bouton gauche par défaut).

````lua
ms.up();
ms.up("right");
````



### mouse.vscroll( amount )
Défile verticalement de la quantité spécifiée.

````lua
ms.vscroll(10);
ms.vscroll(-10);
````



### mouse.hscroll( amount )
Défile horizontalement de la quantité spécifiée.

````lua
ms.hscroll(10);
ms.hscroll(-10);
````



### mouse.position()
Retourne la position actuelle du curseur de la souris.

````lua
x,y = ms.position();
````


