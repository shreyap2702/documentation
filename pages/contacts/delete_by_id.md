# delete_by_id

Delete a contact from AutoSend using its unique contact ID.  
This method calls the `DELETE /contacts/{id}` endpoint and permanently removes the contact.

---

## What this function does

`delete_by_id()` removes a contact from AutoSend by using the system-generated contact identifier.  
The method checks that the contact ID is not empty, then sends a DELETE request to the API.  
If the ID is invalid or the contact does not exist, the API will return an error.

---

## Arguments

**contact_id**  
A non-empty string representing the AutoSend contact identifier.  
This is the unique ID returned whenever a contact is created or updated.

---

## Returns

The API response confirming the deletion.  
This commonly includes fields such as a success status or a message from AutoSend.

---

## Errors

**ValueError**  
Raised when the provided `contact_id` is empty.

**APIError**  
Raised when the API fails to process the delete request due to authentication issues, invalid IDs, or server errors.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.contacts.delete_by_id("contact_123")
```