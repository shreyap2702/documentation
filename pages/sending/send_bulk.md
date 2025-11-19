# `send_bulk()`

Send the same email to multiple recipients in a single request using the `POST/mails/bulk` endpoint.

## What this function does

`send_bulk()` sends **one email template/content** to multiple recipients (up to 100).  
It supports:

- personalized HTML content  
- dynamic template variables  
- reply-to address  
- unsubscribe URL & unsubscribe groups  

All recipients receive the same email template, with dynamic data applied to each one.

## Arguments

**recipients**
List of recipient dictionaries, each containing:

* `email` — recipient email
* `name` — recipient name
  Minimum: 1
  Maximum: 100

**`from_email`**
Sender’s email address.

**`from_name`**
Sender’s display name.

**`subject`**
Subject line of the email.

**`html`**
HTML body of the email.
Supports dynamic placeholders like `{{name}}`.

**`dynamic_data`**
Dictionary of template variables for personalization.

**`reply_to_email`** *(optional)*
Email replies should go to this address.

**`unsubscribe_url`** *(optional)*
RFC 2369 compliant unsubscribe link.

**`unsubscribe_group_id`** *(optional)*
Category/group ID for marketing email preference management.

---

## Errors

### ValidationError
Raised when:

* recipients list is empty
* more than 100 recipients
* a recipient is missing `email` or `name`
* dynamic data fails validation
* unsubscribe URL is invalid

### APIError
Raised when AutoSend returns a 4xx or 5xx error.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

recipients = [
    {"email": "user1@example.com", "name": "Alice"},
    {"email": "user2@example.com", "name": "Bob"},
]

client.sending.send_bulk(
    recipients=recipients,
    from_email="noreply@company.com",
    from_name="Company",
    subject="Product Update",
    html="<p>Hello {{name}}</p>",
    dynamic_data={"name": "User"}
)
```