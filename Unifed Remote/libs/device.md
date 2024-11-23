# Appareil
* [device](#device)
* [wol](#devicewol-mac)
* [irsend](#deviceirsend-code)
* [keyboard](#devicekeyboard)
* [mouse](#devicemouse)
* [switch](#deviceswitch-id)
* [vibrate](#devicevibrate)
* [listen](#devicelisten)
* [toast](#devicetoast-message)
* [server](#deviceserver-name)
	


## device
La bibliothèque ``device`` fournit des actions qui peuvent être effectuées sur l'appareil client.

````lua
local dev = require("device");
````



### device.wol( [mac] )
Dans la plupart des cas, WOL (Wake On LAN) doit être envoyé sans être connecté à un serveur (c'est-à-dire si le serveur est en veille et que vous souhaitez le réveiller). Par conséquent, les actions WOL doivent être spécifiées dans la disposition. Voir [Actions en ligne](../concepts/layout.md) pour en savoir plus sur cette syntaxe.

````xml
<layout>
	<button text="WOL" onclick="@wol" />
</layout>
````

Si aucune ``mac`` n'est spécifiée, alors la dernière mac utilisée du serveur sera utilisée. Sinon, la mac spécifiée sera utilisée.

````xml
<layout>
	<button text="WOL" onclick="@wol,00:00:00:00:00:00:00:00" />
</layout>
````



### device.irsend( code )
Envoyer un code IR (format pronto) en utilisant le blaster IR intégré de l'appareil (si disponible).

````lua
dev.irsend("0000 0000 0000 0000");
````
````xml
<layout>
	<button text="IR" onclick="@irsend,0000 006b 0026 0000 0154 00aa 0015 0015..." />
</layout>
````


### device.keyboard()
Ouvre la télécommande du clavier sur l'appareil.

````lua
dev.keyboard();
````



### device.mouse()
Ouvre la télécommande de la souris sur l'appareil.

````lua
dev.mouse();
````



### device.switch( id )
Ouvre la télécommande avec l'identifiant spécifié ``id`` sur l'appareil.

````lua
dev.switch("Unified.Chrome");
````



### device.vibrate()
Demande à l'appareil d'effectuer un retour haptique.

````lua
dev.vibrate();
````



### device.listen()
Demande à l'appareil de commencer à écouter pour le contrôle vocal (si disponible).

````lua
dev.listen();
````



### device.toast( message )
Affiche un message rapide (toast) sur l'appareil.

````lua
dev.toast("foobar");
````



### device.server( name )
Se connecter au serveur spécifié (nom exact).

````lua
dev.server("Home-PC");
````


