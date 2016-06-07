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

And:

```python
with debug("Doing other stuff", "and finished!"):
    # other code
```

Will result in displaying:

    Doing other stuff ... <here waits for code to run>and finished

# Example

Out of context example showing how this logically put into meaninful sections a procedure:

```python
with debug("Login"):
    response = s.post("https://example.com/api/user/login", data=json.dumps({"user": "cortex@worlddomination.be", "password": "baddrym"}))
    assert response.status_code == 200, response.content

session_data = response.json()

with debug("Get client data"):
    response = s.get('https://example.com/api/client/all?compose=true&user=%s' % session_data["user"], headers={"Session": session_data["token"]})
    assert response.status_code == 200, response.content

client = response.json()[0]

with debug("Get user cert id"):
    response = s.get("https://example.com/api/client/%s/cert/all?active=true" % client["id"], headers={"Session": session_data["token"]})
    assert response.status_code == 200, response.content

cert = response.json()[0]
```
