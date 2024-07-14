
| Name              | Operators                                    | Associativity        | Binding    |
| ----------------- | -------------------------------------------- | -------------------- | ---------- |
| Parenthesized     | (...)                                        |                      |            |
| Primary           | a(), a[], a.b                                | Left-to-right        |            |
| Unary             | -a, !a, ~a, *a, &a                           | Right-to-left        | All above  |
| Multiplicative    | a * b, a / b, a % b                          | Left-to-right        | All above  |
| Additive          | a + b, a - b                                 | Left-to-right        | All above  |
| Shift             | a << b, a >> b                               | Requires parentheses | Unary      |
| Relational        | a < b, a > b, a <= b, a >= b, a == b, a != b | Requires parentheses | All above  |
| Binary AND        | a & b                                        | Left-to-right        | Unary      |
| Binary XOR        | a ^ b                                        | Left-to-right        | Unary      |
| Binary OR         | a \| b                                       | Left-to-right        | Unary      |
| Short-circuit AND | a && b                                       | Left-to-right        | Relational |
| Short-circuit OR  | a \| b                                       | Left-to-right        | Relational |