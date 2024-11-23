# Socket
* [socket](#socket-)
* [new](#socketnew-)
* [connect](#socketconnect-host-port-)
* [connected](#socketconnected-)
* [write](#socketwrite-data-)
* [close](#socketclose-)
* [events](#events)
	* [onconnect](#socketonconnect-)
	* [ondata](#socketondata-data-)
	* [onclose](#socketonclose-)
	* [onerror](#socketonerror-err-)



## socket
La bibliothèque ``socket`` fournit un moyen facile de lire et d'écrire des données binaires.

```lua
-- Créer un nouveau socket
local s = require("socket").new();

-- Attacher un gestionnaire d'événements
s:onconnect(function ()
	s:write("foo");
end);

-- Connecter le socket
s:connect("localhost", 1234);
```


### socket.new( )
Crée un nouveau socket.

```lua
local s = require("socket").new();
```



### socket:connect( host, port )
Se connecte à l'hôte et au port spécifiés. Invoque ``onconnect``.

```lua
local s = require("socket").new();
s:connect("localhost", 1234);
```



### socket:connected( )
Vérifie si le socket est actuellement connecté.

```lua
local s = require("socket").new();
print(s:connected()); -- false
```



### socket:write( data )
Écrit des données brutes dans le socket. Utilisez un tampon pour une gestion facile des données.

```lua
local s = require("socket").new();
s:onconnect(function ()
	-- écrire des données brutes
	s:write("abc");
	
	-- écrire des données à partir du tampon
	local b = require("buffer").new("utf8");
	b:writestring("je supporte l'unicode åäö");
	s:write(b:read());
end);
```



### socket:close( )
Ferme le socket s'il est connecté. Invoque ``onclose``.

```lua
local s = require("socket").new();
s:onconnect(function ()
	s:close();
end);
```



## events



### socket:onconnect( )
Callback à invoquer lorsque la connexion est établie.

```lua
local s = require("socket").new();
s:onconnect(function ()

end);
```



### socket:ondata( data )
Callback à invoquer lorsque des données brutes ``data`` sont reçues. Utilisez un tampon pour une gestion facile des données.

```lua
local s = require("socket").new();
s:ondata(function (data)
	print(data);
	
	-- lire les données dans le tampon
	local b = require("buffer").new("utf8");
	b:write(data);
	print(b:readstring());
end);
```



### socket:onclose( )
Callback à invoquer lorsque la connexion est rompue.

```lua
local s = require("socket").new();
s:onconnect(function ()

end);
```



### socket:onerror( err )
Callback à invoquer lorsqu'une erreur se produit.

```lua
local s = require("socket").new();
s:onerror(function ( err )
	print(err);
end);
s:connect("asdf", 1234);
```


