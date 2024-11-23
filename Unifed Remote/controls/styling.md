# Style
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [couleur](#couleur)
	* [couleur claire / couleur foncée](#couleur-claire--couleur-foncée)
	* [clair / foncé](#clair--foncé)
* [Thème](#thème)
* [Couleurs](#couleurs)



## Aperçu
Les propriétés de style peuvent être utilisées pour changer l'apparence des contrôles.

````xml
<button color="red" />
````

Le style est hérité des grilles aux contrôles, donc définir le style d'un contrôle de conteneur définira le style des contrôles enfants.

````xml
<grid color="green" />
    <button text="vert!" />
    <button text="aussi vert!" />
</grid>
````
Si vous souhaitez colorer une rangée, faites ce qui suit.
````xml
<row>
    <grid color="green">
	    <button text="vert!" />
	    <button text="aussi vert!" />
    </grid>
</row>
````



## Propriétés



### couleur
Définir la [couleur standard](#couleurs) de base. Calcule automatiquement les variations de couleur pour les thèmes et les états.

````xml
<button color="blue" />
````




### couleur claire / couleur foncée
Pour les couleurs personnalisées en hexadécimal, définir la couleur de base pour lorsque l'application est dans le thème respectif. Calcule automatiquement les variations de couleur pour les états.

````xml
<button lightcolor="#cccccc" darkcolor="#444444" />
````



### clair / foncé
Pour des thèmes entièrement personnalisés, créer un spécificateur de thème.

````xml
<button light="color:#aaa;focus:#bbb;active:#ccc" />
````



## Thème
Les spécificateurs de thème sont formatés comme du CSS :

````
normal:#aaa;focus:#bbb;active:#ccc;color:#abcdef
````

Les propriétés suivantes peuvent être utilisées :

Propriété | Utilisation
-------- | ---
normal   | couleur par défaut
focus    | couleur pressée/focalisée
active   | couleur activée/toggle
color    | couleur du texte/de l'entrée




## Couleurs
Liste des couleurs standard qui peuvent être utilisées :

* red
* grey
* blue
* green
* orange
* purple
* pink
* yellow
* transparent
