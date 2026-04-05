# Adding Namespaces

To add new namespaces to your datapack you use the ```Namespace``` class and the ```add_namespaces``` method from the ```Datapack``` class.

```py
my_namespace: Namespace = Namespace(name="my_namespace")

my_pack.add_namespaces(my_namespace)
```

Of course you can create multiple namespaces.

## Whole code

```py
from MCpypack import *

my_pack: Datapack = Datapack(
    name="My Datapack",
    description="My first datapack",
    version="26.1"
)

my_namespace: Namespace = Namespace(name="my_namespace")
my_pack.add_namespaces(my_namespace)

my_pack.export()
```