# Enums
Enums hold numeric constants that can later be used in your code to describe types or offsets.

```
TileType :: enum {
    Ground
    Water
    Pickup
    Door 
}

a = TileType.Water  // Same as "a = 1" 
```
You have the options to add an initial offset, or a step amount. 
```
Tile :: enum by 16 {
    Ground = 0x8000
    Water         // 0x8010
    Pickup        // 0x8020
    Door          // 0x8030
}
hl = Tile.Pickup  // Same as "hl = 0x8020" 
```
## EBNF Specs
```
enum = enum_head, enum_body, enum_tail ;

enum_head = ws, enum_name, ws, "::", ws, "enum", [" by ", integer], ws, "{", ws, [comment], EOL ;

enum_body = [enum_member_with_initial_value], {enum_member} ;

enum_member = ws, member_name, ws, [comment], EOL ;

enum_member_with_initial_value = ws, member_name, ws, "=", ws, integer, ws, [comment], EOL ;

enum_tail = ws, "}", ws, [comment], EOL ;
```
