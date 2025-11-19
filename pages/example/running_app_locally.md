#  Running the Example Locally

This guide walks you through setting up and running the Autosend FastAPI example on your machine.
Follow these steps exactly and the server will start running in a few minutes.

---

## 1. Clone the Repository

```bash
git clone https://github.com/shreyap2702/autosend-sdk-fastapi-example
cd autosend-sdk-fastapi-example
```

---

## 2. Create & Activate a Virtual Environment

### **macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### **Windows (PowerShell)**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```
---

## 3. Set Your Autosend API Key

### **macOS / Linux**

```bash
export AUTOSEND_API_KEY="your_api_key_here"
```

### **Windows (PowerShell)**

```powershell
setx AUTOSEND_API_KEY "your_api_key_here"
```

---

## 4. Start the Server

From the project’s root directory:

```bash
uvicorn app.main:app --reload --app-dir src
```

If installed as a package:

```bash
uvicorn app.main:app --reload
```

---

## 5. Test the Endpoints

Use **curl**, **HTTPie**, or **Postman**.

---

### **a) Test `/subscribe`**

```bash
curl -X POST http://127.0.0.1:8000/subscribe \
  -H "Content-Type: application/json" \
  -d '{
        "name": "Alice Johnson",
        "email": "alice@example.com",
        "categories": ["newsletter"]
      }'
```

You should see:

```json
{
  "status": "success",
  "message": "Subscriber added and synced."
}
```

---

### **b) Test `/send-bulk`**

```bash
curl -X POST http://127.0.0.1:8000/send-bulk \
  -H "Content-Type: application/json" \
  -d '{
        "category": "newsletter",
        "subject": "Hello Subscribers",
        "html": "<p>Hello {{name}}</p>",
        "from_email": "no-reply@example.com",
        "from_name": "Example Team"
      }'
```

Expected output:

```json
{
  "status": "sent",
  "recipients": <number>
}
```

---

## 6. Common Issues

### **1. “KeyError: AUTOSEND_API_KEY”**

You forgot to set the environment variable.

### **2. “404 no subscribers found”**

Your category has no subscribers. Add some via `/subscribe`.

### **3. Database not updating**

Delete the local SQLite file:

```bash
rm subscribers.db
```

and restart.

---

## 7. Stopping the Server

Press:

```
Ctrl + C
```

---

## You’re Ready to Build

You now have a working FastAPI + Autosend integration.
Use this template to extend into real campaigns, dashboards, user systems, or admin tools.

