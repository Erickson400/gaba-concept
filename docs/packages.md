# Packages
Gaba's project structure is similar to [Odin's](https://odin-lang.org/docs/overview/#packages). To paraphrase in Gaba terms:
```
Gaba programs consist of packages. A package is a directory of Gaba code files, all of which have the same package declaration at the top. The gaba build <dir> command takes all the files in the directory <dir>, compiles them into a package and then turns that into an executable. Execution starts in the package’s main procedure.
```
New packages are created inside the main package by creating a sub-folder. You can then use that sub-package in main or other sub-packages by importing them.

### Import statement
```
package main

import "core"
import "level"
```
You can then reference any entities from the level package in this file. Or from the built in "core" library with util functions.

### Exported names
All declarations in a package are public by default.
The private attribute can be applied to an entity to prevent it from being exported from a package.
```
@(private)
MY_CONST :: 74 // cannot be accessed outside this package

@(private="file")
MY_FILE_CONST :: 113 // cannot be accessed outside this file
```
It is good practice to keep things public, only make things private when a naming conflict occurs or if you're making a libray API.
