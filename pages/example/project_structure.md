# Project Structure
This example follows a clean, modular FastAPI layout inside `src/app/`.
Each file has a clear responsibility, making the flow easy to understand and extend.

---

## **Directory Layout**

```
src/
  app/
    database.py        # Database engine + session dependency
    main.py            # FastAPI app, routes (/subscribe, /send-bulk)
    models.py          # SQLAlchemy ORM models (Subscriber)
    schemas.py         # Pydantic request/response schemas
    services.py        # Business logic layer
    __pycache__/
README.md
```

---

## **File-by-File Overview**

### **1. `database.py`**

* Creates the SQLAlchemy engine (SQLite by default).
* Manages the session.
* Provides a `get_db` dependency used by routes.

**Purpose:**
All database connections and session handling in one place.

---

### **2. `models.py`**

Defines a single ORM model:

* `Subscriber`

  * `id: int`
  * `name: str`
  * `email: str`
  * `categories: list[str]` stored as a JSON field

**Purpose:**
Represents each subscriber stored locally.

---

### **3. `schemas.py`**

Contains the Pydantic models for request/response validation:

* `SubscriberIn` — input for `/subscribe`
* `BulkEmailRequest` — input for `/send-bulk`
* Category validation (allowed values)

**Purpose:**
Validates all incoming data to ensure clean, typed inputs.

---

### **4. `services.py`**

This is where most logic lives.

It contains two key functions:

#### **`add_subscriber(db, sub)`**

* Saves subscriber locally
* Calls `client.contacts.create_contact(...)`
* Syncs them with Autosend Contacts

#### **`send_bulk_email(db, payload)`**

* Fetches subscribers for the selected category
* Builds recipient dictionaries
* Calls `client.sending.send_bulk(...)`

**Purpose:**
Central business layer connecting DB ↔ Autosend SDK.

---

### **5. `main.py`**

Defines the FastAPI app and endpoints:

* **POST `/subscribe`**
  Creates a new subscriber and syncs with Autosend.

* **POST `/send-bulk`**
  Sends bulk emails to subscribers in a given category.

**Purpose:**
Entry point of the server and routing layer.

---

## **Why Structure It This Way?**

This layout keeps:

* API routing
* business logic
* validation
* storage
* Autosend SDK calls

**cleanly separated**, making the example easy to extend or use as a template.

