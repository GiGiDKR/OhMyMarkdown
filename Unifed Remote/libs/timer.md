# Minuterie
* [timer](#timer)
	* [timeout](#timertimeout-fn-time-)
	* [interval](#timerinterval-fn-time-)
	* [schedule](#timerschedule-fn-time-)
	* [cancel](#timercancel-id-)



## timer
La bibliothèque de minuterie fournit des délais d'attente, des intervalles et des horaires.

````lua
local tmr = require("timer");
````



### timer.timeout( fn, time )
Appelle la fonction ``fn`` après le ``time`` spécifié en millisecondes. 
Retourne un ID de minuterie qui peut être utilisé pour ``cancel`` le délai d'attente avant qu'il ne soit appelé.

````lua
tid = tmr.timeout(function ()
	print("3 secondes plus tard");
end, 3000);
````

La fonction peut être soit en ligne, soit une fonction nommée, selon ce qui est le plus pratique.

````lua
function foobar()
	print("3 secondes plus tard");
end

tmr.timeout(foobar, 3000);
````



### timer.interval( fn, time )
Appelle la fonction ``fn`` toutes les ``time`` millisecondes. 
Retourne un ID de minuterie qui peut être utilisé pour ``cancel`` l'intervalle à un moment ultérieur.

````lua
tid = tmr.interval(function ()
	print("tic");
end, 1000);
````



### timer.schedule( fn, time )
Appelle la fonction ``fn`` à l'heure spécifiée [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) ``time``. 
Retourne un ID de minuterie qui peut être utilisé pour ``cancel`` l'horaire avant qu'il ne soit appelé.

````lua
tmr.schedule(function ()
	print("bonjour!");
end, "2014-05-06T08:00:00Z");
````



### timer.cancel( id )
Toutes les fonctions de minuterie retournent un ID de minuterie. Cet ID est utilisé pour annuler les événements de minuterie.

````lua
tid = tmr.timeout(...);
tmr.cancel(tid);
````

Vous devez vous assurer que vos minuteries sont démarrées puis annulées de manière appropriée. Par exemple :

````lua
local tid;

events.focus = function ()
	tid = timer.interval(function ()
		print("bonjour tout le monde!");
	end, 1000);
end

events.blur = function ()
	timer.cancel(tid);
end
````


