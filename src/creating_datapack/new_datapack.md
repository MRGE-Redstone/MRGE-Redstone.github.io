# Creating a new Datapack

In order to create a new datapack you first have to import MCpypack.

```py
from MCpypack import *
```

Then you create a new datapack object using the Datapack class.

The Datapack class takes 5 arguments.  
Out of them 3 are required and 2 are optional.

- Required:
    - name: Name of the datapack.
    - description: Description of the datapack.
    - version: The Minecraft version the datapack should be created for.

```py
my_pack: Datapack = Datapack(
    name="My Datapack",
    description="My first datapack",
    version="26.1"
)
```

- Optional:
    - relative_icon_path: Relative path to an icon that should be used for your datapack.
    - relative_export_dir: Directory to export the datapack to. Default is ```export/```.

In the end you have to export your datapack using the ```export``` method.

```py
my_pack.export()
```

There are 2 optional parameters for this method.
- overwrite: Whether the old version should be overwritten ```(True)``` or get a different name ```(False)```. Default is ```True```.
- zip: Whether a ```.zip``` should be created. Default is ```True```.

## Whole code

```py
from MCpypack import *

my_pack: Datapack = Datapack(
    name="My Datapack",
    description="My first datapack",
    version="26.1"
)

my_pack.export()
```