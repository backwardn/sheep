# Coding guidelines

Bash scripiting is very permissive, this guide is here to describe rules to follow by everyone
during development. Some rules are here to prevent potential errors while some others are here
to ensure code style consistency.

Every single contribution has to follow these rules in order to be accepted.

## Variables

### Variable reference

In code, a variable reference is done using the `${}` notation. For example, we write `${myVariable}` instead of `$myVariable`.

### Variable into functions

Everytime it is possible, a variable is declared locally when used inside a function using the `local` keyword. We try to avoid global variable as much as we can.

### Variable namming

Some rules to follow:

- Variable representing script input parameters (consider like constants) are in *screaming snake case* (e.g. `MY_VARIABLE`)
- Other variables and function name are in *snake case* (e.g. `my_function`)

## Functions

### Function documentation

Function documentation is optionnal but strongly encouraged and should be present every time when we
think it is necessary. A function documentation is located immediately before the function declaration
and respects the following format.

```
#
# This function is useful for *** ***
# *** *** *** *** **.
#
# $1 - Input parameter 1 description
# $2 - Input parameter 2 description
# ...
# $n - Input parameter n description
#
```

## Control structures

Control structures like `if`, `for` and `while` are written avoiding using extra new lines before
keywords `then` or `do`. We use semicolon instead.

For instance, we write

```
if [ condition1 ]; then
	cmd1
elif [ condition2 ]; then
	cmd2
else
	cmd3
fi
```

instead of

```
if [ condition1 ]
then
    cmd1
elif [ condition2 ]
then
    cmd2
else
    cmd3
fi
```

## Conditions

### Prefer `test` single bracket

We prefer to uniforme `test` syntax using always single bracket `[` `]`.
We write `[ condition1 ] || [ condition2 ]` instead of `[[ condition1 || condition2 ]] `.

### Prefer `test` flags

Every time it is possible we prefer to use dash flags from the `test` command rather than merely compare using `=` operator. e.g. we write `[ -z "${my_var}" ]` instead of `[ "${my_var}" = "" ]`. And we write
`[ ${my_var} -ne 0 ]` instead of `[ ${my_var} != 0 ]`.

## Code indentation

Indentation is done using `Tab`.

## Misc

### Output capture

To capture command output in a variable we use the `$()` notation. We write `foo="$(bar)"` instead of `foo="``bar``"`.

## Testing

### About unit test

Code must be structured in a way that we are able to write unit tests for functions every time we
think it is necessary.

### About integration test

CI works using sheep configuration files contained in `sheep/tests/integration_test` repository.
These files are named following this model : `distribution_bootMode_CIEouCID_hardware.yml`.

* `hardware` is the type of server targeted by this configuration.
* `distribution` is always written this way : `centOS7`, `openSUSE15_1`, `debian9` and `ubuntu16_04`.
