# Écran
* [screen](#screen-1)
* [capture (full)](#screencapture-)
* [capture (sub)](#screencapture-x-y-w-h-update--)
* [size](#screensize-)



## La bibliothèque screen
La bibliothèque ``screen`` permet de capturer facilement des captures d'écran.

````lua
-- Create a new buffer
local screen = require("screen");
````



### screen.capture( )
Capture toute la zone de l'écran.

````lua
res = screen.capture();
local x = res.x;
local y = res.y;
local w = res.w;
local h = res.h;
local image = res.image;
````



### screen.capture( x, y, w, h, [update]  )
Capture la zone spécifiée de l'écran.

````lua
res = screen.capture(0, 0, 400, 400);
local x = res.x;
local y = res.y;
local w = res.w;
local h = res.h;
local image = res.image;
````

Optionnellement, elle peut retourner uniquement la sous-zone qui a changé depuis l'appel précédent. Si aucun pixel n'a changé depuis l'appel précédent, l'image sera ``nil``. Les coordonnées et la taille retournées correspondront à la sous-zone qui a réellement changé.

````lua
res = screen.capture(0, 0, 400, 400, true);
if (res.image) then
  print("area changed");
else
  print("area same");
end
````



### screen.size( )
Obtenir la taille de l'écran.

````lua
w,h = screen.size();
````


