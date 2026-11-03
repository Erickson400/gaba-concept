# Functions
There are built in math functions which you can use to define constants.
- math.round(x)
- math.cell(x)
- math.floor(x)
- math.sin(x)
- math.cos(x)
- math.tan(x)
- math.asin(x)
- math.acos(x)
- math.atan(x)
- math.atan2(x, y)

You can also define your own functions using the basic math functions as building blocks. They're isolated pure functions, meaning you can't reference constants, only what you pass as arguments.

```
sqrt :: func(x) {
    x * x
}

AREA :: sqrt(75)
```
All constants and arguments in Gaba are Float64s. They'll be automatically rounded to the nearest integer when you use them as a n16 or n8 literal, when indexing an array, or any other place where an integer is required.


