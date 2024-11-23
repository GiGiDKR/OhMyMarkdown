# Modèle de base

Créez un dossier pour votre télécommande et ajoutez 3 fichiers : un fichier ``meta.prop``, un fichier ``layout.xml`` et un fichier ``remote.lua``.

	Foo/
	├── meta.prop
	├── remote.lua
	├── layout.xml

<h3>meta.prop</h3>

Le fichier meta décrit quelques informations de base sur la télécommande.

	meta.name: <nom de la télécommande>
	meta.author: <votre nom>
	meta.description: <écrivez votre description ici>

<ct>meta.prop</ct>

<h3>layout.xml</h3>

Le fichier de mise en page définit l'apparence de la télécommande. En général, il s'agit de quelques lignes de contrôles.

// ...existing code...

<ct>remote.lua</ct>
```
<ct>layout.xml</ct>

<h3>remote.lua</h3>

Le fichier de télécommande définit ce que chaque contrôle doit faire. Notez comment la valeur dans les champs ``ontap`` correspond aux noms des actions.

	kb = libs.keyboard;
	script = libs.script;

	--@help Lancer l'application
	actions.launch = function ()
		os.start("foo.exe");
	end

	--@help Exemple ouvrir un fichier
	actions.open = function ()
		os.open("data.txt");
	end

	--@help Exemple de script shell
	actions.doit = function ()
		script.shell("echo foobar");
	end

	--@help Exemple de frappe de touche
	actions.home = function ()
		kb.stroke("ctrl", "h");
	end

<ct>remote.lua</ct>