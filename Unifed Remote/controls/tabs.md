# Onglets
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [index](#index)
* [Style](#style)
* [Événements](#événements)
	* [onchange](#onchange)


## Aperçu
Le contrôle des onglets fonctionne comme une grille sauf qu'il peut avoir plusieurs pages d'onglets.
Chaque page d'onglet peut avoir un titre et est un contrôle de grille, vous pouvez donc ajouter des rangées directement.

````xml
<layout>
    <tabs>
        <tab text="Page 1">
            <row>
                <button />
            </row>
        </tab>
        <tab text="Page 2">
            <row>
                <button />
            </row>
        </tab>
        <tab text="Page 3">
            <row>
                <button />
            </row>
        </tab>
    </tabs>
</layout>
````



## Propriétés



### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md).

````xml
<tabs id="my_toggle">
    ...
</tabs>
````



### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<tabs visibility="gone">
    ...
</tabs>
````



### texte
Définir le titre d'une page d'onglet.

````xml
<tabs>
    <tab text="foo">
        ...
    </tab>
</tabs>
````



### index
Définir le numéro de l'onglet actif (basé sur zéro).

````xml
<tabs index="1">
    <tab>...</tab>
    <tab>...</tab>
    <tab>...</tab>
</tabs>
````



## Style
Voir la page [style](styling.md) pour plus de détails.



## Événements



### onchange
Se produit lorsque la page d'onglet active change.

````xml
<tabs onchange="update">
    ...
</tabs>
````

````lua
actions.update = function (index)
    ...
end
````


