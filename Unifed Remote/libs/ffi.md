# FFI
* [Déclaration de fonctions](#déclaration-de-fonctions)
* [Fonctions système standard](#fonctions-système-standard)
* [Fonctions externes](#fonctions-externes)
* [Exemples](#exemples)
	* [Typedefs Windows](#typedefs-windows)
	* [Passage de structures](#passage-de-structures)
	* [Passage de chaînes](#passage-de-chaînes)
	* [Accès aux structures](#accès-aux-structures)
	* [Exemples de télécommandes](#exemples-de-télécommandes)


## ffi
La bibliothèque ``ffi`` fournit une interface d'appel de fonctions étrangères.

	local ffi = require("ffi");

Consultez la [documentation officielle de LuaJIT](http://luajit.org/ext_ffi.html) pour plus de détails.



### Déclaration de fonctions
Vous devez d'abord déclarer les fonctions que vous souhaitez utiliser. Consultez les en-têtes ou la documentation de la bibliothèque que vous souhaitez accéder.

	ffi.cdef[[
	void foo(int bar);
	]]


### Fonctions système standard
Pour appeler des fonctions système standard, utilisez ``ffi.C``. Sous Windows, cela inclut des fonctions dans des DLL courantes telles que User32 et Kernel32.

	ffi.cdef[[
	void Sleep(int ms);
	]]

	ffi.C.Sleep(1000);


### Fonctions externes
Pour appeler des fonctions de bibliothèque externes, vous devez d'abord charger la bibliothèque.

	ffi.cdef[[
	bool SetSuspendState(bool hibernate, bool forceCritical, bool disableWakeEvent);
	]]

	local pp = ffi.load("PowrProf");

	pp.SetSuspendState(true, true, false);


## Exemples

### Typedefs Windows
Notez que les typedefs Windows standard doivent être déclarés explicitement.

	ffi.cdef[[
	typedef void* HWND;
	HWND GetDesktopWindow();
	]]

	local hwnd = ffi.C.GetDesktopWindow();


### Passage de structures
L'exemple suivant montre comment créer une structure et la passer en tant que pointeur.

	ffi.cdef[[
	typedef void* HWND;
	typedef long LONG;
	typedef struct {
		LONG x;
		LONG y;
	} POINT;
	HWND WindowFromPoint(POINT Point);
	]]

	local pos = ffi.new("POINT", 123, 456);
	local hwnd = ffi.C.WindowFromPoint(pos);


### Passage de chaînes
L'exemple suivant montre comment créer une chaîne et la passer en tant que pointeur.

	ffi.cdef[[
	typedef void* HWND;
	int GetWindowTextA(HWND hwnd, char* text, int maxCount);
	]]

	local hwnd = 12345;
	local text = ffi.new("char[255]");
	ffi.C.GetWindowTextA(hwnd, text, 255);
	text = ffi.string(text, 255);


### Accès aux structures
L'exemple suivant montre comment accéder aux membres d'une structure.

	ffi.cdef[[
	typedef void* HWND;
	typedef long LONG;
	typedef struct {
		LONG left;
		LONG top;
		LONG right;
		LONG bottom;
	} RECT;
	bool GetWindowRect(LONG hwnd, RECT* rect);
	]]

	local hwnd = 12345;
	local rect = ffi.new("RECT", 0, 0, 0, 0);
	ffi.C.GetWindowRect(hwnd, rect);

	local width = rect.right - rect.left;
	local height = rect.bottom - rect.top;


### Exemples de télécommandes
Quelques exemples de télécommandes utilisant la bibliothèque FFI :

* [Pixel](https://github.com/unifiedremote/Remotes/tree/master/Main/Pixel)
* [Power](https://github.com/unifiedremote/Remotes/tree/master/Main/Power)
* [Spy](https://github.com/unifiedremote/Remotes/tree/master/Main/Spy)
* [Spotify Advanced](https://github.com/unifiedremote/Remotes/tree/master/Main/Spotify%20Advanced)
* [TellStick](https://github.com/unifiedremote/Remotes/tree/master/Main/TellStick)
* [USB-UIRT](https://github.com/unifiedremote/Remotes/tree/master/Main/USB-UIRT)
