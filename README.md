# ![Preview1](http://i.imgur.com/fIPNYkb.png) Crafting Guide

#### `craftguide` is the most comprehensive crafting guide on Minetest.
#### Consult the [Minetest Wiki](http://wiki.minetest.net/Crafting_guide) for more details.

This crafting guide is a blue book named *"Crafting Guide"* or a wooden sign.

This crafting guide features a **progressive mode**.
The progressive mode is a Terraria-like system that only shows recipes you can craft from items in inventory.
The progressive mode can be enabled with `craftguide_progressive_mode = true` in `minetest.conf`.

`craftguide` is also integrated in `sfinv` (Minetest Game inventory) when you enable it with
`craftguide_sfinv_only = true` in `minetest.conf`.

Use the command `/craft` to show the recipe(s) of the pointed node.

![Preview2](https://i.imgur.com/bToFH38.png)

---

## API

### Custom recipes

#### Registering a custom crafting type

```Lua
craftguide.register_craft_type("digging", {
	description = "Digging",
	icon = "default_tool_steelpick.png",
})
```

#### Registering a custom crafting recipe

```Lua
craftguide.register_craft({
	type   = "digging",
	width  = 1,
	output = "default:cobble 2",
	items  = {"default:stone"},
})
```

### Progressive mode

#### `craftguide.add_progressive_filter(function(recipes, player))`

This function adds a recipe filter when progressive mode is enabled.
The default `craftguide` filter will still be used.

Example function to hide recipes for items from a mod called "secretstuff":

```lua
craftguide.add_progressive_filter(function(recipes)
	local filtered = {}
	for _, recipe in ipairs(recipes) do
		if recipe.output:sub(1,12) ~= "secretstuff:" then
			filtered[#filtered + 1] = recipe
		end
	end

	return filtered
end)
```

#### `craftguide.set_progressive_filter(function(recipes, player))`

This function sets an unique recipe filter when progressive mode is enabled.
The default `craftguide` progressive filter will be overridden.

#### `craftguide.get_progressive_filters()`

This function returns all progressive filters that are applied to recipes in progressive mode.
