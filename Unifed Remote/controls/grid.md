# Grille
* [Aperçu](#aperçu)
* [Grilles imbriquées](#grilles-imbriquées)
* [Poids](#poids)
* [Espaces](#espaces)
* [Style](#style)



## Aperçu
Le contrôle de grille est le principal contrôle de conteneur utilisé dans les télécommandes. Il a des rangées,
où chaque rangée contient un ou plusieurs contrôles disposés en colonnes. Une mise en page contient toujours
un contrôle de grille par défaut, vous pouvez donc commencer par ajouter des rangées directement.

````xml
<layout>
    <row>
        <button text="a" />
        <button text="b" />
    </row>
    <row>
        <button text="c" />
        <button text="d" />
    </row>
</layout>
````



## Grilles imbriquées
Les grilles peuvent également contenir des grilles imbriquées pour créer des mises en page plus complexes.

````xml
<layout>
    <row>
        <button text="a" />
        <grid>
            <row>
                <button text="b" />
            </row>
            <row>
                <button text="c" />
            </row>
        </grid>
        <button text="d" />
    </row>
</layout>
````



## Poids
Utilisez le poids pour contrôler la largeur et la hauteur des cellules. Par défaut, les cellules
s'étendent pour remplir tout l'espace disponible de manière égale. Vous pouvez utiliser des poids pour
redistribuer comment l'espace est utilisé par les différentes cellules.

````xml
<layout>
    <row>
        <button text="a" weight="1" />
        <button text="b" weight="2" />
    </row>
</layout>
````

Vous pouvez également appliquer des poids aux rangées pour redistribuer leurs hauteurs.

````xml
<layout>
    <row weight="1">
        <button text="a" />
    </row>
    <row weight="2">
        <button text="a" />
    </row>
</layout>
````

Utilisez ``wrap`` pour que les cellules s'ajustent à la taille de leur contenu.

````xml
<layout>
    <row>
        <button text="a" weight="wrap" />
        <button text="b" />
    </row>
</layout>
````



## Espaces
Les espaces peuvent être utilisés pour créer des cellules vides.

````xml
<layout>
    <row>
        <button text="a" />
        <space />
        <button text="b" />
    </row>
</layout>
````



## Style
Voir la page [style](../concepts/styling.md) pour plus de détails.


