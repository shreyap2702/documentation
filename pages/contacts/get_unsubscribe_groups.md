# get_unsubscribe_groups

Retrieve all unsubscribe groups associated with a specific contact.  
This method queries the `GET /contacts/{id}/unsubscribe-groups` endpoint and returns the groups the contact is currently unsubscribed from or subscribed to.

---

## What this function does

`get_unsubscribe_groups()` takes a contact ID, validates that it is not empty, and then fetches the unsubscribe group settings for that contact.  
This is useful for checking which marketing categories or email groups the user is subscribed or unsubscribed from.  
If the contact ID is missing or invalid, validation fails before the request is made.

---

## Arguments

**contact_id**  
A non-empty string representing the AutoSend contact identifier.  
This is the system-generated contact ID returned during contact creation or update operations.

---

## Returns

The response from AutoSend containing the unsubscribe preferences for the specified contact.  
The response typically includes information about subscription groups and the contact’s opt-in or opt-out status for each group.

---

## Errors

**ValueError**  
Raised when `contact_id` is empty or missing.

**APIError**  
Raised when the API returns an authentication error, invalid contact ID error, or any server-side failure.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

groups = client.contacts.get_unsubscribe_groups("contact_123")

print(groups)
```