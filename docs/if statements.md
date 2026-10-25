# If statements
If statements abstract conditional jumps. They take one condition and enter the scope if met.
## Flag register checking
```
if not zero {
    b = 23
}

ifr carry {
    a++
}

// RGBDS equivalent
    jp z, :+
    ld b, 23
:   jr nc, :+
    inc a
:
```
Else and Else-If are also possible
```
if carry {
    b = 23
} else if zero {
    b = 56
} else {
    b = 0
}

// RGBDS equivalent
    jp nc, .ifElse0
    ld b, 23
    jp .endIf
.ifElse0:
    jp nz, .else
    ld b, 56
    jp .endIf
.else:
    ld b, 0
.endIf:
```
*Note: The RGBDS code is just a behavioral equivalent. The if statements will not pollute the namespace with labels. You can nest if statements with no problem*

Possible conditional codes:
- zero
- not zero
- carry
- not carry

## Comparison checking
You can compare the A register with a comparison operator and a literal/register.
```
if a > 3 {
    b = 23
} else a != c {
    b = 56
} else a <= 64 {
    b = d
} else {
    b = 0
}

// RGBDS equivalent
    cp 3
    jp nc, .ifElse0
    jp z, .ifElse0
    ld b, 23
    jp .endIf
.ifElse0:
    cp c
    jp z, .ifElse1
    ld b, 56
    jp .endIf
.ifElse1:
    cp c
    jp nc, .else
    jp nz, .else
    ld b, d
    jp .endIf
.else:
    ld b, 0
.endIf:
```
Possible conditions, where X is a literal or register:
- a == X
- a != X
- a > X
- a < X
- a >= X
- a <= X

You cannot mix a flag if statement with a comparison else if, and vice versa. You can however mix if and ifr.

## Flag if statement EBNF Specs
```
if_statement = if_head, {else_if}, (else | if_tail);

if_head = ws, if_type, flag_cond, scope;

else_if = ws, "else", if_head ;

else = ws, "else", scope ;

if_tail = ws, "}", ws, [comment], EOL ;

flag_cond = ws, ("zero" | "not zero" | "carry" | "not carry"), ws ;

scope = ws, "{", ws, [comment], EOL, code, ws, "}" ;

if_type = "if" | "ifr" ;

```

## Comparison if statement EBNF Specs
```
if_statement = if_head, {else_if}, (else | if_tail);

if_head = ws, if_type, comp_cond, scope;

else_if = ws, "else", if_head ;

else = ws, "else", scope ;

if_tail = ws, "}", ws, [comment], EOL ;

comp_cond = ws, "a", operator, (literal | register),  ws ;

operator = ws, "==", "!=", ">", "<", ">=", "<=", ws ; 

scope = ws, "{", ws, [comment], EOL, code, ws, "}" ;

if_type = "if" | "ifr" ;
```