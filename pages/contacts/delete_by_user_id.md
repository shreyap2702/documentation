# `delete_by_user_id()`

Delete a contact from AutoSend using your application’s user identifier.  
This method sends a request to the `DELETE /contacts/email/userId/{userId}` endpoint and permanently removes the associated contact.

---

## What this function does

`delete_by_user_id()` deletes a contact based on the `userId` field, which represents your internal user identifier.  
The method validates that the provided user ID is not empty.  
If valid, it performs a DELETE request to remove the contact from AutoSend.  
If the user ID is missing or invalid, an error is raised before the request is made.

---

## Arguments

**`user_id`**  
A non-empty string representing your application’s unique user identifier.  
This value is matched against the `userId` field stored for a contact in AutoSend.

---

## Returns

The response returned by the API delete operation.  
The structure typically includes confirmation of deletion or any related metadata from AutoSend.

---

## Errors

### ValueError
Raised when the provided `user_id` is empty or invalid.

### APIError
Raised when the API rejects the request or returns a failure status, such as authentication issues or a missing contact record.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.contacts.delete_by_user_id("user_12345")
```