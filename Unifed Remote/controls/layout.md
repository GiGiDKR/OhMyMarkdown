# Disposition
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [orientation](#orientation)
	* [défilement](#défilement)
	* [erreur](#erreur)
* [Style](#style)
* [Événements](#événements)
	* [au lancement](#au-lancement)
	* [volume bas](#volume-bas)
	* [volume haut](#volume-haut)
	* [reprendre](#reprendre)
	* [pause](#pause)



## Aperçu
Le fichier de disposition décrit les composants visuels d'une télécommande.



## Propriétés



### orientation
Verrouiller l'orientation de la disposition en utilisant ``portrait`` ou ``landscape``.

````xml
<layout orientation="portrait">

</layout>
````



### défilement
Définir le mode de défilement en utilisant ``none``, ``vertical``, ``horizontal``, et ``both``.

````xml
<layout scroll="vertical">

</layout>
````



### erreur
Afficher un message d'erreur au lieu d'une disposition correcte.

````xml
<layout error="Impossible de trouver les données requises.">

</layout>
````

Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).



## Style
Voir la page [style](styling.md) pour plus de détails.



## Événements



### au lancement
Se produit lorsque le bouton "launch" est pressé dans une télécommande.

````xml
<layout onlaunch="launch">

</layout>
````

````lua
actions.launch = function ()
    ...
end
````



### volume bas
Se produit lorsque le bouton "volume bas" est pressé sur l'appareil client.

````xml
<layout onvolumedown="volume_down">

</layout>
````

````lua
actions.volume_down = function ()
    ...
end
````



### volume haut
Se produit lorsque le bouton "volume haut" est pressé sur l'appareil client.

````xml
<layout onvolumeup="volume_up">

</layout>
````

````lua
actions.volume_up = function ()
    ...
end
````



### pause
Se produit lorsque l'appareil client souhaite mettre en pause (par exemple, un appel téléphonique reçu).

````xml
<layout onpause="pause">

</layout>
````

````lua
actions.pause = function ()
    ...
end
````



### reprendre
Se produit lorsque l'appareil client souhaite reprendre (par exemple, un appel téléphonique terminé).

````xml
<layout onresume="resume">

</layout>
````

````lua
actions.resume = function ()
    ...
end
````


