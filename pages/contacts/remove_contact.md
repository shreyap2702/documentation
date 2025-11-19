# `remove_contacts()`

Remove one or more contacts using the `/contacts/remove` endpoint.  
This method deletes contacts from AutoSend based on their email addresses.

---
## What this function does

`remove_contacts()` accepts a list of email addresses and removes the corresponding contacts from the AutoSend database.  
The method validates that at least one email is provided and ensures each email follows a valid format before making the API request.

## Arguments

**`emails`**
A list containing one or more email addresses.
Each email must be valid.
At least one email is required.

---

## Errors

### ValidationError
Raised when the list is empty or when any email address is invalid.

### APIError
Raised when the AutoSend API cannot process the delete request.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.contacts.remove_contacts([
    "user@example.com",
    "contact@test.com"
])
```