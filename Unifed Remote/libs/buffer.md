# Tampon
* [buffer](#buffer)
* [new](#buffernew-encoding-byteorder-)
* [length](#bufferlength-)
* [available](#bufferavailable-)
* [position](#bufferposition-)
* [at](#bufferat-pos-)
* [tostring](#buffertostring-)
* [tohex](#buffertohex-)
* [écriture](#écriture)
  * [write](#bufferwrite-raw-)
  * [writebuffer](#bufferwritebuffer-buffer-)
  * [writestring](#bufferwritestring-str-)
  * [writeline](#bufferwriteline-str-)
  * [writebyte](#bufferwritebyte-value-)
  * [writebytes](#bufferwritebytes-value-)
  * [writeint8](#bufferwriteint8-value-)
  * [writeint16](#bufferwriteint16-value-)
  * [writeint32](#bufferwriteint32-value-)
  * [writeint64](#bufferwriteint64-value-)
  * [writefloat](#bufferwritefloat-value-)
  * [writedouble](#bufferwritedouble-value-)
* [lecture](#lecture)
  * [read](#bufferread-len-)
  * [readbuffer](#bufferreadbuffer-)
  * [readstring](#bufferreadstring-)
  * [readline](#bufferreadline-)
  * [readbyte](#bufferreadbyte-)
  * [readbytes](#bufferreadbytes-)
  * [readuint8](#bufferreaduint8-)
  * [readint8](#bufferreadint8-)
  * [readuint16](#bufferreaduint16-)
  * [readint16](#bufferreadint16-)
  * [readuint32](#bufferreaduint32-)
  * [readint32](#bufferreadint32-)
  * [readuint64](#bufferreaduint64-)
  * [readint64](#bufferreadint64-)
  * [readfloat](#bufferreadfloat-)
  * [readdouble](#bufferreaddouble-)



## buffer
La bibliothèque ``buffer`` fournit un moyen facile de lire et d'écrire des données binaires.

````lua
-- Créer un nouveau tampon
local buffer = require("buffer").new();
````



### buffer.new( [encoding] [,byteorder] )
Crée un nouveau tampon (encodage UTF8 par défaut et ordre des octets réseau).

Encodages pris en charge :<br />
``ascii``, ``latin1``, ``latin2``, ``latin9``,
``utf8``, ``utf16``, ``utf32``, ``windows1250``, ``windows1251``, ``windows1252``.

Ordres des octets pris en charge :<br />
``le``, ``be``, ``network``, ``native``.

````lua
local b1 = require("buffer").new();
local b2 = libs.buffer.new("utf16");
local b3 = libs.buffer.new("utf8", "le");
````


### buffer:length( )
Retourne la longueur totale des données dans le tampon.

````lua
local b = require("buffer").new();
b:writebyte(123);
print(buffer:length()); -- 1
````



### buffer:available( )
Retourne la longueur des données non lues dans le tampon.

````lua
local b = require("buffer").new();
b:writebyte(123);
print(buffer.available()); -- 1
b:readbyte();
print(buffer.available()); -- 0
````



### buffer:position( )
Retourne la position actuelle dans le tampon.

````lua
local b = require("buffer").new();
b:writebyte(123);
print(b:position()); -- 0
b:readbyte();
print(b:position()); -- 1
````



### buffer:at( pos )
Retourne l'octet à la position spécifiée (basé sur un index zéro).

````lua
local b = require("buffer").new();
b:writestring("abc");
print(b:at(0));  --  3
print(b:at(2));  -- 'b' 98
````



### buffer:tostring( )
Retourne une représentation sous forme de chaîne du tampon.

````lua
local b = require("buffer").new();
b:writebytes(12, 34, 56);
print(b:tostring()); -- [12,34,56]
````



### buffer:tohex( )
Retourne une représentation hexadécimale sous forme de chaîne du tampon.

````lua
local b = require("buffer").new();
b:writebytes(161, 178, 195);
print(b:tostring()); -- [A1,B2,C3]
````



## écriture



### buffer:write( raw )
Écrire des données brutes dans le tampon.

````lua
local b = require("buffer").new();
b:write("abc");
print(b:tostring()); -- [97,98,99]
````


### buffer:writebuffer( buffer )
Copie les données d'un autre tampon.

````lua
local a = require("buffer").new();
b:write("abc");

local b = require("buffer").new();
b:writebuffer(a);
print(b:tostring()); -- [97,98,99]
````


### buffer:writestring( str )
Écrit une chaîne en utilisant l'encodage spécifié (préfixé par la longueur).

````lua
local b = libs.buffer.new("utf16");
b:writestring("abc");
print(b:tostring()); -- [6,97,0,98,0,99,0]
````



### buffer:writeline( str )
Écrit une ligne de texte brute en utilisant l'encodage spécifié (non préfixé par la longueur).

````lua
local b = require("buffer").new();
b:writeline("foobar");
print(b:readline()); -- foobar
````



### buffer:writebyte( value )
Écrit un seul octet dans le tampon.

````lua
local b = require("buffer").new();
b:writebyte(123);
print(b:tostring()); -- [123]
````



### buffer:writebytes( value )
Écrit plusieurs octets dans le tampon.

````lua
local b = require("buffer").new();
b:writebytes(12, 34);
b:writebytes({ 56, 78 });
print(b:tostring()); -- [12,34,56,78]
````



### buffer:writeint8( value )
Écrit une valeur entière de 8 bits.

````lua
local b = require("buffer").new();
b:writeint8(123);
print(b:tostring()); -- [123]
````



### buffer:writeint16( value )
Écrit une valeur entière de 16 bits.

````lua
local b = require("buffer").new();
b:writeint16(123);
print(b:tostring()); -- [0,123]
````



### buffer:writeint32( value )
Écrit une valeur entière de 32 bits.

````lua
local b = require("buffer").new();
b:writeint32(123);
print(b:tostring()); -- [0,0,0,123]
````



### buffer:writeint64( value )
Écrit une valeur entière de 64 bits.

````lua
local b = require("buffer").new();
b:writeint64(123);
print(b:tostring()); -- [0,0,0,0,0,0,0,123]
````



### buffer:writefloat( value )
Écrit une valeur flottante de 32 bits.

````lua
local b = require("buffer").new();
b:writefloat(123.456);
print(b:tostring()); -- [67,122,0,0]
````



### buffer:writedouble( value )
Écrit une valeur flottante de 64 bits.

````lua
local b = require("buffer").new();
b:writedouble(123.456);
print(b:tostring()); -- [64,111,64,0,0,0,0,0]
````



## lecture



### buffer:read( [len] )
Lire des données brutes à partir du tampon.

````lua
local b = require("buffer").new();
b:write("abc");
print(b:read(1)); -- a
print(b:read());  -- bc
````



### buffer:readbuffer( [len] )
Lire des données à partir du tampon dans un nouveau tampon.

````lua
local a = require("buffer").new();
a:write("abc");
print(a:read(1)); -- a

local b = a:readbuffer();
print(b:tostring()) -- [98,99]
````



### buffer:readstring( )
Lire une chaîne en utilisant l'encodage spécifié (préfixé par la longueur).

````lua
local b = require("buffer").new();
b:writestring("abc");
print(b:readstring()); -- abc
````



### buffer:readline( )
Lire une ligne de texte brute en utilisant l'encodage spécifié (non préfixé par la longueur). Retourne ``nil`` s'il n'y a pas de lignes complètes disponibles.

````lua
local b = require("buffer").new();
b:writeline("foobar");
print(b:readline()); -- foobar

b:readline(); -- nil
````



### buffer:readbyte( )
Lire un seul octet à partir du tampon.

````lua
local b = require("buffer").new();
b:writebyte(123);
print(b:readbyte()); -- 123
````



### buffer:readbytes( )
Lire plusieurs octets à partir du tampon.

````lua
local b = require("buffer").new();
b:writestring("abc");
print(b:readbytes()); -- [3,97,98,99]
````



### buffer:readuint8( )
Lire une valeur entière non signée de 8 bits.

````lua
local b = require("buffer").new();
b:writeint8(250);
print(b:readuint8()); --  250
````



### buffer:readint8( )
Lire une valeur entière signée de 8 bits.

````lua
local b = require("buffer").new();
b:writeint8(250);
print(b:readint8()); --  -6
````



### buffer:readuint16( )
Lire une valeur entière non signée de 16 bits.

````lua
local b = require("buffer").new();
b:writeint16(250);
print(b:readuint16()); --  250
````



### buffer:readint16( )
Lire une valeur entière signée de 16 bits.

````lua
local b = require("buffer").new();
b:writeint16(250);
print(b:readint16()); --  -6
````



### buffer:readuint32( )
Lire une valeur entière non signée de 32 bits.

````lua
local b = require("buffer").new();
b:writeint32(250);
print(b:readuint32()); --  250
````



### buffer:readint32( )
Lire une valeur entière signée de 32 bits.

````lua
local b = require("buffer").new();
b:writeint32(250);
print(b:readint32()); --  -6
````



### buffer:readuint64( )
Lire une valeur entière non signée de 64 bits.

````lua
local b = require("buffer").new();
b:writeint64(250);
print(b:readuint64()); --  250
````



### buffer:readint64( )
Lire une valeur entière signée de 64 bits.

````lua
local b = require("buffer").new();
b:writeint64(250);
print(b:readint64()); --  -6
````



### buffer:readfloat( )
Lire une valeur flottante de 32 bits.

````lua
local b = require("buffer").new();
b:writefloat(123.456);
print(b:tostring()); -- [67,122,0,0]
````



### buffer:readdouble( )
Lire une valeur flottante de 64 bits.

````lua
local b = require("buffer").new();
b:writedouble(123.456);
print(b:tostring()); -- [64,111,64,0,0,0,0,0]


