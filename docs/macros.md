# Macros
User defined macros are not supported. Instead there are built-in macros for facilitating repetitive operations.
```
macro_name!(param1, param2, param3, ...etc)
```

## Parameter types
#### int
A signed 64-bit literal/constant. Or any 16-bit constant like a label, procedure, or ROM address.

#### float
A 64-bit floating point number.

#### bool
true or false

### reg8
An 8-bit register

### reg16
A 16-bit register

#### struct
A constant with a Struct definition. e.g "MyStruct :: struct {...}".

#### enum
A constant with an Enum definition. e.g "MyEnum :: enum {...}".

#### string
A constant (Name :: "Eric"), or a literal string ("Hello")

### Optional and Variadtic Parameters
```
// Macro signature:
// do_thing!(string, struct, bool = false, ..integer)

// Invokations:
do_thing!("Big Mac", MyStruct)
do_thing!("Macron", MyStruct, true, 3, 453, 23, 564, 34)
```

Optional parameters can be omitted to keep their default values. They are always between required params and variadic params in the invokation.

Variadic parameters can have any numbers of arguments. There can only be one variadic parameter, and it must be the last in the invokation. They can be omitted too.

## Macro list

Enable ROM bank

enable ram bank

HDMA transfer



