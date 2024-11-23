# Métadonnées

Chaque télécommande doit avoir un fichier méta. Un exemple typique de fichier méta est montré ci-dessous

	meta.name: Foo Bar Remote
	meta.author: Awesome Remote Developer
	meta.description: Une télécommande fantastique pour foo bar.
	meta.url: http://awesome-remote-developer.com/

Le fichier méta peut également remplacer les noms de fichiers par défaut pour les scripts, les mises en page, les paramètres et les icônes :

	meta.remote: foo.lua
	meta.layout: foo.xml
	meta.icon: foo.png
	meta.settings: foo.prop

D'autres champs méta incluent :

	meta.platform: windows linux mac
	meta.enabled: true/false
	meta.hidden: true/false
	meta.version: 1
	meta.friendly: un nom convivial pour la voix
	meta.instance: single/multi
	meta.start: auto/manual
