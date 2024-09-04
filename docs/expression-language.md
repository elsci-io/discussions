Expression Language
----

When creating Table visualizations you can add columns with custom expressions - you can do math, logical, string expressions. Every time you reference one of the columns you need to put its name into `col["col name"]`.

# Common usages

## Calculate a conversion

Conversion as a ratio of reaction Product to the Limiting Reactant:

```
col["Product area"] / (col["Product area"] + col["Reactant area"])
```

Note, column names in quotes are just examples, you need to put your own column names.

## Compare two quantities

Suppose you compare areas of two peaks, and you want to put "true" into the column if PeakA is bigger and "false" otherwise:

```
col["PeakA area"] > (col["PeakB area"]
```

# Language Specification

## Arithmetic

| Example      |  Result |
|--------------|--------:|
| 2 + 3        |       5 |
| 2 - 3        |      -1 |
| 2 * 3        |       6 |
| 2 / 3        | 0.666.. |
| 2 + (10 / 2) |       7 |

## Logical

| Example                | Result |                                               Explanation |
|------------------------|-------:|----------------------------------------------------------:|
| 2 > 3                  |  false |                                                           |
| 2 < 3                  |   true |                                                           |
| 2 >= 3                 |  false |                                                           |
| 2 <= 3                 |   true |                                                           |
| 3 == 3                 |   true |                                          `==` means equal |
| 3 != 3                 |  false |                                      `!=` means not equal |
| ~"blank-01" ==* "blank"~|  true |                                 Deprecated, use ~ instead |
| "blank-01" ~ "blank"   |   true | Checks if string contains another string. Case-sensitive. |
| "a" == "a" && 3 < 10   |   true |                                            `&&` means AND |
| "a" == "b" \|\| 3 < 10 |  true  |                                           `\|\|` means OR |
| "a" in ["a", "b"]      |   true |       `in` checks if any element in array matches the key |

## Conditional logic

The ternary operator allows the result to depend on the condition and whether it evaluates to `true` or `false`:

```
true or false ? "if true" : "if false"
```

Example:

| Example                               |      Result |                     Explanation |
|---------------------------------------|------------:|--------------------------------:|
| 2 > 3 ? "2 is bigger" : "3 is bigger" | 3 is bigger |                                 |
| "" ? "It is empty" : "Not empty"      | It is empty | Empty string is same as `false` |
