# Données
* [data](#data)
* [json](#json)
	* [tojson](#data-tojson-table-)
	* [tojsonpretty](#data-tojsonpretty-table-)
	* [fromjson](#data-fromjson-json-)
* [xml](#xml)
	* [fromxml](#data-fromxml-xml-)
* [base](#base)
	* [tobase64](#data-tobase64-data-)
	* [frombase64](#data-frombase64-str-)
	* [tobase32](#data-tobase32-data-)
	* [frombase32](#data-frombase32-str-)
* [time](#time)
	* [sec2span](#data-sec2span-seconds-)
	* [span2sec](#data-span2sec-span-)
	* [timestamp](#data-timestamp-)
* [security](#security)
	* [nonce](#data-nonce-)
	* [digest](#data-digest-name-data-)
	* [digesthex](#data-digesthex-name-data-)



## data
La bibliothèque ``data`` fournit des analyseurs et des convertisseurs pour diverses formes de données.

````lua
local data = require("data");
````



## json



### data.tojson( table )
Convertit la table Lua en JSON.

````lua
tbl = { foo = 123, bar = "hello world" };
json = data.tojson(tbl);
````



### data.tojsonpretty( table )
Convertit la table Lua en JSON joliment formaté.

````lua
tbl = { foo = 123, bar = "hello world" };
json = data.tojsonpretty(tbl);
````



### data.fromjson( json )

````lua
json = "{ \"foo\" = 123, \"bar\" = \"hello world\" }";
tbl = data.fromjson(json);
````



## xml



### data.fromxml( xml )

````lua
xml = "<foo><bar>hello world</bar></foo>";
root = data.fromxml(xml);
````

Un élément XML est représenté par un objet qui ressemble à ceci :

````lua
{ name = "bar",
  text = "hello world",
  attributes = { ... },
  children = { ... } }
````

Le nombre d'éléments enfants peut être récupéré comme ceci :

````lua
#root.children;
````

Un élément enfant est récupéré comme ceci :

````lua
root.children[1];
````

Les attributs sont récupérés comme ceci :

````lua
root.attributes["foo"];
````



## base



### data.tobase64( data )
Convertit les ``données`` spécifiées en une chaîne encodée en base-64.

````lua
b64str = data.tobase64(...);
````



### data.frombase64( str )
Convertit ``str`` à partir d'une chaîne encodée en base-64.

````lua
data = data.frombase64("...");
````



### data.tobase32( data )
Convertit les ``données`` spécifiées en une chaîne encodée en base-32.

````lua
b32str = data.tobase64(...);
````



### data.frombase32( str )
Convertit ``str`` à partir d'une chaîne encodée en base-32.

````lua
data = data.frombase32("...");
````



## time



### data.sec2span( seconds )
Convertit ``seconds`` en une chaîne de durée au format suivant : [HH:]MM:SS.

````lua
print(data.sec2span(754)); -- 12:34
````



### data.span2sec( span )
Convertit une chaîne de durée en nombre de secondes qu'elle représente.

````lua
print(data.span2sec("12:34")); -- 754
````

	
	
### data.timestamp( )
Obtient le timestamp UNIX actuel (millisecondes).

````lua
print(data.timestamp()); -- 1424096219
````
	


## security



### data.nonce( )
Génère un nonce entier non signé de 64 bits.

````lua
data.nonce();
````



### data.digest( name, data )
Calcule le hachage binaire des ``données`` en utilisant le moteur de hachage spécifié.

Moteurs pris en charge : ``MD5``, ``SHA1``, ``SHA256``, ``SHA512``, etc. Voir la documentation OpenSSL pour une liste des algorithmes de hachage pris en charge.

````lua
data.digest("sha1", "foobar");
````



### data.digesthex( name, data )
Calcule le hachage hexadécimal des ``données`` en utilisant le moteur de hachage spécifié.

Moteurs pris en charge : ``MD5``, ``SHA1``, ``SHA256``, ``SHA512``, etc. Voir la documentation OpenSSL pour une liste des algorithmes de hachage pris en charge.

````lua
data.digesthex("sha1", "foobar");
````


