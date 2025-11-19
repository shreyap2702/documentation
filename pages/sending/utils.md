# Validation Utilities (Sending Module)

The `Sending` class includes internal validation helpers used to ensure emails, templates, attachments, and unsubscribe settings meet AutoSend’s requirements.  
These functions are internal and not meant to be used directly, but understanding them helps explain how the SDK performs input validation before sending emails.

---

## `_extract_placeholders()`

Extracts template variables from HTML content.

This function scans the HTML and detects template placeholders written in the form `{{ name }}`, `{{ plan }}`, or `{{ userId }}`.  
It returns a set of placeholder names found inside the HTML.

### Arguments

**html**  
HTML string that may contain template variables.

### Used By

`_validate_dynamic_data()` — to verify that dynamic data keys match placeholders inside the HTML.

---

## `_validate_dynamic_data()`

Ensures that the `dynamic_data` dictionary correctly matches the template placeholders inside the HTML content.

First, it extracts all placeholders from the HTML using `_extract_placeholders()`.  
Then it compares them with the keys provided in `dynamic_data`.  
If a placeholder is missing in `dynamic_data`, a `ValidationError` is raised.  
If the HTML contains placeholders but `dynamic_data` is empty, validation fails.  
If extra keys are present in `dynamic_data`, they are allowed but logged for debugging.

### Arguments

**html**  
HTML content of the email which may contain placeholders.

**dynamic_data**  
Dictionary containing keys that must correspond to placeholder names inside the HTML.

### Key validations

Missing placeholder keys result in a `ValidationError`.  
Providing no dynamic data when HTML expects them results in a `ValidationError`.  
Extra keys are permitted but noted in logs.

---

## `_validate_attachments()`

Validates the structure, count, and file type of email attachments.

Ensures that attachments do not exceed the maximum limit of twenty files.  
Checks that each attachment has a valid filename.  
Rejects attachments containing blocked file extensions such as `.exe`, `.bat`, `.cmd`, and other unsafe types used in email security filtering.

### Arguments

**attachments**  
A list of attachment objects or `None`.

### Key validations

More than twenty attachments results in a `ValidationError`.  
Blocked file extensions cause a `ValidationError`.  
Only safe, supported file types are allowed.

---

## `_validate_unsubscribe()`

Validates the unsubscribe URL format used in marketing or bulk emails.

Ensures the unsubscribe URL begins with either `http://` or `https://`.  
Any other format is considered invalid and results in a `ValidationError`.  
This validation ensures compliance with RFC 2369 unsubscribe standards.

### Arguments

**unsubscribe_url**  
A string URL or `None`.

### Key validations

The URL must be a valid HTTP or HTTPS link.  
Invalid formats trigger a `ValidationError`.

