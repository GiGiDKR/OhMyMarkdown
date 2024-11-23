# UTF8
* [utf8](#utf8-1)
* [startwith](#utf8startwith-string-find-)
* [endswith](#utf8endswith-string-find-)
* [iequals](#utf8iequals-a-b-)
* [equals](#utf8equals-a-b-)
* [sub](#utf8sub-string-start-length-)
* [char](#utf8char-string-index-)
* [len](#utf8len-string-)
* [indexof](#utf8indexof-string-find-)
* [lastindexof](#utf8lastindexof-string-find-)
* [replace](#utf8replace-string-old-new-)
* [contains](#utf8contains-string-find-)
* [trim](#utf8trim-string-)
* [tolower](#utf8tolower-string-)
* [toupper](#utf8toupper-string-)
* [empty](#utf8empty-string-)
* [split](#utf8split-string-delim-)
* [join (table)](#utf8join-delim-table-)
* [join (...)](#utf8join-delim-part1-part2--)



## utf8
La bibliothèque ``utf8`` fournit des fonctions essentielles de manipulation de chaînes pour le texte encodé en UTF8.

````lua
local utf8 = require("utf8");
````

Toutes les fonctions peuvent être utilisées comme des fonctions globales.

````lua
print(utf8.replace("foo bar", "foo", "hello")); -- "hello bar"
````

Pour de meilleures performances avec de grandes chaînes, créez une instance de chaîne UTF8 et réutilisez-la lorsque cela est possible. Notez la syntaxe de l'instance (``str:``) !

````lua
local str = utf8.new("foo bar");
str:replace("foo", "hello");
print(str:raw()); -- "hello bar"
````



### utf8.startswith( string, find )
Vérifie si ``string`` commence par le texte ``find``.

````lua
print(utf8.startswith("foo bar", "foo")); -- true
print(utf8.startswith("foo bar", "bar")); -- false
````



### utf8.endswith( string, find )
Vérifie si ``string`` se termine par le texte ``find``.

````lua
print(utf8.endswith("foo bar", "foo")); -- false
print(utf8.endswith("foo bar", "bar")); -- true
````



### utf8.iequals( a, b )
Effectue une vérification d'égalité insensible à la casse.

````lua
print(utf8.iequals("foo", "FOO")); -- true
print(utf8.iequals("foo", "foo")); -- true
````



### utf8.equals( a, b )
Effectue une vérification d'égalité sensible à la casse.

````lua
print(utf8.equals("foo", "FOO")); -- false
print(utf8.equals("foo", "foo")); -- true
````



### utf8.sub( string, start, [length] )
Obtient une partie de ``string`` à partir de la position ``start`` jusqu'à la fin de la chaîne ou si ``length`` est défini, jusqu'à la longueur définie.

````lua
print(utf8.sub("This is a text string", 2, 5);  -- "his i"
print(utf8.sub("This is a text string", 2));    -- "his is a text string"
````



### utf8.char( string, index )
Retourne le caractère à un ``index`` spécifique dans la ``string``.

````lua
print(utf8.char("This is a text string", 2)); -- 'i'
````



### utf8.len( string )
Retourne la longueur de ``string``.

````lua
print(utf8.len("This is a text string")); -- 21
````



### utf8.indexof( string, find )
Retourne le premier index de ``find`` dans la ``string``.

````lua
print(utf8.indexof("This is a text string", "text")); -- 11
````



### utf8.lastindexof( string, find )
Retourne le dernier index de ``find`` dans la ``string``.

````lua
print(utf8.lastindexof("This is a text string", "t"));	-- 17
````



### utf8.replace( string, old, new )
Remplace la chaîne ``old`` par la chaîne ``new`` dans la ``string``.

````lua
print(utf8.replace("foo bar", "foo", "hello")); -- "hello bar"
````



### utf8.contains( string, find )
Retourne vrai si ``string`` contient la chaîne ``find``.

````lua
print(utf8.contains("foo bar", "bar"));	-- true
print(utf8.contains("foo bar", "xyz"));	-- false
````



### utf8.trim( string )
Supprime les espaces du début et de la fin de la ``string``.

````lua
print(utf8.trim("   foo   "));	-- "foo"
````



### utf8.tolower( string )
Retourne une version transformée de la ``string`` où toutes les lettres sont en minuscules.

````lua
print(utf8.tolower("FOO"));	-- "foo"
````



### utf8.toupper( string )
Retourne une version transformée de la ``string`` où toutes les lettres sont en majuscules.

````lua
print(utf8.toupper("foo"));	-- "FOO"
````



### utf8.empty( string )
Vérifie si la ``string`` est vide.

````lua
print(utf8.empty("foo")); 	-- false
print(utf8.empty("")); 		-- true
print(utf8.empty(" "));		-- false
````



### utf8.split( string, delim )
Divise la ``string`` en utilisant le ``delim`` spécifié.

````lua
print(utf8.split("foo bar hello world", " ")); -- { "foo", "bar", "hello", "world" }
````



### utf8.join( delim, table )
Joint les éléments dans ``table`` en utilisant ``delim``.

````lua
local items = { "foo", "bar" };
print(utf8.join(" ", items)); -- "foo bar";
````



### utf8.join( delim, part1, part2, ... )
Joint toutes les parties en utilisant ``delim``.

````lua
print(utf8.join(" ", "foo", "bar")); -- "foo bar";
````


