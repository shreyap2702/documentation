# Client Configuration

The `AutosendClient` is the main entry point for using the Autosend Python SDK.  
You must initialize it with your API key before calling any functions.

## Initialize the client

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")
```

The `api_key` is required.
You can find your key in the AutoSend dashboard:

```
https://autosend.com/settings/api-key
```

# Client configuration

The `AutosendClient` is the primary entry point for the Autosend Python SDK. Initialize a single client instance and reuse it across your application.

## Quick initialization

```python
from autosend import AutosendClient
import os

# Read API key from environment (recommended)
client = AutosendClient(api_key=os.getenv("AUTOSEND_API_KEY"))
```

The `api_key` argument is required. You can obtain your API key from the AutoSend dashboard.

## Configuration options

The client supports a few common options when constructing the instance.

- api_key (str, required): Your AutoSend API key.

Example with optional settings:

```python
client = AutosendClient(
    api_key="YOUR_KEY"
)
```

## What the client does for you

- Attaches the API key and required headers to each request
- Formats and validates request payloads
- Sends requests (single and bulk email endpoints)
- Manages contact operations (create, update/upsert, search, remove)
- Wraps API errors into Python exceptions for easier handling

## Best practices

- Store your API key in an environment variable (do not hard-code it).
- Reuse a single `AutosendClient` instance rather than re-creating it per request.
- Catch and handle client exceptions where appropriate (network errors, validation errors, API errors).

## Example: send a single email

```python
client = AutosendClient(api_key="YOUR_KEY")

response = client.send_email(
    to="user@example.com",
    template_id="welcome-template",
    data={"name": "Jane"}
)

print(response)
```