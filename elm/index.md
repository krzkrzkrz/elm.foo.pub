# Elm Journey

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
True ❷
> pi /= pi
False ❹
> not (pi == pi)
False
> pi <= 0 || pi >= 10
False
> 3 < pi && pi < 4
True
```







