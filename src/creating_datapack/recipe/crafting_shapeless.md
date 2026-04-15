# Crafting Shapeless

The first recipe type we will have a look at is the [Crafting Shapeless](https://minecraft.wiki/w/Recipe_(Java_Edition)#crafting_shapeless).

## New Datapack and Namespace

Let's first create a new datapack for our new recipes we will add.

```python
my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)
```

We will also add a new namespace for recipes related to grass.

```python
grass: Namespace = Namespace(
    name="grass"
)
```

## Importing

Now we can at a ```CraftingShapeless``` recipe.  
We import it from ```MCpypack.recipe```.

```python
from MCpypack.recipe import CraftingShapeless
```

> [!NOTE]
> Using CratingShapeless also requires imports from other submodules which are:
> ```python
> from MCpypack.utils import ItemStack
> from MCpypack.item.final import Item
> ```

## New Recipe

The ```CraftingShapeless``` class takes the following required arguments.

- ```name``` -> ```str```: The name of the recipe.
- ```ingredients``` -> ```ItemLike | list[ItemLike]```: Ingredients of the recipe.
- ```result``` -> ```ItemStack```: Result of the recipe.

You can also parse two optional arguments.

- ```group``` -> ```Group```: String identifier for grouping recipes. Default is ```None```.
- ```category``` -> ```CategoryLike```: Recipe book category. Default is ```Category.MISC```.

It will then look like this.

```python
grass_block: CraftingShapeless = CraftingShapeless(
    name="grass_block",
    ingredients=[Item.DIRT, Item.SHORT_GRASS],
    result=ItemStack(
        item_id=Item.GRASS_BLOCK,
    )
)
```

## Add to Namespace

Then we just add the recipe into our namespace

```python
grass.add_recipes(grass_block)
```

> [!NOTE]
> You can also instantly add the recipe to the namespace.
> 
> ```python
> grass.add_recipes(
>     CraftingShapeless(
>         name="grass_block",
>         ingredients=[Item.DIRT, Item.SHORT_GRASS],
>         result=ItemStack(
>             item_id=Item.GRASS_BLOCK,
>         )
>     )
> )
> ```

## Export Datapack

Now we can export our datapack.

```python
my_recipes.add_namespaces(grass)

my_recipes.export()
```

If you now add it to your Minecraft world you should be able to craft a grass block using one dirt and one short grass item regardless of how you arrange them.

## Whole Code

```python
from MCpypack import Datapack, Namespace
from MCpypack.recipe import CraftingShapeless
from MCpypack.utils import ItemStack
from MCpypack.item.final import Item

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

grass: Namespace = Namespace(
    name="grass"
)

grass.add_recipes(
    CraftingShapeless(
        name="grass_block",
        ingredients=[Item.DIRT, Item.SHORT_GRASS],
        result=ItemStack(
            item_id=Item.GRASS_BLOCK,
        )
    )
)

my_recipes.add_namespaces(grass)

my_recipes.export()
```