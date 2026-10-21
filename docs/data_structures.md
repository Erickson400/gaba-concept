# Data Structures File
The *_data_structures.gaba* file holds Structs and Unions for defining the layout of the RAM, and constant structures in ROM. This makes it trivial to write and read your source code similar to C.

## Structs
Structs let you define location constants for data in a tree like fashion. The type of field types are
- u8 &emsp; (1 byte)
- u16 &emsp; (2 bytes)
- string &emsp; (Size varies)
- another struct &emsp; (Size of the struct)
- another struct* &emsp; (2 bytes)

Pointer types are purely used for readability, that way you dont have to suffix your fields with "_ptr". Fields can also be arrays (e.g. u8[23]) except strings. Recursive structs are not allowed.

Strings are only allowed in ROM. Using a struct with a string field in RAM is not allowed. This is because the user most likely wants to type a string literal, and having to match an array's size to a string is cumbersome. Also making strings a pointer to another location adds hidden overhead.

```
Player :: struct {
    health: u8
    sprite_data: u16
    pad(2)              // Offset by 2 bytes
    items: u8[64]       // An array of 64 bytes
    align(2)            // Align to 2 bytes
}
// The Player struct will be 70 bytes.

Coin :: struct {
    normal_value: u8
    multiplier_value: u8
}
Level:: struct {
    player: Player
    coins: Coin[10]
}
// The Level struct will be 90 bytes long.
```

## Unions
Unions fields share RAM space. Useful for bank switching and game state changes to save on RAM.
```
Stuff :: union {
    player: Player
    coin: Coin
    some_ptrs: u16[4]
}
// The size of the union is the size of the largest field.
// In this case it's the size of player (70 bytes).
```

## Unique Structs and Unions
Unique structs and unions are where the final RAM layout will be specified and allocated.
### Unique Structs
```
wram :: unique struct  {
    stuff: Stuff
}
```
You can then use these allocated structs in your source code.
```
bc = wram.stuff  // Will be 0xC000
```
You can get the size of any field in a unique struct by using the implicit *.size* field.
```
bc = wram.stuff.player.items.size  // Will be 64 bytes
bc = wram.stuff.coin.size          // Will be 2 bytes
```
To get the end address of a field in a unique struct, use the implicit *.end* field.
```
bc = wram.stuff.player.sprite_data.end  // Will be 0xC004
```
The valid unique structs are
- vram
- sram
- wram
- oam
- hram

### Unique Unions
Unique unions are similar to unique structs, except they're only for banked RAM.
```
wramx :: unique union {
    bank1: Stuff
    another_bank: u16
}
```
They'll share address space. The namespacing helps the programmer explicetly write what data they're trying to access and prevents bank bugs.
The valid unique unions are
- vramx
- wramx

## Structs in ROM
You can allocate structs in ROM for read-only data in your source code.

Should I make a separate file for rodata allocations. Does that mean I need unions for bank switching.

 size and end allowe din ROM


strings