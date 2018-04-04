# Elm Journey

[Elm](https://guide.elm-lang.org) is a functional language that compiles to JavaScript.

## Elm REPL

To start Elm REPL, type `elm-repl` in a terminal

```elm
-- Creating a function with multiple lines
-- Use \
-- And |, but dont forget to tab (2 spaces)

> pluralize singular plural count = \
|   if count == 1 then singular else plural
<function>
> pluralize "elf" "elves" 3
"elves"
> pluralize "elf" "elves" (round 0.9)
"elf"
```

## Comments

```elm
-- Inline comments:
-- Inline comment here
```

```elm
-- Block comments:
{-
  Block comment here
-}
```

## String concatenation

```elm
"Hello, " ++ "World!"
```

## Strings and characters

```elm
-- This is a string with length of 1
"a"

-- This is a string with length of 3
"abc"

-- This is a single character
'a'

-- An empty string
""

-- Error: Must contain 1 character
'abc'

-- Error: Must contain 1 character
''
```

## Boolean & conditions

* You write `True` and `False` instead of `true` and `false`
* You write `/=` instead of `!==`
* To negate values, you use `not`

```elm
> pi == pi
True
> pi /= pi
False
> not (pi == pi)
False
> pi <= 0 || pi >= 10
False
> 3 < pi && pi < 4
True
```

## Conditions

```elm
-- Ternary condition:
if 1 == 1 then "Yes" else "No"

-- Condition blocks
if foo == 1 then
  "One"
else if foo == 2 then
  "Two"
else
  "Three"
```

## Functions

```elm
-- Parameters are before the =
-- There is no return, since a function body is a single expression
-- And since an expression evaluates to a single value, Elm uses that value as the function's return value

> isOdd num = num % 2 == 1
<function>
> isOdd 5
True
> (isOdd 5)
True
> isOdd (5 + 1)
False
```

## Scopes

`let` espressions can be used to scope declarations

The scope of `dash` and `isKeepable` are contained within `let`, and are not accessible globally

```elm
-- Scoped declaration
-- dash and isKeepable are scoped insided withoutDashes

> withoutDashes str = \
|   let \
|     dash = \
|       '-' \
|     isKeepable character = \
|       character /= dash \
|   in \
|     String.filter isKeepable str

-- Global declaration
-- dash and isKeepable are globally accessible

> dash = '-'
> isKeepable character = character /= dash
> withoutDashes str = String.filter isKeepable str
```

## Anonymous functions

* Functions that dont need a name
* They begin with a `\`
* The parameters are followed by a `->`, instead of a `=`

```elm
-- Named function
> area w h = w * h

-- Anonymous function
> \w h -> w * h

-- Another example
> import Char
> String.filter (\char -> Char.isDigit char) "(800) 555-1234"
"8005551234"

-- Refactored version of above
> String.filter Char.isDigit "(800) 555-1234"
"8005551234"
```

## Operators

```elm
-- Inflix style
7 - 4 == 4

-- Prefix style
(-) 4 3 == 4

-- Some examples:
> divideBy = (/)
<function>
> 7 / 2
3.5
> (/) 7 2
3.5
> divideBy 7 2
3.5

-- Operator precedence
> (==) ((+) 3 4) ((-) 8 1)
True : Bool
```

## List

* You can ask for its first element
* You can ask for its length
* You can iterate over its elements
* It is immutable
* If you need to ask for elements at various different positions, you can first convert from an Elm List to an Elm Array
* Can be combined with another list via `++` operator
* All elements must have a consistent type
* Lists are used far more often (than arrays) because they have better performance characteristics in typical Elm use cases

```elm
[ "one fish", "two fish" ]
```


```elm
```







