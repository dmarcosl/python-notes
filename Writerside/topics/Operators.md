# Operators

## Arithmetic Operators

| Operator | Name           | Description                                     | Example       |
|----------|----------------|-------------------------------------------------|---------------|
| `+`      | Addition       | Sum or concatenate values                       | `1 + 2 = 3`   |
| `-`      | Subtraction    | Subtract right to left                          | `5 - 1 = 4`   |
| `*`      | Multiplication | Multiplies values                               | `2 * 6 = 12`  |
| `/`      | Division       | Divide left by right                            | `16 / 2 = 8`  |
| `%`      | Modulus        | Divide left by right and returns remainder      | `17 % 2 = 1`  |
| `**`     | Exponent       | Exponencial calculation (power)                 | `2**8 = 256`  |
| `//`     | Floor Division | Divide left by right rounding to the lowest int | `17 // 5 = 3` |

## Comparison Operators

| Operator | Name                    | Description                                              | Example         |
|----------|-------------------------|----------------------------------------------------------|-----------------|
| `==`     | Equals                  | If the values are equals                                 | `2 == 2`, True  |
| `!=`     | Not equals              | If the values are not equals                             | `1 != 6`, True  |
| `>`      | Greather than           | If the first value is greather than the second           | `6 > 3`, True   |
| `<`      | Less than               | If the first value is less than the second               | `7 < 3`, False  |
| `>=`     | Greather than or equals | If the first value is greather than or equals the second | `4 >= 4`, True  |
| `<=`     | Less than or equals     | If the first value is less than or equals the second     | `3 >= 2`, False |

## Assignment Operators

| Operator | Name                      | Description                                                | Example       |
|----------|---------------------------|------------------------------------------------------------|---------------|
| `=`      | Assign                    | Assign the value                                           | `a = 6`, 6    |
| `+=`     | Add and assign            | Sum and assign the value                                   | `a += 3`, 9   |
| `-=`     | Subtract and assign       | Subtract right to left and assign the value                | `a -= 3`, 6   |
| `*=`     | Multiply and assign       | Multiply and assign the value                              | `a *= 4`, 24  |
| `/=`     | Divide and assign         | Divide left by right and assign the value                  | `a /= 3`, 8   |
| `%=`     | Modulus and assign        | Divide left by right and assign assign the ramainder       | `a %= 3`, 2   |
| `**=`    | Exponent and assign       | Assign the exponential calculation                         | `a **= 4`, 16 |
| `//=`    | Floor division and assign | Divide left by right and assign rounding to the lowest int | `a //= 5`, 3  |

## Logical Operators

| Operator | Name        | Description               | Example                 |
|----------|-------------|---------------------------|-------------------------|
| `and`    | Logical AND | If both are True          | `3 < 5 and 5 > 4`, True |
| `or`     | Logical OR  | If any of both is True    | `1 > 5 or 3 < 4`, True  |
| `nor`    | Logical NOT | Reverse the logical state | `not 1 > 2`, True       |

## Membership Operators

| Operator | Description                         | Example                                       |
|----------|-------------------------------------|-----------------------------------------------|
| `in`     | If the value is in the variable     | `'bird' in 'the bird is yellow'`, True        |
| `not in` | If the value is not in the variable | `'two' not in ['one', 'two', 'three']`, False |

## Identity Operators

| Operator | Description                                   |
|----------|-----------------------------------------------|
| `is`     | If the variables point to the same object     |
| `is not` | If the variables not point to the same object |
