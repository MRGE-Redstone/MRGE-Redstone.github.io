# Crafting Transmute

If you want to preserve all components of an ingredient you have to use the [CraftingTransmute](https://minecraft.wiki/w/Recipe_(Java_Edition)#crafting_transmute) recipe type.

## Importing

You also import the ```CraftingTransmute``` class from ```MCpypack.recipe```.

```python
from MCpypack.recipe import CraftingTransmute
```

## New Recipe

The ```CraftingTransmute``` class takes the following required arguments.

- ```name``` -> ```str```: The name of the recipe.
- ```input``` -> ```ItemLike```: Item whose components will be copied.
- ```material``` -> ```ItemLike```: Additional item for the recipe.
- ```result``` -> ```ItemStack```: Result of the recipe.

You can also parse two optional arguments.

- ```group``` -> ```Group | None```: String identifier for grouping recipes. Default is ```None```.
- ```category``` -> ```CategoryLike```: Recipe book category. Default is ```Category.MISC```.

It will then look like this.

```python
mining.add_recipes(
    CraftingTransmute(
        name="shimmer",
        input=Item.DIAMOND_BLOCK,
        material=Item.AMETHYST_SHARD,
        result=ItemStack(
            item_id=Item.DIAMOND,
            components=components.ItemComponents(
                components.EnchantmentGlintOverride(True)
            )
        )
    )
)
```

> [!IMPORTANT]
> You need to import the following for this example.
> ```python
> from MCpypack import components
> ```

You now are able to use a diamond block and an amethyst shard to craft a diamond that shimmers and also copy the data of the diamond block.

You can also use it to keep enchantments on tools.

```python
mining.add_recipes(
    CraftingTransmute(
        name="always_copper",
        input=Tag.ITEM.PICKAXES,
        material=Item.COPPER_BLOCK,
        result=ItemStack(
            item_id=Item.COPPER_PICKAXE,
        )
    )
)
```

> [!IMPORTANT]
> You need to import the following for this example.
> ```python
> from MCpypack.item.final import Tag
> ```

You can now upgrade every pickaxe to a copper pickaxe.

> [!NOTE]
> You cannot insert a copper pickaxe as Minecraft does not allow to result to be the same as the input in ```CraftingTransmute``` recipes.

## Whole code

```python
from MCpypack import Datapack, Namespace, components
from MCpypack.recipe import CraftingTransmute
from MCpypack.utils import ItemStack
from MCpypack.item.final import Item, Tag

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

mining: Namespace = Namespace(
    name="mining"
)

mining.add_recipes(
    CraftingTransmute(
        name="shimmer",
        input=Item.DIAMOND_BLOCK,
        material=Item.AMETHYST_SHARD,
        result=ItemStack(
            item_id=Item.DIAMOND,
            components=components.ItemComponents(
                components.EnchantmentGlintOverride(True)
            )
        )
    ),
    CraftingTransmute(
        name="always_copper",
        input=Tag.ITEM.PICKAXES,
        material=Item.COPPER_BLOCK,
        result=ItemStack(
            item_id=Item.COPPER_PICKAXE,
        )
    )
)

my_recipes.add_namespaces(mining)

my_recipes.export()
```