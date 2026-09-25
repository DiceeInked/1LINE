# 1(LINE)

**1(LINE)** is a deliberately simple, function-based programming language designed to be easy to learn and memorize.

## General Rules

- The language is heavily function-based.
- Spaces, tabs, and line breaks are completely ignored by the language. They are only for organization and readability.
- `/TEXT/` can be used for comments/notes.
- Parentheses with no function defining them are automatically treated as values (`val`).
- Every executable piece of code must be contained inside a code block.
- Source-code order does not determine logical execution order when block order numbers are used.

## Code Blocks

### `flag`

```
flag()[CODE]
```

`flag` is a normal code block that runs the codes.

Example:

```
(5)flag()[CODE]
```

### `reap`

```
reap()[CODE]
```

With no tick rate, `reap` runs once per rendered screen frame.

A specified rate runs independently of the display's rendering frame rate:

```
reap(60)[CODE]
reap(30)[CODE]
reap(120)[CODE]
```


### `func`

```
func((NAME)(PARAMETERS))[CODE]
```

Creates a function.

Example:

```
func((add)(a)(b))[
    return(cal(num(fun(a))+num(fun(b))))
]
```

## Block Order

Every block may have an order number:

```
(NUMBER)flag()[CODE]
(NUMBER)reap()[CODE]
(NUMBER)func(...)[CODE]
```

Rules:

- `0` and any number greater than `0` are valid.
- If no number is given, it defaults to `0`.
- Lower numbers execute before higher numbers.
- Blocks with the same number are logically simultaneous. The implementation may process them sequentially, but source-processing order must not change the language's behavior.
- The order number applies equally to `flag`, `reap`, and `func`.
- Using a function or variable before it exists according to execution order produces an error.

## Variables

```
glo(val(NAME)val(VALUE))
loc(val(NAME)val(VALUE))
set(val(NAME)val(VALUE))
```

- `glo` creates a global variable.
- `loc` creates a local variable.
- `set` changes an existing variable's value.

Variable rules:

- Referencing a nonexistent variable is an error.
- Using a variable before it has been created is an error.
- Creating a variable with a name that is already taken is an error.

## Values

```
val(ANYTHING)
var(VARIABLE)
fun(PARAMETER)
boo(TRUE)
boo(FALSE)
nul()
```

- `val` represents a value.
- `var` accesses a regular variable.
- `fun` accesses a function parameter.
- `boo` creates a boolean.
- `nul` represents null/no value.

## Text

```
txt(TEXT)
```

## Numbers

```
num(NUMBER)
int(5)
flo(5.5)
```

- `num` is a generic number type.
- `int` is an integer.
- `flo` is a float.

## Math

```
cal(...)
```

Operators:

- `+` addition
- `-` subtraction
- `*` multiplication
- `:` division
- `^` exponentiation

Examples:

```
cal(num(5)+num(3))
cal(num(10)-num(4))
cal(num(5)*num(2))
cal(num(10):num(2))
cal(num(2)^num(3))
```

Numeric results follow normal type promotion:

- `int + int` → `int`
- `int + flo` → `flo`
- `flo + flo` → `flo`
- `num + num` → `num`

Text inside `cal` is invalid.

## Comparisons

`com` returns a boolean.

```
com(val(ANYTHING)==val(ANYTHING))
com(val(ANYTHING)!=val(ANYTHING))
com(val(ANYTHING)>=val(ANYTHING))
com(val(ANYTHING)<=val(ANYTHING))
com(val(ANYTHING)>val(ANYTHING))
com(val(ANYTHING)<val(ANYTHING))
```

## Boolean Logic

```
and(boo(BOOL)boo(BOOL))
ore(boo(BOOL)boo(BOOL))
not(boo(BOOL))
```

- `and` is true when both values are true.
- `ore` is true when at least one value is true.
- `not` reverses a boolean.

## IF / ELSE

```
if(boo(BOOL)do(CODE))
if(boo(BOOL)do(CODE)EL(CODE))
```

`if` is a normal function, not a block. `EL` can be placed directly after `do`.

Example:

```
if(com(var(score)>=int(10))do(SAY(txt(Passed)))EL(SAY(txt(Failed))))
```

## Functions

Define:

```
func((NAME)(PARAMETERS))[CODE]
```

Call:

```
func((NAME)(ARGUMENTS))
```

Example:

```
func((add)(3)(5))
```

Typed form:

```
func(txt(add)int(3)int(5))
```

Access parameters with:

```
fun(NAME)
```

Function rules:

- Duplicate parameter names are an error.
- A parameter name cannot match an existing variable name.
- Too few arguments are an error. The function does not run.
- Too many arguments are an error. The function does not run.
- Calling a function before it exists according to execution order is an error.
- Creating a function with a name already used by another function is an error.

## Return

Return one value:

```
return(VALUE)
```

Multiple values:

```
return((1)(2))
return((1)(2)(3))
```

Each parenthesized item is a separate returned value.

Multiple returned values are represented as a list. List creation and access syntax has not been finalized yet.

## Output

The current core language is console-based.

```
SAY(VALUE)
```

Example:

```
SAY(txt(Hello world!))
```

## Packages

The core language is intentionally minimal. Future packages will add functionality beyond the core.

A future example package is a `basic` package.

The core language is intended to provide the fundamental building blocks: variables, values, functions, parameters, returns, conditions, boolean logic, math, and console output.

## Errors

Confirmed error cases include:

- Referencing a nonexistent variable.
- Using a variable before it has been created.
- Creating a duplicate variable.
- Creating a duplicate function.
- Calling a function before it exists according to execution order.
- Passing the wrong number of function arguments.
- Using an invalid type in an operation, such as text inside `cal`.

The complete error system will be designed separately.

## Current Scope

1(LINE) is currently a minimal core language and is not yet intended to provide full application-building functionality by itself.

The language is currently centered around defining functions, running them, manipulating values, making decisions, performing calculations, and producing console output.

Additional functionality is planned through packages.
