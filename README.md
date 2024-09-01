# Lusid

If you have the following:

* Macbook
* Python

You can programatically control iMessage, here's how

## Quickstart

Start here if you're just interested in sending a message

1. Install the dependency

```bash
$ pip install lusid
```

2. Import the `send_message` function and voila

```python
from lusid import send_message

to = "123-456-7890"
body = "Yeehaw"
send_message(to, body)
```

## Basic example

Start here if you're interested in something interacting with received messages

1. Install the dependency

```bash
$ pip install lusid
```

2. Create a "client" to repeatedly read your inbox (the rest of this quickstart assumes you're writing to a file named `app.py` but feel free to replace that later on with whatever you named your to)

```python
# app.py

from lusid import create_simple_message_client

def start_client():
  create_simple_message_client(
    message_handler=lambda to, body: None
  )

if __name__ == "__main__":
  start_client()
```

3. Define a function for handling messages:

```python
# Snippet

def handle_message(from, body):
  print(f"Handling the message [{body}] from [{from}]")
  return "Some funny autoreply here" # Or None to not reply at all
```

3. Next we're going to include the function we defined earlier

```diff
# app.py

from lusid import create_simple_message_client

+def handle_message(from, body):
+  print(f"Handling the message [{body}] from [{from}]")
+  return "Some funny autoreply here" # Or None to not reply at all

def start_client():
  create_simple_message_client(
    message_handler=lambda to, body: None
  )

if __name__ == "__main__":
  start_client()
```

Then actually use it as our message handler

```diff
# app.py

from lusid import create_simple_message_client

def handle_message(from, body):
  print(f"Handling the message [{body}] from [{from}]")
  return "Some funny autoreply here" # Or None to not reply at all

def start_client():
  create_simple_message_client(
-    message_handler=lambda to, body: None
+    message_handler=handle_message
  )

if __name__ == "__main__":
  start_client()
```

4. Now your script is set up to automatically reply to every received message with "Some funny autoreply here"

```bash
$ python app.py
Some terminal output indicating it's running...
```

## Complex example

Suppose you wanted to be able to inform a friend as to whether or not it's Thursday while also having message interaction, here's how you can accomplish that
