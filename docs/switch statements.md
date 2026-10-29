# Switch statements
Switch statements are an alternative to If statements. They create a lookup table for conditional jumps, this makes them extremely fast at the expense of ROM space. It is recommended to use them when checking equality over tens or hundreds of cases.
```
switch a {
case 0:
    b = 0
    break           // Break out of the switch statement.
    d = 86
case 1:
    b = 1
case 2, 3, 4, 5:    // Creates multiples cases that point to the same code.
    b = 0xFF
case 11:            // Out of order cases
    b = 24
    fallthrough     // Execution will fall to case 7.
case 7:
    b = 75
default:
}
```
Switches work on the A register only. Cases automatically break out of the switch when they finish unlike C, unless the *fallthrough* keyword is placed at the end of the case. You can have up to 127 cases, excluding default since it's always present even if omitted. 

## How it works
The compiler placed each case section into ROM with a jump instruction at the end of each case pointing to the end of the switch. They're ordered in the same way you wrote them. A lookup table is then created with it's size being the (biggest_case - smallest_case), in the example above it would be 12 cases. Any case not specified between this range will be pointing to default (6, 8, 9, 10 in this example). The lookup table will hold pointers to the beginning of each case. Before the cases are allocated, a jp instruction will jump to our next location and skips all the data. This location checks if a is within it's case range, if not then it jumps to default (or leaves the switch if no default), if it is in range then it indexes the lookup table and jumps to it's corresponding case. Omitting Default creates a default case that has a jump to the end of the switch. 
- Check that A is within range, if not then exit the switch
- Set HL to the lookup table
- Add the minimum case offset to A
- Shift A left by one
- Add A to HL using carry
- Dereference HL
- Jump to HL

## Caveats
Other than the A register, switches also use the HL register. Store the HL register on the stack before the statement if you want to preserve it. HL is only used when jumping into a case, you can modify it inside a case and it will keep that value even after the switch.






