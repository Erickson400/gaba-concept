# Procedures
Procedures are used as subroutines. They have an implicit return instruction at the end.

```
add1 := proc {
    a++
}

call add1

// RGBDS equivalent
add1:
    inc a
    ret

    call add1

```



