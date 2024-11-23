# Liste
* [Aperçu](#aperçu)
* [Propriétés](#propriétés)
	* [id](#id)
	* [visibilité](#visibilité)
	* [texte](#texte)
	* [icône](#icône)
	* [image](#image)
* [Événements](#événements)
	* [ontap](#ontap)
	* [onhold](#onhold)

## Aperçu
Le contrôle de liste fournit un moyen facile d'afficher de grandes quantités de données.

````xml
<layout>
    <list>
        <item text="élément 1" />
        <item text="élément 2" />
        <item text="élément 3" />
        ...
    </list>
</layout>
````

## Propriétés

### id
Définir l'ID pour ce contrôle afin qu'il puisse être mis à jour plus tard. Voir [bibliothèque de mise en page](../libs/layout.md#mise-à-jour).

````xml
<list id="my_toggle">
    ...
</list>
````

### visibilité
Définir l'état de visibilité en utilisant ``visible`` ou ``invisible`` ou ``gone``.

````xml
<list visibility="gone">
    ...
</list>
````

### texte
Définir le texte à afficher dans un élément.

````xml
<list>
    <item text="foo" />
    <item text="bar" />
</list>
````

Les éléments peuvent également afficher du sous-texte en utilisant le délimiteur ``\n``.

````xml
<list>
    <item text="foo\nbar" />
    <item text="hello\nworld" />
</list>
````

### icône
Définir l'icône à afficher dans un élément. Voir [liste des icônes](../res/icons.md#icônes) des icônes disponibles.

````xml
<list>
    <item icon="select" text="foo" />
    <item icon="select" text="bar" />
</list>
````

### image
Définir une image personnalisée à afficher dans un élément. Doit être un chemin relatif au fichier de mise en page.

````xml
<list>
    <item image="img.png" text="foo" />
    <item image="img.png" text="bar" />
</list>
````

## Événements

### ontap
Se produit lorsqu'un élément est tapé.

````xml
<list ontap="tapped">
    ...
</list>
````

````lua
actions.tapped = function (index)
    ...
end
````

### onhold
Se produit lorsqu'un élément est maintenu enfoncé.

````xml
<list onhold="held">
    ...
</list>
````

````lua
actions.held = function (index)
    ...
end
````


