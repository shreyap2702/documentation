# Autosend Python SDK

This SDK provides a simple Python SDK for the AutoSend Email API.
It removes the need to manually build HTTP requests, manage payloads, or handle API endpoints.

If you want to send transactional emails, bulk messages, or manage contacts from Python, this SDK provides a clean and consistent way to do it.

You can see this simple example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

response = client.send_email(
    to="user@example.com",
    template_id="welcome-template",
    data={"name": "John"}
)

print(response)
```

The package is published on PyPI: https://pypi.org/project/autosend-shreya-sdk  
Install with `pip install autosend-shreya-sdk`

<Note>Note: This is an unofficial package and is not an official Autosend release.</Note>

