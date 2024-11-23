# Système de fichiers (FS)
* [Bibliothèque `fs`](#bibliothèque-fs)
* [Contexte](#contexte)
    * [remotefile](#fsremotefile)
    * [remotedir](#fsremotedir)
    * [workingdir](#fsworkingdir)
* [Répertoires](#répertoires)
    * [homedir](#fshomedir)
    * [appdir](#fsappdir)
    * [special](#fsspecial-csidl)
* [Commun](#commun)
    * [name](#fsname-path)
    * [fullname](#fsfullname-path)
    * [extension](#fsextension-path)
    * [exists](#fsexists-path)
    * [copy](#fscopy-source-destination)
    * [move](#fsmove-source-destination)
    * [rename](#fsrename-source-destination)
    * [delete](#fsdelete-path-recursive--false)
* [Chemin](#chemin)
    * [parent](#fsparent-path)
    * [expand](#fsexpand-path)
    * [path](#fspath-str)
    * [combine](#fscombine-a-b)
    * [absolute](#fsabsolute-rel)
    * [temp](#fstemp)
* [Arborescence](#arborescence)
    * [roots](#fsroots)
    * [files](#fsfiles-path-hidden)
    * [dirs](#fsdirs-path-hidden)
    * [list](#fslist-path-hidden)
* [Créer](#créer)
    * [createdir](#fscreatedir-path)
    * [createdirs](#fscreatedirs-path)
    * [createfile](#fscreatefile-path)
* [Lire et écrire](#lire-et-écrire)
    * [write](#fswrite-path-content)
    * [writelines](#fswritelines-path-lines)
    * [append](#fsappend-path-content)
    * [appendlines](#fsappendlines-path-lines)
    * [read](#fsread-path)
    * [readlines](#fsreadlines-path)
* [Attributs](#attributs)
    * [isfile](#fsisfile-path)
    * [isdir](#fsisdir-path)
    * [ishidden](#fsishidden-path)
    * [size](#fssize-path)
    * [created](#fscreated-path)
    * [modified](#fsmodified-path)


## Bibliothèque `fs`
La bibliothèque ``fs`` fournit des fonctions essentielles du système de fichiers pour les fichiers et les dossiers.

````lua
local fs = require("fs");
````



## Contexte



### fs.remotefile
Retourne le chemin vers le fichier distant actuel.

````lua
path = fs.remotefile();
````



### fs.remotedir
Retourne le chemin vers le répertoire distant actuel.

````lua
path = fs.remotedir();
````



### fs.workingdir
Retourne le chemin vers le répertoire de travail.

````lua
path = fs.workingdir();
````



## Répertoires



### fs.homedir
Retourne le chemin vers le répertoire personnel de l'utilisateur.

````lua
path = fs.homedir();
````



### fs.appdir
Retourne le chemin vers le répertoire du serveur.

````lua
path = fs.appdir();
````



### fs.special( csidl )
Retourne le chemin du dossier spécial spécifié par ``csidl`` (entier ou chaîne).

````lua
path = fs.special("startmenu");
path = fs.special("csidl_startmenu");
````

Consultez [MSDN](http://msdn.microsoft.com/en-us/library/windows/desktop/bb762494.aspx) pour une liste des valeurs CSIDL.



## Commun



### fs.name( path )
Retourne le nom (sans extension) du ``path`` spécifié.

````lua
--name sera "log"
name = fs.name("c:\\temp\\log.txt");
````



### fs.fullname( path )
Retourne le nom complet (y compris l'extension) du ``path`` spécifié.

````lua
--fullname sera "log.txt"
fullname = fs.fullname("c:\\temp\\log.txt");
````


### fs.extension( path )
Retourne l'extension du ``path`` spécifié.

````lua
--ext sera "txt"
ext = fs.extension("c:\\temp\\log.txt");
````



### fs.exists( path )
Retourne true si ``path`` existe.

````lua
exists = fs.exists();
````



### fs.copy( source, destination )
Copie le fichier ou le dossier de ``source`` vers ``destination``.

````lua
fs.copy("c:\\temp\\log.txt", "c:\\temp2\\log.txt");
````



### fs.move( source, destination )
Déplace le fichier ou le dossier de ``source`` vers ``destination``.

````lua
fs.move("c:\\temp\\log.txt", "c:\\temp2\\log.txt");
````



### fs.rename( source, destination )
Renomme le fichier ou le dossier de ``source`` vers ``destination``.

````lua
fs.rename("c:\\temp\\log.txt", "c:\\temp\\log2.txt");
````



### fs.delete( path, [recursive = false] )
Supprime le fichier ou le dossier situé à ``path``. Définissez ``recursive`` sur true si tous les fichiers et dossiers situés à ce chemin doivent être supprimés. Si le dossier contient des fichiers ou des sous-dossiers et que ``recursive`` est défini sur false, le dossier ne sera pas supprimé.

````lua
--supprime le fichier log.txt
fs.delete("c:\\temp\\log.txt");
--supprime tous les fichiers et dossiers situés dans temp
fs.delete("c:\\temp\\", true);
````



## Chemin



### fs.parent( path )
Retourne le chemin du répertoire parent situé à ``path``.

````lua
parent = fs.parent("c:\\temp");
````



### fs.expand( path )
Développe un ``path``.

````lua
fs.expand("c:\\temp\\newfile.txt");
````



### fs.path( str )
Convertit une chaîne ``str`` en un chemin valide.

````lua
--retourne "c:\\temp\\log.txt" sous Windows.
path = fs.path("c:\\temp/log.txt");
````



### fs.combine( a, b )
Combine le chemin ``a`` avec le chemin ``b`` en gérant l'absence de barre oblique entre les chemins.

````lua
--combined sera "c:\\temp\\log.txt"
combined = fs.fullname("c:\\temp", "log.txt");
````



### fs.absolute( rel )
Étant donné un chemin relatif ``rel``, le chemin absolu est retourné.

````lua
--abs sera "c:\\temp\\log.txt" si la télécommande est située à "c:\\temp"
abs = fs.absolute("log.txt");
````



### fs.temp()
Retourne un nom de chemin unique pour un fichier temporaire dans le répertoire de travail du système.

````lua
path = fs.temp();
````



## Arborescence



### fs.roots
Retourne un tableau de tous les répertoires racine disponibles.

````lua
roots = fs.roots();
````



### fs.files( path, [hidden] )
Retourne un tableau de fichiers situés au ``path`` spécifié.

````lua
files = fs.files("c:\\");

--Imprime les chemins de tous les fichiers dans le répertoire
for i = 1, #files do
    print(files[i]);
end
````



### fs.dirs( path, [hidden] )
Retourne un tableau de sous-répertoires situés au ``path`` spécifié.

````lua
dirs = fs.dirs("c:\\");

--Imprime les chemins de tous les sous-répertoires dans le répertoire
for i = 1, #dirs do
    print(dirs[i]);
end
````



### fs.list( path, [hidden] )
Retourne un tableau de sous-répertoires et de fichiers situés au ``path`` spécifié.

````lua
items = fs.list("c:\\");

--Imprime les chemins de tous les sous-répertoires et fichiers dans le répertoire
for i = 1, #items do
    print(items[i]);
end
````



## Créer



### fs.createdir( path )
Crée le répertoire ``path``.

````lua
--si c:\temp\ existe, alors "newdir" est créé.
fs.createdir("c:\\temp\\newdir");
````



### fs.createdirs( path )
Crée le répertoire ``path`` et tous les parents requis.

````lua
--si c:\temp\ existe, alors "newdir" et "anotherdir" sont créés.
fs.createdirs("c:\\temp\\newdir\\anotherdir");
````



### fs.createfile( path )
Crée un fichier ``path``.

````lua
--un fichier "newfile.txt" est créé.
fs.createdirs("c:\\temp\\newfile.txt");
````



## Lire et écrire



### fs.write( path, content )
Écrit dans un fichier. ``path`` le fichier dans lequel écrire et ``content`` les informations à écrire dans le fichier.

````lua
fs.write("c:\\temp\\log.txt", "Ceci est du contenu");
````



### fs.writelines( path, lines )
Écrit une liste de ``lines`` dans un fichier situé à ``path``.

````lua
fs.write("c:\\temp\\log.txt", {"Ligne 1", "Ligne 2"});
````



### fs.append( path, content )
Ajoute une chaîne contenant ``content`` à un fichier situé à ``path``.

````lua
fs.append("c:\\temp\\log.txt", "nouveau contenu");
````



### fs.appendlines( path, lines )
Ajoute une liste de ``lines`` à un fichier situé à ``path``.

````lua
fs.appendlines("c:\\temp\\log.txt", {"ligne3", "ligne4"});
````



### fs.read( path )
Lit le contenu entier d'un fichier. ``path`` le fichier à lire.

````lua
content = fs.read("c:\\temp\\log.txt");
````



### fs.readlines( path )
Retourne une liste de lignes dans le fichier situé à ``path``.

````lua
lines = fs.readlines("c:\\temp\\log.txt");
````



## Attributs



### fs.isfile( path )
Vérifie si un ``path`` est un fichier ou non. Retourne true si ``path`` est un fichier.

````lua
--retourne true car "newfile.txt" est un fichier
res = fs.isfile("c:\\temp\\newfile.txt");
--retourne false car "c:\\temp\\" n'est pas un fichier
res = fs.isfile("c:\\temp\\");
````



### fs.isdir( path )
Vérifie si un ``path`` est un répertoire ou non. Retourne true si ``path`` est un répertoire.

````lua
--retourne false car "newfile.txt" n'est pas un répertoire
res = fs.isdir("c:\\temp\\newfile.txt");
--retourne true car "c:\\temp\\" est un répertoire
res = fs.isdir("c:\\temp\\");
````



### fs.ishidden( path )
Vérifie si le fichier ou le répertoire situé à ``path`` est masqué par le système de fichiers.

````lua
--retourne true si le fichier est masqué.
res = fs.ishidden("c:\\temp\\newfile.txt");
````



### fs.size( path )
Retourne la taille d'un fichier ou d'un répertoire situé à ``path``.

````lua
size = fs.size("c:\\temp\\newfile.txt");
````



### fs.created( path )
Retourne l'heure de création du fichier ou du répertoire situé à ``path``.

````lua
time = fs.created("c:\\temp\\newfile.txt");
````



### fs.modified( path )
Retourne l'heure de modification du fichier ou du répertoire situé à ``path``.

````lua
time = fs.modified("c:\\temp\\newfile.txt");
````


