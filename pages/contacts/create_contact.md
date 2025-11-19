# create_contact

Create a new contact in AutoSend using the `/contacts` endpoint.  
This method registers a contact with required fields and optional metadata.  
The SDK performs validation before sending the request.

---

## What this function does

`create_contact()` creates a contact record inside AutoSend’s contact database.  
It validates the email format, checks that the first and last names are not empty, and ensures that custom fields (if provided) follow the correct structure.  
Once validated, the contact is created through the API.

---

## Function Definition

<details>
<summary><strong>Click to view full function</strong></summary>

```python
def create_contact(
    self,
    email: str,
    first_name: str,
    last_name: str,
    user_id: str | None = None,
    custom_fields: Dict[str, Any] | None = None,
) -> Any:
    """
    Create a new contact in the system.
    """

    logger.info("Creating contact: %s", email)

    self._validate_email(email)
    self._validate_non_empty(first_name, "firstName")
    self._validate_non_empty(last_name, "lastName")

    if custom_fields is not None and not isinstance(custom_fields, dict):
        raise ValidationError(
            "custom_fields must be a dictionary.", field="customFields"
        )

    payload = {
        "email": email,
        "firstName": first_name,
        "lastName": last_name,
    }

    if user_id:
        payload["userId"] = user_id

    if custom_fields:
        payload["customFields"] = custom_fields

    logger.debug("Contact payload validated and ready for creation.")
    return self._client.post("/contacts", data=payload)
````

</details>

---

## Arguments

**email**
The contact’s email address. Must be in a valid email format.

**first_name**
The contact’s first name. Cannot be empty.

**last_name**
The contact’s last name. Cannot be empty.

**user_id**
Optional user identifier that you may use to associate this contact with your internal system.

**custom_fields**
Optional dictionary containing any additional key–value metadata for the contact.
Must be a dictionary if provided.

---

## Errors

**ValidationError**
This error is raised when the provided email is invalid, when first name or last name is empty, or when custom fields are not a dictionary.

**APIError**
Returned when the AutoSend API rejects the request (for example, invalid payload or authentication failure).

---

## Example

```python
from autosend import AutosendClient

client = AutosendClient(api_key="YOUR_AUTOSEND_API_KEY")

client.contacts.create_contact(
    email="john.doe@example.com",
    first_name="John",
    last_name="Doe"
)
```