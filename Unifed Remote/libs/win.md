# Windows
* [kill](#winkill-process-)
* [close](#winclose-process-)
* [quit](#winquit-process-)
* [active](#winactive)
* [desktop](#windesktop)
* [process](#winprocess-name-)
* [window](#winwindow-process-)
* [title](#wintitle-window-)
* [class](#winclass-target-)
* [switchto](#winswitchto-target-)
* [switchtowait](#winswitchtowait-target-timeout-)
* [list](#winlist-all-)
* [find](#winfind-class-title-)
* [findall](#winfindall-parent-class-title-recursive-)
* [post](#winpost-window-message-wparam-lparam-)
* [send](#winsend-window-message-wparam-lparam-)
* [findimage](#winfindimage-image-window-)


## win
La bibliothèque ``win`` fournit des fonctions essentielles pour la plateforme Windows.
````lua
	local win = libs.win;
````


### win.kill( process )
Tue le processus avec le nom ou l'ID de processus spécifié.
````lua
	win.kill(1234);
	win.kill("calc.exe");
````

### win.close( process )
Envoie un message de fermeture de fenêtre au nom ou à l'ID de processus spécifié.
````lua
	win.close(1234);
	win.close("calc.exe");
````

### win.quit( process )
Envoie un message de fermeture d'application au nom ou à l'ID de processus spécifié.
````lua
	win.quit(1234);
	win.quit("calc.exe");
````

### win.active()
Retourne le handle de la fenêtre active (au premier plan).
````lua
	hwnd = win.active();
````

### win.desktop()
Retourne le handle de la fenêtre du bureau.
````lua
	hwnd = win.desktop();
````

### win.process( name )
Retourne l'ID du processus avec le nom spécifié.
````lua
	pid = win.process("calc.exe");
````

### win.window( process )
Retourne le handle de la fenêtre du processus avec le nom ou l'ID spécifié.
````lua
	hwnd = win.window("calc.exe");
````

### win.title( window )
Retourne le titre du handle de fenêtre ou du nom de processus spécifié.
````lua
	title = win.title(1234);
	title = win.title("calc.exe");
````

### win.class( target )
Retourne le nom de la classe de la fenêtre ou du processus spécifié.
````lua
	cls = win.class(1234);
	cls = win.class("calc.exe");
````

### win.switchto( target )
Change la fenêtre active pour la fenêtre ou le processus spécifié.
````lua
	win.switchto(1234);
	win.switchto("calc.exe");
````

### win.switchtowait( target, [timeout] )
Change la fenêtre active pour la fenêtre ou le processus spécifié et attend qu'elle devienne active.
````lua
	win.switchtowait(1234);
	win.switchtowait("calc.exe");
````
Un délai d'attente peut également être spécifié (par défaut 100 ms).
````lua
	win.switchtowait(1234, 500);
	win.switchtowait("calc.exe", 500);
````

### win.list( [all] )
Retourne un tableau des tâches en cours d'exécution sur l'ordinateur.
````lua
	tasks = win.list();
````
Chaque tâche est représentée par un objet comme celui-ci :
````js
	{ Handle = 1234,
	  Title = "foobar",
	  Name = "foobar.exe" }
````
Tous les processus peuvent être listés en spécifiant ``all`` comme ``true``.
````lua
	processes = win.list(true);
````

### win.find( class, title )
Trouve la fenêtre avec la ``class`` et/ou le ``title`` spécifiés.
````lua
	hwnd = win.find("ChromeWidgetWin_1", nil);
	hwnd = win.find(nil, "Calculator");
	hwnd = win.find("foobar_class", "foobar");
````

### win.find( parent, after, class, title )
Trouve la fenêtre avec la ``class`` et/ou le ``title`` spécifiés avec le ``parent`` donné et l'enfant précédent ``after``.
````lua
	parent = win.find("ChromeWidgetWin_1", nil);
	hwnd = win.find(parent, 0, "foobar", nil);
````

### win.findall( parent, class, title, [recursive] )
Retourne une liste de fenêtres avec la ``class`` et/ou le ``title`` spécifiés pour le ``parent`` donné.
````lua
	-- Trouver le handle du navigateur Chrome
	parent = win.find("ChromeWidgetWin_1", nil);

	-- Lister toutes les fenêtres enfants (c'est-à-dire tous les onglets)
	tabs = win.findall(parent, "ChromeWidgetWin_1", nil, true);
````

### win.post( window, message, wparam, lparam )
Envoie un message à la fenêtre spécifiée et retourne si cela a réussi.
````lua
	hwnd = win.find("ChromeWidgetWin_1", nil);
	success = win.post(hwnd, 0x1234, 0, 0);
````

### win.send( window, message, wparam, lparam )
Envoie un message à la fenêtre spécifiée et retourne le résultat.
````lua
	hwnd = win.find("ChromeWidgetWin_1", nil);
	result = win.send(hwnd, 0x1234, 0, 0);
````

### win.findimage( image, [window] )
Effectue une correspondance d'image avec le fichier ``image`` spécifié.
````lua
	x,y = win.findimage("play_button.png");
````
Un handle de fenêtre spécifique peut être spécifié, sinon l'écran entier est utilisé.
````lua
	hwnd = win.find("ChromeWidgetWin_1", nil);
	x,y = win.findimage("play_button.png", hwnd);
````

