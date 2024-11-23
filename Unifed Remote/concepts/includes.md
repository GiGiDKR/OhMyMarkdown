# Inclus

La fonction ``include`` peut être utilisée pour simplifier la réutilisation de fonctionnalités communes partagées entre plusieurs télécommandes.
Par exemple, vous pouvez avoir un ensemble d'actions ou de fonctions que vous souhaitez utiliser dans plusieurs variantes d'une télécommande.
Vous pouvez placer cela dans un fichier appelé ``common.lua``.

	Télécommandes/
		Exemple/
			common.lua
			Foo/
				meta.prop
				remote.lua
			Bar/
				meta.prop
				remote.lua

Dans l'implémentation de chaque télécommande, vous pouvez ensuite inclure le fichier commun et utiliser ce que vous y avez placé.
Par exemple, dans le fichier ``remote.lua`` pour la télécommande ``Foo`` :

	include("../common.lua")

	actions.foo = function ()
		func_from_common("foo");
	end
