# Événements d'action

Les événements d'action peuvent être utilisés pour effectuer certaines fonctionnalités avant et après l'exécution d'une action. Cela est utile pour
exécuter des fonctionnalités communes pour de nombreuses actions, journaliser, configurer et démonter, filtrer les actions, etc.

	events.preaction = function (name, extras)
		-- Faire quelque chose avant que les actions ne soient exécutées...
		return true;
	end

	events.postaction = function (name, extras)
		-- Faire quelque chose après que les actions ont été exécutées...
	end

	actions.foo = function ()
		-- Ma fonction foo bar...
	end

Notez que l'événement preaction doit renvoyer une valeur booléenne indiquant si l'action doit être exécutée ou non.
Si preaction renvoie true, alors l'action et par conséquent l'événement postaction seront déclenchés. Sinon, ils ne le seront pas.
Si un événement preaction n'est pas disponible, alors les actions seront toujours déclenchées.

	events.preaction = function (name, extras)
		-- Ignorer toutes les actions nommées "foo"
		if (name == "foo") then
			return false;
		end
		return true;
	end

Il est également possible de mettre en œuvre un événement de rattrapage (ou de secours) pour les actions. Cet événement est utilisé pour capturer les actions
qui n'ont pas été explicitement définies. Cela est particulièrement utile pour les télécommandes qui peuvent avoir besoin d'utiliser des actions générées dynamiquement
ou nommées de manière variable (où les noms d'action ne sont pas connus à l'avance). Notez qu'il est exécuté si et seulement si une
action n'est pas explicitement implémentée.

	events.action = function (name, extras)
		-- Capturer les actions non définies ici...
	end
