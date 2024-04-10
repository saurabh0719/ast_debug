# ast_debug

Just an experiment for lazy debugging.

**Do not use** in production or other critical environments, the code relies on modifying the AST for debugging. 

```sh
$ pip install ast_debug
```

#### Example 

```python

import ast_debug

@ast_debug.trace(['a', 'b'])
def do_something(a=5, b=6):
    a = a + b
    c = a
    a = "Experimenting with the AST"
    b = c + b
    a = c + b
    return a

do_something(1, 2)

```

Output -

```
executing: do_something(a = 1, b = 2)
debug: do_something: a = 3
debug: do_something: a = Experimenting with the AST
debug: do_something: b = 5
debug: do_something: a = 8
```

#### trace

The `trace` function is the decorator to add prints to the AST.

```python
def trace(
    variables=None,
    args=True,
    result=False,
    max_len=None,
    verbose=False,
    use_spaces=False
):
    """
    An experimental decorator for tracing function execution using AST.

    Args:
        variables (list, optional): Variables to trace. Traces all if None. Default is None.
        args (bool, optional): Whether to print function arguments. Default is True.
        result (bool, optional): Whether to print function return value. Default is False.
        max_len (int, optional): Max length of printed values. Truncates if exceeded. Default is None.
        verbose (bool, optional): Whether to print detailed trace info. Default is False.
        use_spaces (bool, optional): Whether to add empty lines for readability. Default is False.

    Returns:
        function: Decorator for function tracing.
    """
```
<hr>