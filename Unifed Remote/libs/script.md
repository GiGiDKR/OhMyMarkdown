# Script
* [script](#script-1)
* [batch](#)
* [powershell](#)
* [applescript](#)
* [shell](#)
* [default](#)



## script
La bibliothèque ``script`` facilite l'exécution de scripts système à distance.

````lua
local script = libs.script;
````

Toutes les fonctions de script acceptent une ou plusieurs lignes pour faciliter l'écriture de scripts plus longs.

````lua
output = script.apple(
	"tell application \"Spotify\"",
		"set out to player state",
	"end tell"
);
````

Les fonctions de script renvoient 3 valeurs :

````lua
out,err,res = script.default(...);
````

Vous pouvez facilement exécuter des scripts à partir de fichiers en utilisant la bibliothèque ``fs`` :

````lua
local src = libs.fs.read("foo.bat");
script.batch(src);
````



### script.batch( [...] )
Exécute un script Windows Batch.

````lua
cd = script.batch("echo %cd%");
````



### script.powershell( [...] )
Exécute un script Windows PowerShell.

````lua
process_list = script.powershell(
	"ps | Where-Object { $_.Name -eq \"svchost\" }"
);
````



### script.apple( [...] )
Exécute un AppleScript.

````lua
path = script.apple("set out to (path to me)");
````



### script.shell( [...] )
Exécute un script shell en utilisant l'interpréteur par défaut (typiquement ``sh``).
 
 ````lua
foo = script.shell("echo $PWD");
````


Vous pouvez spécifier un interpréteur différent avec une ligne shebang :

````lua
foo = script.shell(
	"#!/bin/bash",
	"echo $PWD"
);
````


Notez que sous Windows, la fonction ``shell`` crée un fichier Batch.

````lua
foo = script.shell("echo %USERNAME%");
````



### script.default( line, [...] )
Exécute le script par défaut selon la plateforme.

* Windows: ``script.batch``.
* Mac OS X: ``script.apple``.
* Linux/Unix: ``script.shell``.

