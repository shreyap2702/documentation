# send_email

Send a single transactional or marketing email through the `/mails/send` endpoint.

## What this function does

`send_email()` sends **one email** to a single recipient.  
It supports both transactional and marketing use cases, including:

- HTML content
- dynamic template variables
- attachments
- reply-to address
- unsubscribe URL or unsubscribe group ID

The SDK handles validation, payload structure, and the final POST request.

## Arguments

**to_email**
Recipient’s email address.

**to_name**
Recipient’s display name.

**from_email**
Sender’s email address.

**from_name**
Sender’s display name.

**subject**
Subject line of the email.

**html**
HTML content of the email.

**dynamic_data**
Dictionary of template variables used inside HTML or templates.

**reply_to_email** *(optional)*
Custom reply-to address.

**attachments** *(optional)*
A list of attachments following the Autosend API format.

**unsubscribe_url** *(optional)*
RFC 2369 compliant unsubscribe URL.

**unsubscribe_group_id** *(optional)*
Unsubscribe group/category ID for grouped marketing preferences.

---

## Errors

**ValidationError**
Raised when:

* attachments exceed limits
* blocked extensions are detected
* dynamic data validation fails
* unsubscribe URL is invalid

**APIError**
Raised when the AutoSend API returns an error (4xx or 5xx).

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.sending.send_email(
    to_email="user@example.com",
    to_name="John Doe",
    from_email="noreply@company.com",
    from_name="Company",
    subject="Welcome!",
    html="<h1>Hello {{name}}</h1>",
    dynamic_data={"name": "John"}
)
```