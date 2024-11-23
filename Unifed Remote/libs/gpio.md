# GPIO
* [map](#gpiomap-name)
* [name](#gpioname-name)
* [index](#gpioindex-index)
* [header](#gpioheader-header)
* [capture](#capture-pin)
* [release](#release-pin)
* [releaseall](#releaseall)
* [pin](#gpioindex-index)
* [out](#gpioout-pin)
* [get](#gpioget-pin)
* [set](#gpioset-pin-value)
* [high](#gpiohigh-pin)
* [low](#gpiolow-pin)



## GPIO
La bibliothèque GPIO fournit un accès à l'interface GPIO (General Purpose Input Output) disponible sous Linux. La fonctionnalité de mappage des broches est actuellement disponible uniquement pour Raspberry Pi. La fonction "map" configure des tables de recherche pour trouver des broches par nom, index ou en-tête. Pour Raspberry Pi, l'index suit le même numéro que celui utilisé par [WiringPi](https://projects.drogon.net/raspberry-pi/wiringpi/).

### gpio.map( name )
Définit la carte des broches à utiliser.

	--définit la carte sur la carte Raspberry Pi
	gpio.map("ip");

### gpio.name( name )
Obtenir une broche de la carte définie par le ``name``.

	pin = gpio.name("SDA");

### gpio.index( index )
Obtenir une broche par l'``index`` de la broche.

	pin = gpio.index(5);

### gpio.header( header )
Le numéro d'``header`` de la broche.

	pin = gpio.header(5);

### gpio.capture( pin )
Capturer les broches lorsque vous souhaitez les contrôler, donnez la méthode une ``pin`` à capturer. Aucune autre application ne peut utiliser la broche.

	pin = gpio.index(5);
	gpio.capture(pin);

### gpio.release( pin )
Libérer la ``pin`` au système d'exploitation.

	pin = gpio.index(5);
	gpio.release(pin);

### gpio.in( pin )
Définir la direction de la ``pin`` comme une broche d'entrée.

	pin = gpio.index(5);
	gpio.in(pin);

### gpio.out( pin )
Définir la direction de la ``pin`` comme une broche de sortie.

	pin = gpio.index(5);
	gpio.out(pin);

### gpio.get( pin )
Vérifier si la ``pin`` est haute ou basse. Retourne true si la ``pin`` est haute.

	pin = gpio.index(5);
	res = gpio.get(pin);

### gpio.set( pin, value )
Définir la ``pin`` sur haute ou basse. Définir ``value`` sur true si la broche doit être haute.

	pin = gpio.index(5);
	--broche définie sur haute
	gpio.set(pin, true);
	--broche définie sur basse
	gpio.set(pin, false);

### gpio.high( pin )
Définir la ``pin`` sur haute.

	pin = gpio.index(5);
	--broche définie sur haute
	gpio.high(pin);

### gpio.low( pin )
Définir la ``pin`` sur basse.

	pin = gpio.index(5);
	--broche définie sur basse
	gpio.low(pin);