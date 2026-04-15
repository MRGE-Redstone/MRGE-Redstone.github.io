# Adding Namespaces

You learned how to create your first datapack.
Now we want to add namespaces to that datapack.

## Importing Namespaces

To add new namespaces to your datapack you use the ```Namespace``` class and the ```add_namespaces``` method from the ```Datapack``` class.
To do this we have to also import the Namespace class from MCpypack.

```py
from MCpypack import Datapack, Namespace
```

## Creating Namespaces

After that we can create a new datapack with a custom name.

```py
my_namespace: Namespace = Namespace(name="my_namespace")

my_pack.add_namespaces(my_namespace)
```

> [!NOTE]
> The ```name``` is currently the only argument the class accepts, but it is still recommended to use keyword arguments here.

Of course you can create multiple namespaces.
```py
my_first_namespace: Namespace = Namespace(name="my_first_namespace")
my_second_namespace: Namespace = Namespace(name="my_second_namespace")

my_pack.add_namespaces(
    my_first_namespace,
    my_second_namespace,
)
```

> [!NOTE]
> As you may have noticed we didn't include any whitespaces ot other special characters in the names of our namespaces. This is because Minecraft has a special set of [rules](https://minecraft.wiki/w/Tutorial:Creating_a_data_pack#Legal_characters) what characters namespace names can include.

## Overwriting Game Content

Later you may want to change certain predefined aspects of the game like recipes.
To do that you have to create a new namespace named ```minecraft```.

## Whole Code

```py
from MCpypack import Datapack, Namespace

my_pack: Datapack = Datapack(
    name="My Datapack",
    description="My first datapack",
    version="26.1"
)

my_namespace: Namespace = Namespace(name="my_namespace")
my_pack.add_namespaces(my_namespace)

my_pack.export()
```