# Gaba-Concept
A concept/plan/idea for a Gameboy Color High Level Assembler. Weather it'll ever be made is uncertain. The architecture will keep changing as I learn more about Gameboy assemblers.
```
package main

main := proc() {
    a = 0xC
    if a == 5 {
        a += 21 + carry
        gotor infinite_loop
    } else if a = 0xC {
        test bit 2 in a
        if not zero {
            gotor main
        }
    }

    loop infinite_loop {
        a++
    }
    goto main
}
```
### Goals
Simplicity and redability is the main goal of the project. Unlike RGBDS which is rich in features, Gaba is tailored for developing GBC games with MBC5 enabled only. It's not recommended for decomps or hacks. The language should be enjoyable to write, and non-cryptic to read for a new developer, 

### Features
- Scopes
- Enums
- Structs
- Unions
- Arrays
- Procedures
- Strings
- Charmaps
- If/else
- Loop
- Switch statements

Inspired by [Odin](https://odin-lang.org/docs/overview/), [RGBDS](https://rgbds.gbdev.io/), and [GB.HLA](https://github.com/daid/GB.HLA).



