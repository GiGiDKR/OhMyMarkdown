# Serveur
* [server](#server-1)
* [load](#serverload-id-)
* [unload](#serverunload-id-)
* [run](#serverrun-id-action-extra--)
* [update](#serverupdate-update-update--)
	


## server
La bibliothèque ``server`` fournit des fonctions d'aide pour interagir avec le serveur et d'autres télécommandes.

````lua
local server = require("server");
````



### server.load( id )
Demande au serveur de charger (créer) la télécommande spécifiée.

````lua
server.load("Unified.Chrome");
````



### server.unload( id )
Demande au serveur de décharger (détruire) la télécommande spécifiée.

````lua
server.unload("Unified.Chrome");
````



### server.run( id, action [,extra, ...] )
Demande au serveur d'exécuter une action pour la télécommande spécifiée.

````lua
server.run("Unified.Chrome", "back");
server.run("Unified.Command", "execute", "echo foobar");
````

Le serveur chargera automatiquement (créera) la télécommande.



### server.update( update [,update, ...] )
Effectue une ou plusieurs mises à jour de la disposition pour la télécommande active.

````lua
server.update(
	{ id = "info", text = "foobar" },
	{ id = "tgl", checked = true }
);
````

Pour des mises à jour simples, vous pouvez utiliser la bibliothèque d'aide [layout](#layout.md).

Cette fonction doit être utilisée pour effectuer des mises à jour avancées telles que des listes et des dialogues. Voir [ici](../controls/dialogs.md).
