# UIA
* [root](#uiaroot)
* [desktop](#uiadesktop)
* [focused](#uiafocused)
* [frompoint](#uiafrompoint)
* [fromhandle](#uiafromhandle)
* [find](#uiafind)
* [findby](#uiafindby)
* [child](#uiachild)
* [children](#uiachildren)
* [property](#uiaproperty)
* [name](#uianame)
* [properties](#uiaproperties)
* [firstchild](#uiafirstchild)
* [lastchild](#uialastchild)
* [nextsibling](#uianextsibling)
* [previoussibling](#uiaprevioussibling)
* [setvalue](#uiasetvalue)
* [dodefaultaction](#uiadodefaultaction)
* [toggle](#uiatoggle)
* [rangesetvalue](#uiarangesetvalue)


## uia
La bibliothèque ``uia`` fournit un accès à l'API d'automatisation de Windows.

	local uia = libs.uia;

Astuce : Inspect Objects est un utilitaire utile (inclus dans le SDK Windows).


### uia.root()
Retourne l'élément d'automatisation racine.

	root = uia.root();



### uia.desktop()
Retourne l'élément d'automatisation du bureau.

	desktop = uia.desktop();



### uia.focused()
Retourne l'élément d'automatisation actuellement focalisé.

	focused = uia.focused();



### uia.frompoint( x, y )
Retourne l'élément d'automatisation aux coordonnées d'écran spécifiées.

	element = uia.frompoint(123, 456);



### uia.fromhandle( hwnd )
Retourne l'élément d'automatisation pour le handle de fenêtre spécifié.

	hwnd = win.find("some_class_name", nil);
	element = uia.fromhandle(hwnd);



### uia.find( element, name [, scope] )
Trouve le premier élément avec le nom donné. La portée par défaut est les enfants.

	-- Trouve le premier enfant du bureau nommé "Netflix".
	desktop = uia.desktop();
	netflix = uia.find(desktop, "Netflix");

Les portées valides sont : ``ancestors``, ``children``, ``descendants``, ``element``, ``parent``, ``subtree``.

	-- Trouve le premier élément dans tout le sous-arbre de netflix nommé "PauseResume"
	uia.find(netflix, "PauseResume", "subtree");

Avertissement : Évitez d'utiliser subtree sur de grandes hiérarchies car cela peut prendre beaucoup de temps.



### uia.findby( element, property, type, value [, scope] )
Trouve le premier élément avec la valeur donnée pour le nom de propriété donné. La portée par défaut est les enfants.

	desktop = uia.desktop();
	foo = uia.findby(desktop, "ProcessId", "int", 3196);

Les types pris en charge sont : ``string``, ``double``, ``float``, ``int``, ``bool``, ``long``.



### uia.child( parent, index )
Retourne l'élément enfant à l'index donné (notez l'index 0).

	desktop = uia.desktop();
	first = uia.child(desktop, 0);



### uia.children( parent )
Retourne un tableau de tous les éléments enfants pour le parent donné.

	desktop = uia.desktop();
	children = uia.children(desktop);



### uia.property( element, name )
Retourne la valeur du nom de propriété spécifié.

	desktop = uia.desktop();
	name = uia.property(name);



### uia.name( element )
Retourne le nom de l'élément donné.

	desktop = uia.desktop();
	name = uia.name(desktop);



### uia.properties( e )
Retourne une table de propriétés pour l'élément donné.

	desktop = uia.desktop();
	props = uia.properties(desktop);



### uia.firstchild( element )
Retourne le premier enfant (ou nil) de l'élément spécifié.

	desktop = uia.desktop();
	first = uia.firstchild(desktop);



### uia.lastchild( element )
Retourne le dernier enfant (ou nil) de l'élément spécifié.

	desktop = uia.desktop();
	last = uia.lastchild(desktop);



### uia.nextsibling( element )
Retourne le frère suivant (ou nil) de l'élément spécifié.

	desktop = uia.desktop();
	next = uia.nextsibling(desktop);



### uia.previoussibling( element )
Retourne le frère précédent (ou nil) de l'élément spécifié.

	desktop = uia.desktop();
	previous = uia.previoussibling(desktop);


	
### uia.setvalue( element, value )
Définit la valeur d'un élément qui implémente le ValuePattern.

	element = ...;
	uia.setvalue(element, 50);



### uia.dodefaultaction( element )
Effectue l'action par défaut d'un élément qui implémente le LegacyAccessibilityPattern.

	element = ...;
	uia.dodefaultaction(element);



### uia.toggle( element )
Bascule l'état d'un élément qui implémente le TogglePattern.

	element = ...;
	uia.toggle(element);



### uia.rangesetvalue( element, value )
Définit la valeur de la plage d'un élément qui implémente le RangeValuePattern.

	element = ...;
	uia.setrangevalue(element, 50);











