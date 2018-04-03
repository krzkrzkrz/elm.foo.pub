# Elm Journey

Elm is a functional language that compiles to JavaScript.

[Elm](https://guide.elm-lang.org)

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




```elm
```







