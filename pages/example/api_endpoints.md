# API Endpoints

This example provides two main API endpoints:

1. **POST `/subscribe`** — Add a subscriber and sync to Autosend
2. **POST `/send-bulk`** — Send category-targeted bulk emails

Both endpoints live in `src/app/main.py`.

---

## **1. POST `/subscribe`**

### **Purpose**

Store a new subscriber in the local database and create a corresponding contact in Autosend.

### **Request Body (`SubscriberIn`)**

```json
{
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "categories": ["newsletter", "updates"]
}
```

### **Flow**

1. Validate request using Pydantic schema
2. Store subscriber locally
3. Call:

```python
client.contacts.create_contact(...)
```

4. Return success response

### **Typical Response**

```json
{
  "status": "success",
  "message": "Subscriber added and synced."
}
```

---

## **2. POST `/send-bulk`**

### **Purpose**

Send a bulk email to all subscribers belonging to a selected category.

### **Request Body (`BulkEmailRequest`)**

```json
{
  "category": "newsletter",
  "subject": "This Week's News",
  "html": "<p>Hello {{name}}</p>",
  "from_email": "no-reply@example.com",
  "from_name": "Example Team"
}
```

### **Flow**

1. Validate request
2. Query local DB for subscribers in the given category
3. Build recipient objects
4. Determine `unsubscribe_group_id` using category mapping
5. Call:

```python
client.sending.send_bulk(...)
```

### **Typical Response**

```json
{
  "status": "sent",
  "recipients": 12
}
```

---

## **3. Validation Rules**

### **Allowed Categories**

Defined in `schemas.py`, e.g.:

* `newsletter`
* `promotions`
* `updates`

If a request uses an invalid category, FastAPI returns a 422 error before reaching service logic.

---

## **4. Error Handling**

While minimal in the example, ideal behavior is:

* Use FastAPI `HTTPException` for invalid states
* Convert SDK errors into clean JSON errors
* Validate that category has active subscribers

Example:

```python
raise HTTPException(status_code=404, detail="No subscribers found.")
```

---

## **5. Summary of Endpoints**

| Method | Endpoint     | Description                                      |
| ------ | ------------ | ------------------------------------------------ |
| POST   | `/subscribe` | Add subscriber locally & create Autosend Contact |
| POST   | `/send-bulk` | Send email to all subscribers in a category      |

