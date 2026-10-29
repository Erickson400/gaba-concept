# Loops
Loops create an infinite loop. You can use the *continue* and *break* keywords to skip an iteration or leave the loop.
```
my_loop := loop {
    loopr {                         // Loop with relative jumps.
        break                       // Anoymous loops break from their current scope.
        break my_loop if not carry  // You can continue/break from a parent loop.
    } 
    continue if a == 0
}

// RGBDS equivalent
my_loop:
nested_loop:
    jr nested_loop.break
    jr nc, my_loop.break
    jr nested_loop
nested_loop.break:
    cp 0
    jp z, my_loop
    jp my_loop
my_loop.break:
```


