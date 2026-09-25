# AI Security Code Reviewer

## 1. Project Overview

AI Security Code Reviewer is a Python-based AI application that reviews source code for common security vulnerabilities.

The application accepts a natural-language security question, a code snippet, and an optional programming language. It uses the Gemini API with a system prompt that defines the model as an AI security expert.

When the model identifies that the submitted code may contain security risks, it can automatically call the local `scan_vulnerabilities` tool. The tool scans the code using security rules and returns structured findings. Gemini then uses these findings to generate a clear security review.

---

## 2. Objective

The main objective of this project is to demonstrate how an LLM can be combined with a local security-analysis tool to automatically identify and explain common vulnerabilities in source code.

The application provides:

- A summary security verdict
- Detected vulnerabilities
- Severity levels
- Line references
- Suggested fixes
- Plain-language explanations

---

## 3. Features

- Natural-language security questions
- Source-code security analysis
- Gemini API integration
- AI-powered security review
- Automatic function/tool calling
- Local vulnerability scanner
- Structured security findings
- Severity classification
- Line references
- Suggested security fixes
- Plain-language explanations
- Clean-code handling
- API and tool error handling
- Independent unit testing of the scanner

---

## 4. Vulnerabilities Detected

The local `scan_vulnerabilities()` tool checks for the following common security issues:

### 4.1 Hardcoded Secrets

Detects possible hardcoded:

- Passwords
- API keys
- Secrets
- Tokens
- Credentials

Example:

```python
password = "admin123"
```

Recommended solution:

Store sensitive information in environment variables or a secure secrets-management system.

---

### 4.2 Code Injection

Detects the use of:

```python
eval()
exec()
```

These functions can become dangerous when used with untrusted input.

Recommended solution:

Avoid using `eval()` or `exec()` with untrusted data and use safer alternatives.

---

### 4.3 SQL Injection

Detects possible SQL queries constructed using string concatenation or interpolation.

Example:

```python
query = "SELECT * FROM users WHERE id=" + user_id
```

Recommended solution:

Use parameterized queries or prepared statements.

---

### 4.4 Command Injection

Detects the use of:

```python
subprocess(..., shell=True)
```

Recommended solution:

Avoid `shell=True` where possible and pass command arguments safely as a list.

---

### 4.5 Insecure Deserialization

Detects potentially unsafe deserialization such as:

```python
pickle.loads(data)
```

and unsafe:

```python
yaml.load(data)
```

without appropriate safe loading.

Recommended solution:

Avoid deserializing untrusted data and use safe deserialization methods.

---

### 4.6 Weak Hashing

Detects the use of:

```python
md5()
sha1()
```

for password hashing.

Recommended solution:

Use modern password-hashing algorithms such as Argon2, bcrypt, or scrypt.

---

### 4.7 Missing Input Validation

Detects direct use of:

```python
input()
```

where user-controlled data is accepted without visible validation.

Recommended solution:

Validate, sanitize, and constrain user input before processing it.

This is implemented as a heuristic and does not prove that validation is completely absent.

---

## 5. Technology Stack

* Python 3.10+
* Google Gemini API
* Google Gen AI Python SDK
* Regular Expressions
* Pytest
* VS Code

---

## 6. Project Structure

```text
code_sentry/
│
├── main.py
├── tools.py
├── prompts.py
├── README.md
│
└── tests/
    └── test_tools.py
```

### File Description

### `main.py`

Contains the main application logic.

It:

* Reads the Gemini API key
* Accepts the user's security question
* Accepts the code snippet
* Accepts the programming language
* Sends the request to Gemini
* Provides `scan_vulnerabilities` as a callable tool
* Displays the final security review

### `tools.py`

Contains the local:

```python
scan_vulnerabilities()
```

function.

It performs heuristic security checks and returns structured findings.

### `prompts.py`

Contains the system prompt that defines Gemini as an AI security code reviewer.

### `tests/test_tools.py`

Contains unit tests for the vulnerability scanner.

### `README.md`

Contains project documentation, setup instructions, examples, testing information, and limitations.

---

## 7. Requirements

Before running the project, make sure the following are installed:

* Python 3.10 or higher
* Gemini API key
* Google Gen AI SDK
* Pytest

---

## 8. Installation

Install the Google Gen AI SDK:

```bash
pip install google-genai
```

Install pytest:

```bash
pip install pytest
```

---

## 9. Gemini API Key Setup

The application reads the Gemini API key from the environment variable:

```text
GEMINI_API_KEY
```

### Windows PowerShell

Set the API key using:

```powershell
$env:GEMINI_API_KEY="YOUR_API_KEY"
```

Verify that the key is available without displaying the actual key:

```powershell
if ($env:GEMINI_API_KEY) { Write-Host "API key is set" } else { Write-Host "API key is missing" }
```

The API key should never be hardcoded in the source code or uploaded to GitHub.

---

## 10. Running the Application

Open the terminal in the project directory:

```text
code_sentry
```

