# Stonecutting

Next we will cover the [Stonecutting](https://minecraft.wiki/w/Recipe_(Java_Edition)#stonecutting) recipe type. It is the only recipe type for the stonecutter.

## Importing

We import the `Stonecutting` class from `MCpypack.recipe`.

```python
from MCpypack.recipe import Stonecutting
```

## New Recipe

The `Stonecutting` class takes the following required arguments.

- `name` -> `str`: The name of the recipe.
- `ingredient` -> `ItemLike`: Ingredient of the recipe.
- `result` -> `ItemStack`: Result of the recipe.

The `Stonecutting` class does not take any optional arguments.

It will look like this.

```python
Stonecutting(
    name="oak_stairs",
    ingredient=Item.OAK_PLANKS,
    result=ItemStack(
        item_id=Item.OAK_STAIRS,
    )
)
```

Now we can use a stonecutter to turn one oak plank into one oak stair.

## Whole Code
```python
from MCpypack import Datapack, ItemStack, Namespace
from MCpypack.item.final import Item
from MCpypack.recipe import Stonecutting

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

carpenter: Namespace = Namespace(
    name="carpenter"
)

carpenter.add_recipes(
    Stonecutting(
        name="oak_stairs",
        ingredient=Item.OAK_PLANKS,
        result=ItemStack(
            item_id=Item.OAK_STAIRS,
        )
    )
)

my_recipes.add_namespaces(carpenter)

my_recipes.export()
```