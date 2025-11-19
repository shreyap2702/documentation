# Contact Validation Utilities

The `Contacts` class includes small internal validation helpers used to ensure contact data is well-formed before being sent to the AutoSend API.  
These helper methods are not meant to be used directly by developers, but they are important for understanding how the SDK validates inputs internally.

---

## `_validate_email()`

Validates that an email address is correctly formatted.

### What this function does

This method checks that the email value is not empty and contains an `@` symbol.  
If the email is missing or incorrectly formatted, it raises a `ValidationError`.  
This validation is applied before creating, updating, or searching contacts to prevent invalid data from being sent to the API.

### Arguments

**email**  
The email address being validated.  
Must be a non-empty string containing an `@`.

**field**  
Internal field name used in error messages.  
Defaults to `"email"`.

---

## `_validate_non_empty()`

Ensures that a required string field is not empty.

### What this function does

This method checks that the provided value is not empty and does not consist only of whitespace.  
If the value is empty, a `ValidationError` is raised.  
This validation is applied to contact fields such as `firstName`, `lastName`, and other required strings.

### Arguments

**value**  
The string to validate.  
Must be non-empty after trimming whitespace.

**field**  
Name of the field being validated.  
This is included in any error message for clarity.