Run:

```powershell
python main.py
```

The application displays:

```text
============================================================
          AI SECURITY CODE REVIEWER
============================================================

Enter your security question:
```

The user is then asked for:

1. Security question
2. Code snippet
3. Programming language

After entering the complete code, type:

```text
END
```

on a new line.

---

## 11. Example: Vulnerable Code

### Security Question

```text
Is this code secure?
```

### Code

```python
password = "admin123"

user_input = input("Enter expression: ")
result = eval(user_input)
```

### Programming Language

```text
Python
```

### Example Result

The application can produce a result similar to:

```text
SECURITY REVIEW

Summary Verdict:
HIGH RISK

Findings:

Finding 1: Code Injection
Severity: High
Line Reference: Line 4

Suggested Fix:
Avoid using eval() with untrusted user input.

Finding 2: Hardcoded Secret
Severity: High
Line Reference: Line 1

Suggested Fix:
Store passwords and secrets in environment variables
or a secure secrets-management system.
```

The exact wording of the Gemini response may vary.

---

## 12. Example: Clean Code

### Security Question

```text
Is this code secure?
```

### Code

```python
def add_numbers(a, b):
    return a + b

result = add_numbers(10, 20)
print(result)
```

### Programming Language

```text
Python
```

### Expected Result

The application should report that no obvious security vulnerabilities were identified in the submitted code.

For example:

```text
SECURITY REVIEW

Summary Verdict:
SAFE

Findings:
No security vulnerabilities were identified in this code snippet.
```

The exact wording of the Gemini response may vary.

---

## 13. Automatic Tool Calling

The project uses Gemini's automatic function/tool calling capability.

The local scanner is provided to the model as a callable tool:

```python
tools=[scan_vulnerabilities]
```

The application does not always run the scanner before sending every request.

Instead, the model can determine when the scanner is relevant based on the user's question and submitted code.

The general workflow is:

```text
User
  |
  | Security Question + Code
  v
Gemini
  |
  | Detects potential security risk
  v
scan_vulnerabilities()
  |
  | Structured Findings
  v
Gemini
  |
  | Explanation + Recommendations
  v
Security Review
```

---

## 14. Structured Scanner Output

The local scanner returns findings in a structured format.

Example:

```python
{
    "findings": [
        {
            "category": "Hardcoded Secret",
            "severity": "High",
            "line": 1,
            "description": "A possible secret or credential is hardcoded.",
            "fix": "Store secrets in environment variables or a secure secret manager."
        }
    ]
}
```

This structure allows the AI model to use the scanner results when generating the final security review.

---

## 15. Testing

The vulnerability scanner can be tested independently without calling the Gemini API.

Run:

```powershell
python -m pytest
```

The test suite contains eight tests covering:

1. Hardcoded secrets
2. `eval()` / `exec()`
3. SQL injection
4. `subprocess` with `shell=True`
5. Insecure deserialization
6. Weak hashing
7. Clean code
8. Missing input validation

Expected result:

```text
8 passed
```

The scanner tests are kept separate from the Gemini integration so that the local security logic can be tested independently.

---

## 16. Error Handling

The application handles several basic error conditions.

### Missing API Key

If `GEMINI_API_KEY` is not configured, the application displays:

```text
Error: GEMINI_API_KEY environment variable is not set.
```

### Empty Code

If no code is entered, the application displays:

```text
Error: Code snippet cannot be empty.
```

### Gemini/API Errors

API communication errors are caught and displayed instead of causing the application to crash unexpectedly.

---

## 17. Assumptions and Limitations

The local scanner uses regular expressions and heuristic rules rather than a complete static-analysis engine.

Therefore:

* It may produce false positives.
* It may miss vulnerabilities that require deeper program analysis.
* The missing-input-validation check is heuristic.
* Detecting `input()` does not prove that validation is completely absent.
* The scanner is intended as a security review aid and not as a replacement for a complete professional security audit.

The AI-generated security explanation may also vary between requests because the response is generated by the Gemini model.

---

## 18. Security Considerations

The Gemini API key should be stored as an environment variable and should not be included directly in source code.

The project should not be committed to a public repository with a real API key.

Sensitive source code should also be handled carefully because the application sends the submitted code to the configured Gemini API.

---

## 19. Project Testing Summary

The project was tested using both local unit tests and Gemini integration tests.

### Local Scanner Test

```text
8 passed
```

### Vulnerable Code Test

The application successfully identified:

* Hardcoded credentials
* Code injection through `eval()`

and generated a high-risk security review.

### Clean Code Test

The application successfully returned a safe result for a simple arithmetic function with no detected security vulnerabilities.

---

## 20. Conclusion

The AI Security Code Reviewer demonstrates the integration of an LLM with a local security-analysis tool.

The local scanner detects common security vulnerability patterns and returns structured findings, while Gemini automatically uses the tool when appropriate and converts the findings into a readable security review.

The project also includes independent unit tests to verify the correctness of the vulnerability scanner.