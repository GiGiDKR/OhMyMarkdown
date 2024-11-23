# URI
Ce document décrit la syntaxe des URI de l'application. Ces URI sont utilisés pour les Widgets, les Actions Rapides et pour contrôler
l'application Unified Remote depuis d'autres applications (par exemple Tasker). Ils sont disponibles pour Android et iOS pour le moment.

* [Syntaxe](#syntaxe)
* [Afficher](#afficher-dans-lapplication)
* [Télécommandes et Actions](#télécommandes-et-actions)
* [Actions de l'appareil](#actions-de-lappareil)
* [Changer de serveur](#changer-de-serveur)


## Syntaxe

Le schéma utilisé pour les URI Unified Remote est ``ur`` et le premier segment doit être ``intent``. Cela est suivi par une ou plusieurs paires clé-valeur,
qui définissent ce que la commande URI doit faire.

    ur://intent/key1:value1/key2:value2/...


## Afficher dans l'application
La commande ``show`` peut être utilisée pour ouvrir l'application, ou ouvrir des écrans spécifiques dans l'application.

    ur://intent/show:home
    ur://intent/show:status
    ur://intent/show:preferences
    ur://intent/show:servers
    ur://intent/show:remotes


## Télécommandes et Actions
La commande ``remote`` peut être utilisée pour ouvrir une télécommande.

    ur://intent/remote:Unified.Power

La commande ``action`` peut également être utilisée pour exécuter une action spécifique.

    ur://intent/remote:Unified.Power/action:lock

Les extras peuvent être spécifiés avec la commande ``extra``.

    ur://intent/remote:Core.Input/action:text/extra:foobar



## Actions de l'appareil
La commande ``device`` peut être utilisée pour exécuter des actions de l'appareil.

    ur://intent/device:wol
    ur://intent/device:keyboard
    ur://intent/device:keyboard
    ur://intent/device:mouse
    ur://intent/device:switch/extra:Unified.Chrome
    ur://intent/device:vibrate
    ur://intent/device:toast/extra:<message-ici>
    ur://intent/device:irsend/extra:<code-ir-ici>


## Changer de serveur
La commande ``server`` peut être utilisée pour passer à un autre serveur.

    ur://intent/server:Test-PC

Elle peut également être utilisée avec d'autres commandes.

    ur://intent/server:Test-PC/remote:Unified.Power/action:lock