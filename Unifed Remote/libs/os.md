# OS
* [os](#os-1)
* [extensions](#extensions)
  * [sleep](#ossleep-time-)
  * [open](#osopen-path-args-)
  * [openall](#osopenall-path-)
  * [start](#osstart-command-arg1-arg2--)
  * [script](#osscript-script-)
  * [throw](#osthrow-message-)



## os
La bibliothèque ``os`` est une bibliothèque Lua standard. C'est une bibliothèque globale et n'a pas besoin d'être importée.

Consultez la [documentation officielle de Lua](http://www.lua.org/manual/5.1/) pour plus de détails.

```lua
os.clock();
```



## extensions

La bibliothèque ``os`` a été étendue avec quelques fonctions supplémentaires.



### os.sleep( time )
Suspend l'exécution pendant ``time`` millisecondes.

```lua
os.sleep(1000);
```


### os.open( path, [args] )
Ouvre le fichier spécifié en utilisant le programme par défaut. Si le chemin est un script ou un exécutable, il l'exécutera dans une nouvelle fenêtre. Sous Windows, il utilise ``ShellExecute`` en interne.

```lua
os.open("C:\\file.txt");
```

Il peut également être utilisé pour ouvrir un dossier sur votre bureau.

```lua
os.open("C:\\foo\\");
```


### os.openall( path )
Ouvre tous les fichiers en utilisant le programme par défaut dans le dossier spécifié (par exemple, tous les fichiers musicaux dans un dossier).

```lua
os.openall("C:\\foo\\");
```


### os.start( command, [arg1], [arg2], [...] )
Démarre le processus ou le programme spécifié par ``command``. Il s'exécute sans attendre la fin du processus ni capturer la sortie ou le code de résultat. Pour cela, utilisez plutôt la fonction standard ``os.execute``.

```lua
os.start("foobar.exe");
```

Sous Windows, ``command`` est également comparé aux applications installées.

```lua
os.start("spotify");
```

Des arguments peuvent également être passés :

```lua
os.start("ipconfig", "/all");
```



### os.script( script )
Alias pour [script.default](script.md#scriptdefault-).

```lua
os.script("echo \"foo\"");
```



### os.throw( message )
Génère une erreur et arrête l'action en cours.

```lua
os.throw("something bad happened >.<");
```


