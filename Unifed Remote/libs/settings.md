# Paramètres
* [settings](#settings-1)
* [get](#get)
* [set](#set)
	


## settings
La bibliothèque ``settings`` peut être utilisée pour obtenir et définir des données que vous souhaitez stocker.

La bibliothèque ``settings`` est globale et n'a pas besoin d'être importée.



### get
Les paramètres sont facilement lus en utilisant le global ``settings``.

````lua
print("the port is " .. settings.port);
````

Pour les clés contenant des espaces ou d'autres noms/caractères invalides :

````lua
settings["foo bar 123"];
````



### set
Les paramètres peuvent tout aussi facilement être modifiés.

````lua
settings.port = 8080;
````

Pour les clés contenant des espaces ou d'autres noms/caractères invalides :

````lua
settings["foo bar 123"] = "hello world!";
````
