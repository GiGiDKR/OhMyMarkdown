# Structure

Les télécommandes sont organisées en répertoires :

	Télécommandes/
	├── Foo/
	│   ├── meta.prop
	│   ├── remote.lua
	│   ├── layout.xml
	│   ├── icon.png
	├── Bar/
	│   ├── meta.prop
	│   ├── remote.lua
	│   ├── layout.xml
	│   ├── icon.png
	...

Au démarrage, le serveur analyse un ensemble de répertoires de télécommandes configurés. Le serveur recherche des répertoires contenant des fichiers ``meta.prop``.

Les noms de fichiers indiqués ci-dessus sont les noms par défaut que le serveur recherche. Cependant, ils peuvent également être remplacés dans le fichier meta.

