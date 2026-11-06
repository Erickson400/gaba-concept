# Loops
Loops are used to iterate over a block of code. There are three ways to loop.
```
// Infinite loop
loop {

}

// Loop while a condition is met when it starts.
// Similar to a C while loop.
loop while not zero {

}

// Loop while a condition is met when it finishes.
// Similar to a C do-while loop.
loop {

} while a > 5
```
You can use the *continue* and *break* keywords to skip an iteration or leave the loop.
```
:column_iter: loop {                    // Labeled loop for nested continue/break
    loopr {                             // Loop with relative jumps.
        break                           // Loops without labels break from their current scope.
        break column_iter if not carry  // Conditional break
    } 
    continue if a == 0                  // Conditional continue
}

// RGBDS equivalent
column_iter:
nested_loop:
    jr nested_loop.break
    jr nc, column_iter.break
    jr nested_loop
nested_loop.break:
    cp 0
    jp z, column_iter
    jp column_iter
column_iter.break:
```


