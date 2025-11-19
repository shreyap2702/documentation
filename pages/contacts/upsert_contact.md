# `upsert_contact()`

Create a new contact or update an existing one using the `/contacts/email` endpoint.  
This method is recommended for contact synchronization because it automatically updates a contact if the email already exists.

---

## What this function does

`upsert_contact()` checks whether a contact with the given email already exists.  
If it exists, the contact is updated with the new information.  
If it does not exist, a new contact is created.  
The method validates email format, ensures required names are provided, and verifies that custom fields are structured correctly.

## Arguments

**`email`**
The contact’s email address. Must follow a valid email format.

**`first_name`**
The contact’s first name. Cannot be empty.

**`last_name`**
The contact’s last name. Cannot be empty.

**`user_id`**
Optional user identifier assigned by your application.

**`custom_fields`**
Optional dictionary containing additional metadata for the contact.
Must be a valid dictionary if provided.

---

## Errors

### ValidationError
This error is raised when the email is invalid, when first name or last name is empty, or when custom fields are not in dictionary format.

### APIError
Returned when the AutoSend API fails to process the request (4xx or 5xx errors).

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.contacts.upsert_contact(
    email="john.doe@example.com",
    first_name="John",
    last_name="Doe"
)
```