# Bit
* [bit](#bit-1)
* [bnot](#bitbnot-x-)
* [band](#bitband-x-y-)
* [bor](#bitbor-x-y-)
* [bxor](#bitbxor-x-y-)
* [lshift](#bitlshift-x-n-)
* [rshift](#bitrshift-x-n-)
* [arshift](#bitarshift-x-n-)
* [rol](#bitrol-x-n-)
* [ror](#bitror-x-n-)
* [tohex](#bittohex-x-n-)
* [tobit](#bittobit-x-)
	


## bit
La bibliothèque ``bit`` fournit des opérations au niveau des bits.

	local bit = require("bit");

Consultez la [documentation officielle de LuaJIT](http://bitop.luajit.org/api.html) pour plus de détails.



### bit.bnot( x )
Retourne le **non** bit à bit de ``x``.



### bit.band( x, y )
Retourne le **et** bit à bit de ``x`` et ``y``.



### bit.bor( x, y )
Retourne le **ou** bit à bit de ``x`` et ``y``.



### bit.bxor( x, y )
Retourne le **ou exclusif** bit à bit de ``x`` et ``y``.



### bit.lshift( x, n )
Retourne le **décalage logique à gauche** bit à bit de ``x`` de ``n`` étapes.



### bit.rshift( x, n )
Retourne le **décalage logique à droite** bit à bit de ``x`` de ``n`` étapes.



### bit.arshift( x, n )
Retourne le **décalage arithmétique à droite** bit à bit de ``x`` de ``n`` étapes.



### bit.rol( x, n )
Retourne la **rotation à gauche** bit à bit de ``x`` de ``n`` étapes.



### bit.ror( x, n )
Retourne la **rotation à droite** bit à bit de ``x`` de ``n`` étapes.



### bit.tohex( x [,n] )
Fonction d'aide pour convertir un nombre en chaîne hexadécimale.



### bit.tobit( x )
Fonction d'aide pour normaliser les valeurs.


