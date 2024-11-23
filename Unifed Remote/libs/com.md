# COM
* [luacom](#luacom-1)
* [luacom.CreateObject](#luacomcreateobject-id-)
* [luacom.GetObject](#luacomgetobject-id-)
* [Libération](#releasing)



## luacom
La bibliothèque ``com`` peut être utilisée pour créer et accéder à des instances COM sur Windows. Elle est accessible en utilisant la variable globale ``luacom``.

````lua
obj = luacom.CreateObject("PowerPoint.Application");
````

Pour une référence complète, consultez le [Manuel de l'utilisateur LuaCOM](http://www.tecgraf.puc-rio.br/~rcerq/luacom/pub/1.3/luacom-htmldoc/).



## luacom.CreateObject( id )
Crée une instance de l'objet avec l'identifiant spécifié.

````lua
obj = luacom.CreateObject("PowerPoint.Application");
````



## luacom.GetObject( id )
Trouve une instance en cours d'exécution de l'objet avec l'identifiant spécifié.

````lua
obj = luacom.GetObject("PowerPoint.Application");
````



## Libération
Il est très important de libérer tous les objets COM lorsqu'ils ne sont plus utilisés.

````lua
obj = nil;
collectgarbage();
````


