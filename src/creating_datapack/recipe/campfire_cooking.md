# Campfire Cooking

Now we will have a look at the [Campfire Cooking](https://minecraft.wiki/w/Recipe_(Java_Edition)#campfire_cooking) recipe type. It is the only recipe type for the campfire.

## Importing

We import the `CampfireCooking` class from `MCpypack.recipe`.

```python
from MCpypack.recipe import CampfireCooking
```

## New Recipe

The `CampfireCooking` class takes the following required arguments.

- `name` -> `str`: The name of the recipe.
- `ingredient` -> `ItemLike`: Ingredient of the recipe.
- `result` -> `ItemStack`: Result of the recipe.

> [!WARNING]
> In versions before 26.1 the count field was not allowed for the result.

You can also parse two optional arguments.

- `cookingtime` -> `Time`: Cookingtime in real-life time values. Default is `None`.
- `experience` -> `Experience`: The output experience of the recipe. Default is `None`.

It will then look like this.

```python
CampfireCooking(
    name="edible_gold",
    ingredient=Item.GOLD_BLOCK,
    result=ItemStack(
        item_id=Item.GOLD_INGOT,
        count=2,
        components=components.ItemComponents(
            components.Consumable(),
            components.Food(
                nutrition=20,
                saturation=20.0,
                can_always_eat=True,
            )
        )
    ),
    cookingtime=Time(Seconds(90)),
    experience=25,
)
```

Now we are able to put gold blocks onto a campfire and as a result we get two edible pieces of gold ingots, which are a very strong source of food.

## Whole Code
```python
from MCpypack import Datapack, Namespace, Seconds, components, Time
from MCpypack.item.final import Item
from MCpypack.recipe import CampfireCooking
from MCpypack.utils import ItemStack

my_recipes: Datapack = Datapack(
    name="My Recipes",
    description="Adding missing recipes to make the world a better place.",
    version="26.1",
)

luxury: Namespace = Namespace(
    name="luxury"
)

luxury.add_recipes(
    CampfireCooking(
        name="edible_gold",
        ingredient=Item.GOLD_BLOCK,
        result=ItemStack(
            item_id=Item.GOLD_INGOT,
            count=2,
            components=components.ItemComponents(
                components.Consumable(),
                components.Food(
                    nutrition=20,
                    saturation=20.0,
                    can_always_eat=True,
                )
            )
        ),
        cookingtime=Time(Seconds(90)),
        experience=25,
    )
)

my_recipes.add_namespaces(luxury)

my_recipes.export()
```