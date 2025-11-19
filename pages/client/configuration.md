# Client Configuration

The `AutosendClient` is the main entry point for using the Autosend Python SDK.  
You must initialize it with your API key before calling any functions.

## Initialize the client

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")
````

The `api_key` is required.
You can find your key in the AutoSend dashboard:

```
https://autosend.com/settings/api-key

## Optional Parameters

The client supports a few optional arguments.

### `base_url`

Use this only if you are testing against a custom or staging server.

```python
client = AutosendClient(
    api_key="YOUR_KEY",
    base_url="https://api.autosend.com"
)
```

Default is the official Autosend API URL.

### `timeout`

Set a custom request timeout (in seconds):

```python
client = AutosendClient(
    api_key="YOUR_KEY",
    timeout=10
)
```

Default: `30` seconds.

---

## What the client handles

* attaches the API key to every request
* validates your inputs
* formats JSON payloads
* wraps API errors into simple Python exceptions

---

## Example: basic usage

```python
client = AutosendClient(api_key="YOUR_KEY")

response = client.send_email(
    to="test@example.com",
    template_id="welcome",
    data={"name": "User"}
)
```

---

This is all you need to configure the client before using the email or contact modules.

```