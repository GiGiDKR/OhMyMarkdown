# Télécommande

Le fichier de script de la télécommande contient l'implémentation de la fonctionnalité de la télécommande écrite en langage de script Lua.
Le fichier de script de la télécommande contient les gestionnaires d'événements qui se produisent.
Par exemple, lorsque la télécommande est créée ou détruite, ou lorsqu'elle gagne ou perd le focus.

	-- Événements
	events.create = function ()
		-- charger une ressource...
	end

	events.focus = function ()
		-- démarrer des minuteries...
	end

	events.blur = function ()
		-- arrêter des minuteries...
	end

	events.destroy = function ()
		-- décharger des ressources...
	end

Le fichier de script contient également les gestionnaires d'actions. Ceux-ci implémentent la fonctionnalité que les télécommandes peuvent effectuer,
et la fonctionnalité à laquelle d'autres télécommandes (ou Widgets ou Actions Rapides dans l'application) peuvent se lier.

	-- Actions
	actions.foo = function ()
		-- Ma fonction foo...
	end

	actions.bar = function ()
		-- Ma fonction bar...
	end

	actions.foo_bar = function ()
		-- Ma fonction foo bar...
	end

Vous pouvez avoir autant d'actions que vous le souhaitez, et vous pouvez les nommer comme vous le souhaitez (tant qu'elles sont des littéraux Lua légaux).
Nous vous recommandons d'utiliser des noms en minuscules avec un trait de soulignement (_) pour séparer les mots.

## Métadonnées d'aide
Pour permettre à l'application de savoir ce qu'une action fait, il est important d'ajouter des métadonnées à chaque action. Il existe deux types différents de métadonnées qui peuvent être envoyées à l'application. Le premier est une description de ce qu'une action fait.
```lua
--@help <Description de l'action>
```
Le deuxième type est le type de paramètres que l'action accepte et une description pour chaque paramètre. Il peut y avoir de nombreux paramètres différents.
```lua
--@param <nom du paramètre>:<type> <description du paramètre>
--@param <nom du paramètre>:<type2> <description 2 du paramètre>
```
Il existe 10 types différents de paramètres.
```
string:   une chaîne
strings:  tableau de chaînes
button:   un bouton de souris
buttons:  tableau de boutons de souris
key:	  une touche de clavier
keys: 	  tableau de touches de clavier
enum(item1,item2): une valeur d'un énum
enums(item1,item2): tableau de valeurs d'un énum
number:   une valeur numérique
numbers:  tableau de valeurs numériques
```

Exemple de toutes les informations d'aide utilisées dans le fichier de la télécommande :
```lua
--@help string test
--@param s:string c'est une chaîne
actions.string = function(s)
end

--@help strings test
--@param ss:strings ce sont des chaînes
actions.strings = function(ss)
end

--@help button test
--@param bt:button c'est un bouton
actions.button = function(bt)
end

--@help buttons test
--@param bts:buttons ce sont des boutons
actions.buttons = function(bts)
end

--@help key test
--@param k:key c'est une touche
actions.key = function(k)
end

--@help keys test
--@param ks:keys ce sont des touches
actions.keys = function(ks)
end

--@help enum(hello,hi) test
--@param e:enum(hello,hi) c'est un énum
actions.enum = function(e)
end

--@help enums(hello,hi) test
--@param es:enums(hello,hi) ce sont des énums
actions.enums = function(es)
end

--@help number test
--@param n:number c'est un nombre
actions.number = function(n)
end

--@help numbers test
--@param ns:numbers ce sont des nombres
actions.numbers = function(ns)
end
```
