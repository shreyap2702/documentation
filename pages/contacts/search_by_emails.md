# `search_by_emails()`

Search for multiple contacts at once using a list of email addresses.  
This method sends a request to the `/contacts/search/emails` endpoint and returns all matching contacts.

---

## What this function does

`search_by_emails()` takes one or more email addresses, validates each one, and then performs a search through the AutoSend API.  
If the list is empty or any email address is invalid, validation fails before the request is made.  
After successful validation, the method queries the API and returns all contacts that match the provided emails.

---

## Arguments

**`emails`**  
A list containing one or more email addresses.  
Must not be empty, and each email must be formatted correctly.

---

## Returns

A dictionary containing the contacts found for the given email list.  
Each returned contact may include its stored details such as name, email, custom fields, and other metadata.

---

## Errors

### ValidationError
Raised when no emails are provided or when any email is invalid.

### APIError
Raised when the API request fails due to invalid credentials, incorrect payload, or server issues.

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

results = client.contacts.search_by_emails([
    "user1@example.com",
    "user2@example.com"
])

print(results)
```
