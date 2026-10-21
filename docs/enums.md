# Enums File
The *_enums.gaba* file holds enums for numeric constants that can later be used in your assembly code as flags.

## Enums
```
// In _enums.gaba
TileType :: enum {
    Ground = 4  // Optional initial value
    Water
    Pickup
    Door
}
```
```
// In your assembly code
a = TileType.Water
```
Enums can range from 0 to 255, if it overflows it'll wrap around. Even though they have an 8-bit range, they can be used in instructions that take n16 or u3 values. An error will be thrown in the case you pass an enum value greater than 7 for u3.

