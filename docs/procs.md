# Procedures
Procedures are used as subroutines. They have an implicit return instruction, and have the ability to pushpop r16 registers.

```
add1 := proc(bc, de) {
    a++
}

// Equivalent to the above.
add1 := {
    push bc
    push de
    a++
    pop de
    pop bc
    ret
}
```



