# `get_contact()`

Retrieve a single contact from AutoSend using its unique contact ID.  
This method calls the `GET /contacts/{id}` endpoint and returns all stored details for that contact.


---

## What this function does

`get_contact()` takes a contact ID and returns the full contact record stored in AutoSend.  
It validates that the ID is not empty, then performs a GET request to retrieve the contact.  
If the contact does not exist or the ID is invalid, the method raises an error.

---

## Arguments

**`contact_id`**  
A non-empty string representing the unique identifier of the contact to retrieve.  
This ID is the internal AutoSend contact ID returned during create or update operations.

---

## Returns

A dictionary containing the contact information stored in AutoSend.  
The response may include fields such as:

- name  
- email  
- phone  
- custom fields  
- subscription status  
- unique contact ID  

The exact structure depends on what data exists for that contact.

---

## Errors

### ValueError
Raised when the provided `contact_id` is empty or missing.

### NotFoundError
Raised when no contact exists with the given ID.

### APIError
Raised for any API failure, including invalid authentication or server errors.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

contact = client.contacts.get_contact("contact_123")

print(contact["email"])
````