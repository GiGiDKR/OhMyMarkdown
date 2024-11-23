# Clavier
* [keyboard](#keyboard)
* [press](#keyboardpress-key-)
* [stroke](#keyboardstroke-key-)
* [text](#keyboardtext-text-)
* [down](#keyboarddown-key-)
* [up](#keyboardup-key-)
* [character](#keyboardcharacter-chr-)
* [ismodifier](#keyboardismodifier-key-)
* [iskey](#keyboardiskey-key-)

## keyboard
La bibliothèque clavier fournit des actions pour simuler des frappes de touches et envoyer du texte. Consultez la [liste des touches](../res/keys.md).

````lua
local kb = require("keyboard");
````

### keyboard.press( key, [...] )
Effectue une ou plusieurs pressions de touches **consécutives**.

````lua
kb.press("down", "down", "return");
kb.press("return");
````

### keyboard.stroke( key, [...] )
Effectue une frappe de touche en utilisant une ou plusieurs touches.

````lua
kb.stroke("ctrl", "shift", "return");
kb.stroke("win");
````

### keyboard.text( text )
Tape le texte spécifié, y compris les caractères unicode et spéciaux.

````lua
kb.text("hello world!");
kb.text("åäö");
````

### keyboard.down( key, [...] )
Appuie sur une ou plusieurs touches **consécutives** jusqu'à ce que ``up`` soit appelé.

````lua
kb.down("return");
````

### keyboard.up( key, [...] )
Relâche une ou plusieurs touches **consécutives** qui ont été pressées.

````lua
kb.up("return");
````

### keyboard.character( chr )
Tape le code de caractère spécifié (code de caractère UTF8 entier).

````lua
kb.character(0x123);
````

### keyboard.ismodifier( key )
Retourne un booléen spécifiant si la touche est un modificateur (par exemple, ctrl, shift, alt).

````lua
print(kb.ismodifier("ctrl"));    -- true
print(kb.ismodifier("return"));  -- false
````

### keyboard.iskey( key )
Retourne un booléen spécifiant si la touche est un nom de touche valide.

````lua
print(kb.iskey("f1"));   -- true
print(kb.iskey("$"));    -- false
````


