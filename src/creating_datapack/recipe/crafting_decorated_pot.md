# Crafting Decorated Pot

Next we will cover the [Crafting Decorated Pot](https://minecraft.wiki/w/Recipe_(Java_Edition)#crafting_decorated_pot) recipe type. It copies the four ingredients and saves them as the decorated pot component.

## Importing

We import the ```CraftingDecoratedPot``` class from ```MCpypack.recipe```.

```python
from MCpypack.recipe import CraftingDecoratedPot
```

## New Recipe

The ```CraftingDecoratedPot``` class takes the following required arguments.

- ```name``` -> ```str```: The name of the recipe.
- ```left``` -> ```ItemLike```: Left ingredient of the recipe.
- ```richt``` -> ```ItemLike```: Right ingredient of the recipe.
- ```front``` -> ```ItemLike```: Front ingredient of the recipe.
- ```back``` -> ```ItemLike```: Back ingredient of the recipe.
- ```result``` -> ```ItemStack```: Result of the recipe.

```left```, ```right```, ```front```, and ```back``` are the positions of the items. In a 3 by 3 crafting grid it would look like this:

```
" B " -> B = back
"L R" -> L = left; R = right
" F " -> F = front
```

It will then look like this.

```python
luxury.add_recipes(
    CraftingDecoratedPot(
        name="gold_inside_diamond",
        left=Item.GOLD_INGOT,
        right=Item.GOLD_INGOT,
        back=Item.GOLD_INGOT,
        front=Item.GOLD_INGOT,
        result=ItemStack(
            item_id=Item.DIAMOND
        )
    )
)
```

> [!IMPORTANT]
> Don't forget to create the ```luxury``` namespace.

## Whole Code

```python
from MCpypack import Datapack, Namespace
from MCpypack.recipe import CraftingDecoratedPot
from MCpypack.utils import ItemStack
from MCpypack.item.final import Item

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

luxury: Namespace = Namespace(
    name="luxury"
)

luxury.add_recipes(
    CraftingDecoratedPot(
        name="gold_inside_diamond",
        left=Item.GOLD_INGOT,
        right=Item.GOLD_INGOT,
        back=Item.GOLD_INGOT,
        front=Item.GOLD_INGOT,
        result=ItemStack(
            item_id=Item.DIAMOND
        )
    )
)

my_recipes.add_namespaces(luxury)

my_recipes.export()
```