# Dialogues

## Dialogue de liste
````lua
local items = {
	{ type = "item", text = "élément 1" },
	{ type = "item", text = "élément 2" },
	{ type = "item", text = "élément 3" }
};

server.update({ id = "list", ontap = "mondialogue", children = items });

actions.mondialogue = function(i)
        -- if (i == 0) then élément 1 ...
end

````

## Dialogue de message

````lua
server.update({ 
	type = "dialog", 
	text = "Bonjour le monde!", 
	ontap = "mondialogue",
	children = {
		{ type = "button", text = "Foo" },
		{ type = "button", text = "Bar" }
	}
});

actions.mondialogue = function(i)
        -- if (i == 0) then Foo! ...
end

````

## Dialogue de saisie

````lua
server.update({
	id = "mondialoguesaisie",
	type = "input",
	title = "Écrivez quelque chose!", 
	ontap = "mondialoguesaisie_fini"
});

actions.mondialoguesaisie_fini = function(txt)
        if (is_valid(txt)) then 
		fancy_stuff(txt) ...
	end
end

````
