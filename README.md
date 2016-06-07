# Debug Context Manager

Super simple context manager to wrap a block of code with a debug message that
display a custom text before the block of code starts then display "done" or a
custom string once the block of code is finished.

This is a nicier way than using a `print` before and a `print` after the code
(and prints everything on the same line).

It also logically group lines of code in a log procedure in meaninful sections.

# Usage

```python
from debug_context_manager import debug

with debug("Doing this stuff"):
    # some code
```

Will result in displaying:

    Doing this stuff ... <here waits for code to run>done

```python
with debug("Doing other stuff", "and finished!"):
    # other code
```

Will result in displaying:

    Doing other stuff ... <here waits for code to run>and finished
