# Constants
Constants are the bedrock of Gaba. They are used as comptime values that can be invoked to structure your whole project.


### Constant Types

```
// int
Integer :: 12

// float
PI :: 3.1415

// string
Greeting :: "Hello"
City :: "England" with my_charmap

// Enum
Fruit :: enum {
    Apple
    Orange
    Banada
    PassionFruit
}

// Struct
Coin :: struct {
    normal_value: u8
    multiplier_value: u8
}

// Func
sqrt :: func(x) {
    x * x
}

```
