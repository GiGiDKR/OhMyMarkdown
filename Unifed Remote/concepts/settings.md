# Paramètres

Les télécommandes peuvent également avoir un fichier de paramètres qui fournit des paramètres de configuration pour l'implémentation de la télécommande.
Cela facilite la configuration de paramètres tels que, par exemple, les détails de connexion nécessaires au fonctionnement d'une télécommande. Il peut
également être utilisé pour le stockage (par exemple, les valeurs mises en cache ou l'état précédent).


## Format

Le format est ``clé: valeur``.

    clé1: valeur1
	clé2: valeur2
	clé3: valeur3


## Emplacement

Les paramètres doivent être stockés dans un fichier appelé ``settings.prop`` dans le répertoire de la télécommande.

	Télécommandes/
	├── Foo/
	│   ├── meta.prop
	│   ├── remote.lua
	│   ├── layout.xml
	│   ├── icon.png
	│   ├── settings.prop


## Utilisation

Il est automatiquement généré si vous définissez des paramètres depuis votre télécommande.

    actions.foo = function ()
        local foo = settings.foo;
        settings.foo = "bar";
    end

Référez-vous à la bibliothèque [settings](../libs/settings.md) pour plus de détails.


## Valeurs par défaut

Le gestionnaire de serveur détecte si un fichier de paramètres est disponible pour une télécommande. Cela permet de modifier
les paramètres de la télécommande depuis le gestionnaire. Pour activer cela, les paramètres par défaut doivent être spécifiés pour la télécommande (les valeurs
peuvent être vides cependant).

    nom_utilisateur:
    mot_de_passe:
    port: 5432

