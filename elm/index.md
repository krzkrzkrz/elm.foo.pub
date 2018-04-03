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



```elm
```







