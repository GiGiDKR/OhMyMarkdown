# Journal
* [log](#log)
* [trace](#logtrace-message-)
* [info](#loginfo-message-)
* [warn](#logwarn-message-)
* [error](#logerror-message-)



## log
La bibliothèque ``log`` peut être utilisée pour la journalisation de diagnostics.

````lua
local log = require("log");
````



### log.trace( message )
Enregistre un message de niveau trace (généralement utilisé pour le débogage).

````lua
log.trace("quelque chose s'est passé");
````



### log.info( message )
Enregistre un message de niveau information pour la journalisation normale.

````lua
log.info("quelque chose de vraiment excitant s'est passé! :D");
````



### log.warn( message )
Enregistre un message de niveau avertissement (problèmes importants non critiques).

````lua
log.warn("quelque chose de mauvais s'est passé, mais nous pouvons récupérer :)");
````



### log.error( message )
Enregistre un message de niveau erreur (problèmes critiques).

````lua
log.error("quelque chose de vraiment mauvais s'est passé! >.<");
````


