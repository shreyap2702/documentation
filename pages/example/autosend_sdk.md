# Using the Autosend SDK

This example integrates the **Autosend Python SDK** directly inside the service layer (`services.py`).
The SDK is used for two main purposes:

1. **Creating contacts** when a subscriber joins
2. **Sending bulk emails** to a specific category

This page explains exactly how and where the SDK is used.

---

## 1. SDK Initialization

Inside `services.py`, the SDK client is created:

```python
client = AutosendClient(api_key="YOUR_API_KEY")
```

> Note: In the demo, the key is hardcoded.
> In production, load it using environment variables.

Example:

```python
import os
client = AutosendClient(api_key=os.getenv("AUTOSEND_API_KEY"))
```

---

## 2. Adding a Contact

When a subscriber joins via `/subscribe`, the service stores them locally and then syncs them to Autosend using:

```python
client.contacts.create_contact(
    email=sub.email,
    first_name=sub.name.split()[0],
    last_name=sub.name.split()[-1],
    user_id=None,
    custom_fields={"categories": sub.categories}
)
```

### **Why this matters**

* Your FastAPI app stores subscribers for your own logic.
* Autosend also needs the subscriber so it can include them in bulk sends.
* This keeps both systems consistent.

---

## 3. Sending Bulk Email

The `/send-bulk` endpoint dispatches category-specific campaign emails.

Inside `services.py`, the code:

1. **Fetches subscribers** in the chosen category
2. **Builds a list of recipients:**

```python
recipients = [
    {
        "email": s.email,
        "name": s.name,
        "dynamicData": {}
    }
    for s in subscribers
]
```

3. **Calls the SDK’s bulk send API:**

```python
client.sending.send_bulk(
    recipients=recipients,
    from_email=payload.from_email,
    from_name=payload.from_name,
    subject=payload.subject,
    html=payload.html,
    dynamic_data={},
    unsubscribe_group_id=unsubscribe_group_id
)
```

---

## 4. What the SDK Enables in This Example

| Feature                | What the SDK Enables                        |
| ---------------------- | ------------------------------------------- |
| Contacts sync          | Ensures every subscriber exists in Autosend |
| Bulk sending           | Send campaign emails to lists of recipients |
| dynamicData            | Supports variable/template replacements     |
| Unsubscribe groups     | Category-specific opt-out behavior          |
| Attachments (optional) | Supported but not used in the example       |

---

## Takeaway

The Autosend SDK in this example acts as a **bridge** between:

**Local subscribers → Autosend Contacts → Bulk Send API**

Your FastAPI server remains the controller; Autosend handles the email delivery.
