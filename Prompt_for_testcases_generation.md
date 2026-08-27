> \*\*Act as a Senior QA Lead.\*\* Based on the Epic provided below, generate a comprehensive Test Suite.

>

> \*\*Requirements for the Output:\*\*

>

> 1.  \*\*Categorization:\*\* Segregate test cases into the following types: Functional, Validation, Negative, Edge Case, API, and UI/UX.

> 2.  \*\*Structure:\*\* Use a Markdown table format with the following columns: \*\*TC-ID\*\*, \*\*Test Scenario\*\*, \*\*Test Steps\*\*, \*\*Expected Result\*\*, and \*\*Priority\*\* (P0: Critical, P1: High, P2: Medium, P3: Low).

> 3.  \*\*Naming Convention:\*\* All Scenario Summaries must follow the professional format: \*"Verify \[Action] when \[Condition]..."\*

> 4.  \*\*Coverage:\*\* Ensure full traceability to the Epic, covering data integrity, error handling, and boundary conditions.

>

###### > \*\*\[INSERT EPIC DESC]\*\*



\-----



\### Example of what the output will look like



\*Using a "User Login" Epic as a placeholder example:\*



\#### 1\\. Functional Test Cases



| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |

| :--- | :--- | :--- | :--- | :--- |

| \*\*FT-01\*\* | Verify successful login with valid credentials. | 1. Enter valid email.
2. Enter valid password.
3. Click "Login". | User is redirected to the dashboard. | P0 |



\#### 2\\. Negative \& Validation Test Cases



| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |

| :--- | :--- | :--- | :--- | :--- |

| \*\*NV-01\*\* | Verify error message when password field is empty. | 1. Enter valid email.
2. Leave password blank.
3. Click "Login". | System displays "Password is required" validation. | P1 |



\#### 3\\. API Test Cases



| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |

| :--- | :--- | :--- | :--- | :--- |

| \*\*API-01\*\* | Verify POST /auth/login returns 200 OK with Bearer token. | Send POST request with valid JSON payload. | Response code 200 and a valid JWT token is returned. | P0 |



\-----



\### Pro-Tips for a QA Lead



&#x20; \* \*\*Edge Cases:\*\* When you provide the Epic, if there are date pickers, currency fields, or file uploads, I will automatically include "Leap Year," "Zero Balance," and "Over-limit file size" scenarios.

&#x20; \* \*\*UI/UX:\*\* These will focus on accessibility (WCAG), responsiveness, and element alignment.


Use (instead of P0,P1,P2,P3 use Critical, High, Medium, Low)

I want ID-s like 'FT-01' , 'VAL-01', 'NEG-01', 'EDGE-01', 'API-01', 'UI-01' 



 