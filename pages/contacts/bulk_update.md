# `bulk_update()`

Create or update multiple contacts in a single request.  
This method uses the `POST/contacts/bulk-update` endpoint to process up to 100 contacts at once.

---

## What this function does

`bulk_update()` accepts a list of contact dictionaries.  
Each contact is uniquely identified by its email address.  
If a contact already exists, it is updated; if it does not exist, it is created.  
All contacts are validated before sending the request, including checking that emails are provided and correctly formatted.  
This method allows efficient synchronization of large contact lists.

---

## Arguments

**`contacts`**  
A list containing one or more contact dictionaries.  
Each contact must include an `email` field.  
The list must not be empty and cannot exceed one hundred contacts.  
Each email address is validated before the request is made.

**`run_workflow`**  
A boolean value indicating whether associated workflows should be triggered after updating the contacts.  
Defaults to `False`.

---

## Returns

A dictionary containing the bulk update results.  
The response includes the status of each contact, indicating whether it was created, updated, or failed.

---

## Errors

### ValidationError
Raised when the list is empty, when the list is not a proper list, when it exceeds one hundred items, or when a contact is missing an email or contains an invalid email address.

### APIError
Raised when the AutoSend API fails to process the request due to authentication errors, invalid payload, or internal server issues.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

contacts_to_update = [
    {"email": "john@example.com", "firstName": "John"},
    {"email": "jane@example.com", "firstName": "Jane"}
]

result = client.contacts.bulk_update(contacts_to_update)

print(result)
```
