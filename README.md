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
 
