# Introduction
This example demonstrates how to integrate the **Autosend Python SDK** into a simple FastAPI backend.
The goal is to show how Autosend can be plugged into a real-world service that handles:

* **Storing subscribers locally**
* **Syncing subscribers to Autosend Contacts**
* **Sending category-based bulk emails**
* **Handling unsubscribe groups per category**

This is a minimal app designed for learning and reference—not production complexity.

---

## What this Example Does

### **1. Store Subscribers**

When a user subscribes, their:

* name
* email
* category preferences

are saved in a local SQLite database.

---

### **2. Sync with Autosend Contacts**

Every subscriber is also added to Autosend Contacts using:

```python
client.contacts.create_contact(...)
```

This keeps your internal subscriber list consistent with Autosend.

---

### **3. Send Category-Targeted Bulk Emails**

A `/send-bulk` endpoint allows sending bulk emails to all subscribers belonging to a specific category.

Under the hood, it uses:

```python
client.sending.send_bulk(...)
```

---

### **4. Category-Based Unsubscribe Mapping**

Each category maps to a specific `unsubscribe_group_id`, so subscribers can opt-out of individual groups.

---

## High-Level Flow

```
Subscribe → Store in DB → Sync to Autosend → Send Bulk Email → Respect Unsubscribe Groups
```

---

## Who This Example Is For

* Developers integrating Autosend into FastAPI services
* Teams wanting to understand Contacts + Bulk Send usage
* Anyone who needs a clean starting point to build a full emailing backend