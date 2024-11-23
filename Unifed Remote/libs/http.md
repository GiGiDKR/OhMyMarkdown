# HTTP
* [http](#http)
* [get](#httpget-url-callback-)
* [post](#httppost-url-content-callback-)
* [request](#httprequest-request-callback-)
* [discover](#httpdiscover-options)
* [encodedecode](#encodedecode)
	* [encode](#httpencode-value-)
	* [decode](#httpdecode-value-)
	* [urlencode](#httpurlencode-value-)
	* [urlcomponentencode](#httpurlcomponentencode-value-)
	* [urldecode](#httpurldecode-value-)



## http
La bibliothèque ``http`` peut être utilisée pour envoyer des requêtes HTTP(S).

````lua
local http = require("http");
````



### http.get( url, callback )
Crée une requête HTTP(S) GET asynchrone simple.

````lua
local url = "http://www.unifiedremote.com/whats-my-ip";
http.get(url, function (err, resp)
	if (err) then return; end
	print(resp);
end);
````



### http.post( url, content, callback )
Crée une requête HTTP(S) POST asynchrone simple.

````lua
local url = "http://some.web.site/api/do";
local content = "some content to post";
http.post(url, content, function (err, resp)
	if (err) then return; end
	print(resp);	
end);
````



### http.request( request, callback )
Crée une requête HTTP(S) personnalisée spécifiée par la table ``request``.

````lua
local headers = { "key" = "value",
                  "foo" = "bar" };

local req = { method = "post",
		      url = "http://foo.bar/api/do",
		      mime = "text/plain",
		      headers = headers,
		      content = "foobar" };

http.request(req, function (err, resp)
	if (err) then return; end
	print(resp);		
end);
````

La table de réponse ressemble à ceci :

````lua
{ status = "200",
  reason = "ok",
  length = "12345",
  mime = "text/plain",
  headers = {...},
  content = "..." };
````



### http.discover( options )
Scanne le réseau à la recherche de serveurs HTTP filtrés par les ``options`` spécifiées.

````lua
-- Trouver tous les serveurs HTTP écoutant sur le port 81
local result = http.discover({ port = 81 });
````

Où le résultat est un tableau d'adresses IP :

````lua
{ "192.168.1.23",
  "192.168.1.128" };
````

La table d'options prend en charge les valeurs suivantes :

````lua
{ mask = "...",			-- Masque IP, par défaut : 255.255.255.0
  min = 123,			-- adresse min, par défaut : 0
  max = 128,			-- adresse max, par défaut : 254
  port = 81,			-- numéro de port, par défaut : 80
  timeout = 5 };		-- délai d'attente du test, par défaut : 1 (sec)
````



## encode/decode



### http.encode( value )
Encode en HTML la valeur spécifiée (échappe &<>"').

````lua
http.encode("&<>\"\'");				--> "&amp;&lt;&gt;&quot;&apos;"
````



### http.decode( value )
Décode toutes les entités HTML (nommées et numérotées déc/hex) dans la valeur spécifiée.

````lua
http.decode("&amp;&#39;&#x27;");	-->	&''
````



### http.urlencode( value )
Encode en URL la ``value`` spécifiée.

````lua
http.urlencode("foo bar");			--> "foo%20bar"
````



### http.urlcomponentencode( value )
Encode les caractères de composant d'URL : ?#/=&:

````lua
http.urlcomponentencode("...");
````



### http.urldecode( value )
Décode en URL la ``value`` spécifiée.

````lua
http.urldecode("foo%20bar");		--> "foo bar"
````

Pour des mises à jour de disposition avancées (par exemple, listes ou dialogues), utilisez plutôt [``libs.server.update``](./server.md#server_update).


