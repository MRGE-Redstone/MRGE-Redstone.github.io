# Crafting Shaped

Now we will have a look at the [Crafting Shaped](https://minecraft.wiki/w/Recipe_(Java_Edition)#crafting_shaped) recipe type.

## Importing

First let's import the ```CraftingShaped``` class from ```MCpypack.recipe```.

```python
from MCpypack.recipe import CraftingShaped
```

> [!NOTE]
> Using ```CratingShaped``` requires the same additional imports as ```CraftinShapeless```.

## New Recipe

The ```CraftingShaped``` class takes the following required arguments.

- ```name``` -> ```str```: The name of the recipe.
- ```pattern``` -> ```list[str]```: Pattern representing the crafting grid.
- ```key``` -> ```dict[str, ItemLike]```: All keys used in ```pattern``` and the corresponding items.
- ```result``` -> ```ItemStack```: Result of the recipe.

You can also parse three optional arguments.

- ```group``` -> ```Group | None```: String identifier for grouping recipes. Default is ```None```.
- ```category``` -> ```CategoryLike```: Recipe book category. Default is ```Category.MISC```.
- ```show_notification``` -> ```bool | None```: Determines if a notification is shown when unlocking the recipe. Default is ```None```.

It will then look like this.

```python
grass.add_recipes(
    CraftingShaped(
        name="grow_grass",
        pattern=[
            "A",
            "A",
        ],
        key={"A": Item.SHORT_GRASS},
        result=ItemStack(
            item_id=Item.TALL_GRASS,
        )
    )
)
```

If you now place two short grass item above each other you get one tall grass.  
This recipe works even for a 2 by 2 crafting grid.  

## Full Grid

You can also extend it to a 3 by 3 grid.

For that we add a new namespace for mining.

```python
mining: Namespace = Namespace(
    name="mining"
)

my_recipes.add_namespaces(mining)
```

Now we create a new recipe in that namespace.

```python
mining.add_recipes(
    CraftingShaped(
        name="diamond_in_stone",
        pattern=[
            "AAA",
            "ABA",
            "AAA",
        ],
        key={
            "A": Item.STONE,
            "B": Item.DIAMOND,
        },
        result=ItemStack(
            item_id=Item.DIAMOND_ORE,
        )
    )
)
```

## Empty Fields

If you want to leave certain fields empty you just use a space for that in the string.

```python
mining.add_recipes(
    CraftingShaped(
        name="best_iron_pick",
        pattern=[
            "AAA",
            " B ",
            " B ",
        ],
        key={
            "A": Item.IRON_BLOCK,
            "B": Item.BLAZE_ROD,
        },
        result=ItemStack(
            item_id=Item.IRON_PICKAXE,
            components=components.ItemComponents(
                components.Unbreakable(),
                components.Enchantments({
                    Enchantment.EFFICIENCY: 10,
                })
            )
        )
    )
)
```

> [!IMPORTANT]
> For this example you also need to import the following:
> ```python
> from MCpypack import components
> from MCpypack.item.final import Enchantment
> ```

## Whole code

```python
from MCpypack import Datapack, Namespace, components
from MCpypack.recipe import CraftingShaped
from MCpypack.utils import ItemStack
from MCpypack.item.final import Item, Enchantment

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

grass: Namespace = Namespace(
    name="grass"
)

grass.add_recipes(
    CraftingShaped(
        name="grow_grass",
        pattern=[
            "A",
            "A",
        ],
        key={"A": Item.SHORT_GRASS},
        result=ItemStack(
            item_id=Item.TALL_GRASS,
        )
    )
)

mining: Namespace = Namespace(
    name="mining"
)

mining.add_recipes(
    CraftingShaped(
        name="diamond_in_stone",
        pattern=[
            "AAA",
            "ABA",
            "AAA",
        ],
        key={
            "A": Item.STONE,
            "B": Item.DIAMOND,
        },
        result=ItemStack(
            item_id=Item.DIAMOND_ORE,
        )
    ),
    CraftingShaped(
        name="best_iron_pick",
        pattern=[
            "AAA",
            " B ",
            " B ",
        ],
        key={
            "A": Item.IRON_BLOCK,
            "B": Item.BLAZE_ROD,
        },
        result=ItemStack(
            item_id=Item.IRON_PICKAXE,
            components=components.ItemComponents(
                components.Unbreakable(),
                components.Enchantments({
                    Enchantment.EFFICIENCY: 10,
                })
            )
        )
    )
)

my_recipes.add_namespaces(grass, mining)

my_recipes.export()
```