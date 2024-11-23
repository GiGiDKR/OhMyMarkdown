
# Disposition

Le fichier de disposition décrit les composants visuels d'une télécommande. Par exemple, les boutons, les listes, les curseurs, etc. que l'utilisateur voit lorsqu'il ouvre une télécommande dans l'application. La disposition est décrite en utilisant XML.

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout>
<row>
	<label id="my_label" text="this is a label" />
</row>
<row>
	<toggle id="my_toggle" text="this is a toggle button" />
</row>
<row>
	<slider id="my_slider" text="this is a slider" />
</row>
<row>
	<button text="foo" ontap="foo" />
	<button text="bar" ontap="bar" />
</row>
</layout>
```

## Actions en ligne

Les actions sont soit spécifiées en se référant au nom d'une action dans le fichier `remote.lua`, soit elles peuvent être définies en ligne. Les actions en ligne sont particulièrement importantes pour les actions qui doivent fonctionner même si le client n'est pas connecté à un serveur (par exemple Wake On LAN).
```xml
<!-- Action en ligne -->
<button text="foo" ontap="core.mouse.click" />

<!-- Action en ligne avec extras -->
<button text="foo" ontap="core.keyboard.press,wlin" />

<!-- Action de périphérique en ligne -->
<button text="foo" ontap="@wol" />

<!-- Envoi IR en ligne -->
<button text="Volume Up" ontap="@irsend,0000 0000 0000 ... 0000 0000 0000" />
```