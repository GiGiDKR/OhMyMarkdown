# Disposition
* [Mise à jour](#mise-à-jour)
* [Exemple](#exemple)
* [Avancé](#avancé)
	


## layout
La bibliothèque ``layout`` peut être utilisée pour modifier les propriétés des contrôles. C'est une bibliothèque globale et n'a pas besoin d'être importée.



### Mise à jour
Les contrôles peuvent être facilement modifiés en utilisant la syntaxe suivante.

	layout.{id}.{property} = {value};


### Exemple
	
	<layout>
		<row>
			<toggle id="my_toggle" text="foo" />
		</row>
		<row>
			<label id="my_label" text="foo" />
		</row>
		<row>
			<slider id="my_slider" progress="0" progressmax="100" />
		</row>
	</layout>
	
<ct>layout.xml</ct>

	layout.my_toggle.checked = true;
	layout.my_label.text = "bar";
	layout.my_slider.progress = 50;

<ct>remote.lua</ct>



### Avancé
Pour des mises à jour de disposition avancées (par exemple, listes ou dialogues), utilisez plutôt [``libs.server.update``](./server.md#server_update).