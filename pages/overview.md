## About the SDK

The Autosend Python SDK is a lightweight wrapper around the AutoSend Email API.

AutoSend is an email platform for developers and marketers to send and track transactional and marketing emails.
With this SDK, you do not need to write raw HTTP requests or JSON payloads.
All you need is your API key.

The SDK handles the following key tasks:

* Request formatting
* Validation
* Error handling
* Sending emails (transactional and bulk)
* Managing contacts

The goal is to help developers integrate AutoSend quickly in any Python application.

---

## Installation

You can install the SDK from PyPI or directly from GitHub.

### Install from PyPI

```bash
pip install autosend-shreya-sdk
````

### Import the Client

```python
from autosend import AutosendClient
```

### Install from GitHub (Alternative)

```bash
pip install git+https://github.com/shreyap2702/autosend-python-sdk.git
```

-----

## Quickstart Examples

### Initialize the Client

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")
```

-----

### Send a Single Email

```python
response = client.send_email(
    to="user@example.com",
    template_id="welcome-template",
    data={"name": "John"}
)

print(response)
```

The SDK handles:

  * Payload structure
  * POST request
  * API URL selection
  * Error wrapping

-----

### Send Bulk Emails

```python
response = client.send_bulk(
    recipients=[
        {"email": "a@example.com", "data": {"name": "A"}},
        {"email": "b@example.com", "data": {"name": "B"}},
    ],
    template_id="update-template"
)

print(response)
```

-----

### Create Contact 

```python
client.create_contact(
    email="john.doe@example.com",
    first_name="John",
    last_name="Doe"
)
```
