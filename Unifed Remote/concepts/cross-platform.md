# Multi-plateforme

## Métadonnées

Certaines télécommandes peuvent être implémentées pour fonctionner sur tous les systèmes d'exploitation (Windows, Linux, Mac OS X). Cependant, certaines télécommandes peuvent ne fonctionner que pour un système d'exploitation spécifique. Cela peut être contrôlé en spécifiant le champ ``meta.platform`` dans le fichier méta de la télécommande :

	# uniquement pour Windows
	meta.platform: windows

Il peut également spécifier plusieurs systèmes d'exploitation autorisés.

	# pour Windows et Linux
	meta.platform: windows linux


## Qualificateurs

Un autre scénario est celui où vous souhaitez prendre en charge plusieurs systèmes d'exploitation, mais avez besoin de différentes implémentations pour certains systèmes d'exploitation.
Cela peut être contrôlé en utilisant des qualificateurs dans les noms de fichiers de la télécommande. L'exemple suivant montre comment vous
pourriez avoir une implémentation par défaut plus une implémentation spécifique pour Mac OS X.

	Télécommandes/
		Exemple/
			meta.prop
			remote.lua
			remote_osx.lua
			layout.xml
			icon.png

Vous pouvez également spécifier une implémentation différente pour chaque système d'exploitation :

	Télécommandes/
		Exemple/
			meta.prop
			remote_win.lua
			remote_osx.lua
			remote_linux.lua
			layout.xml
			icon.png

Les qualificateurs de fichiers peuvent également être appliqués aux fichiers de mise en page, de propriétés et d'icônes.