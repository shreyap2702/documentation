# upsert_contact

Create a new contact or update an existing one using the `/contacts/email` endpoint.  
This method is recommended for contact synchronization because it automatically updates a contact if the email already exists.

---

## What this function does

`upsert_contact()` checks whether a contact with the given email already exists.  
If it exists, the contact is updated with the new information.  
If it does not exist, a new contact is created.  
The method validates email format, ensures required names are provided, and verifies that custom fields are structured correctly.

---

## Function Definition

<details>
<summary><strong>Click to view full function</strong></summary>

```python
def upsert_contact(
    self,
    email: str,
    first_name: str,
    last_name: str,
    user_id: str | None = None,
    custom_fields: Dict[str, Any] | None = None,
) -> Any:
    """
    Create a new contact or update an existing contact if the email already exists.
    """

    logger.info("Upserting contact: %s", email)

    self._validate_email(email)
    self._validate_non_empty(first_name, "firstName")
    self._validate_non_empty(last_name, "lastName")

    if custom_fields is not None and not isinstance(custom_fields, dict):
        raise ValidationError("custom_fields must be a dictionary.", field="customFields")

    payload = {
        "email": email,
        "firstName": first_name,
        "lastName": last_name,
    }

    if user_id:
        payload["userId"] = user_id

    if custom_fields:
        payload["customFields"] = custom_fields

    logger.debug("Contact payload validated for upsert.")
    return self._client.post("/contacts/email", data=payload)
````

</details>

---

## Arguments

**email**
The contact’s email address. Must follow a valid email format.

**first_name**
The contact’s first name. Cannot be empty.

**last_name**
The contact’s last name. Cannot be empty.

**user_id**
Optional user identifier assigned by your application.

**custom_fields**
Optional dictionary containing additional metadata for the contact.
Must be a valid dictionary if provided.

---

## Errors

**ValidationError**
This error is raised when the email is invalid, when first name or last name is empty, or when custom fields are not in dictionary format.

**APIError**
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