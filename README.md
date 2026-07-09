# cog-day-1

session #2 

Inline Suggestions
These keys help you control the gray text that Copilot types while you work. [1]
Accept suggestion: Tab
Accept next word: Ctrl + Right Arrow (Windows) | Cmd + Right Arrow (Mac)
Accept next line: Ctrl + Enter (Windows) | Cmd + Enter (Mac)
Dismiss suggestion: Escape [1, 2]
Suggestions Window
Sometimes Copilot gives you more than one choice. Use these keys to see them. [1]
Next suggestion: Alt + ] (Windows/Linux) | Option + ] (Mac)
Previous suggestion: Alt + [ (Windows/Linux) | Option + [ (Mac) [1]
Chat and Tools
These keys open the chat panel so you can talk to Copilot and ask questions. [1]
Open chat panel: Ctrl + Alt + I (Windows/Linux)
Inline chat / Ask question: Ctrl + I (Windows/Linux) [1]
 




Lab 1: The Prompt Makeover
Objective: Move candidates from writing naive, single-line prompts that yield fragile code to constructing engineered, deterministic prompts that generate production-ready software.
The Setup: Your Codespace Environment
Before running these exercises, ensure your candidates have their VS Codespace open and have created a baseline project structure. For this lab, we are building a Secure File Processing & Metadata Extraction Utility in Python.
Instruct candidates to create an empty file named processor.py and open it. This will be their active editor window.
Step 1: The Vague & Broken Way (The Wrong Way)
In this step, we simulate how an untrained developer interacts with GitHub Copilot.
Instructions for Candidates
Open processor.py.
Open Copilot Chat (Ctrl + Shift + I or the sidebar).
Copy and paste the following vague prompt and hit Enter.
The Vague Prompt
Plaintext
 
 
write a python script to read a user data file and parse it into json and log it
 
 
 
Step 2: The Refactored Way (The Right Way)
Now, we will completely overhaul the prompt by applying the Anatomy of a Great Prompt and a Chain-of-Thought (CoT) paradigm.
Instructions for Candidates
Clear the contents of processor.py.
In Copilot Chat, paste the engineered prompt below and hit Enter.
The Refactored Prompt
Markdown
 
# GOALBuild a robust, production-ready Python utility function called `safe_ingest_user_metadata` that safely processes an incoming JSON file and validates its structural integrity.
# CONTEXT- Runtime: Python 3.11+- Data Validation: Use Pydantic v2 to enforce field-level constraints.- Logging: Use Python's built-in `logging` module to output structured validation messages.
# CONSTRAINTS- Resource Security: File parsing must use a secure context manager to handle system resources safely.- Explicit Error Boundaries: Catch and log `FileNotFoundError`, `PermissionError`, and Pydantic `ValidationError` explicitly. Return a tuple of (bool, dict_or_error_message).
- Memory Constraint: Do not read the entire file into memory at once if it exceeds a threshold; assume it could be large.
- No absolute path executions; restrict lookups to localized data directories.
# CHAIN-OF-THOUGHT LOGIC
Process the request using these sequential steps:
1. Define a Pydantic schema class `UserMetadata` with fields: `user_id` (int), `email` (str), and `signup_date` (ISO date string).
2. Validate the path using `pathlib.Path`.
3. Open the file securely, read the JSON stream, and deserialize it.
4. Pass the dictionary into the Pydantic schema inside an explicit try-except matrix.
5. Log a structured success or failure message containing the `user_id`.
# EXPECTED OUTPUT SCHEMAIf successful, return: (True, {"status": "validated", "payload": PydanticModel})
If failed, return: (False, {"status": "failed", "reason": "Error details string"})




 Another :


 🚫 The Bad Prompt
"Write a python pandas script to clean some order data and make sure it has no null values."
⚡ The Good Prompt (Context-Aware Architecture)
Markdown
 
# ROLEYou are an expert Lead Data Engineer specializing in robust, distributed data pipelines.
# GOALBuild a production-grade Python function named `clean_and_bound_orders` using the pandas library that sanitizes an incoming DataFrame of e-Commerce orders.
# CONTEXT & CONSTRAINTS- Input Columns: `order_id` (str), `customer_id` (str), `order_amount` (float), `timestamp` (str), `coupon_code` (str).- Null Boundaries: `order_id`, `customer_id`, and `order_amount` have strict non-null boundaries. Drop any rows failing this. `coupon_code` can be null; fill missing values with the string "NONE".- Type Enforcement: Convert `timestamp` into a standard ISO datetime object. If parsing fails, drop the row.- Output: Return a clean, strictly typed pandas DataFrame along with a tracking dictionary showing metadata execution metrics (e.g., rows dropped, clean rows remaining).
# EXPECTED BEHAVIOREnsure the function handles empty dataframes gracefully without raising unhandled memory or index exceptions.
 
