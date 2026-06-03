# Excel Test Case Auto-Fill Tool

This utility reads test cases from `testcases.txt` and automatically populates the corresponding rows in `template.xlsx`, generating an output Excel file.

---

# Folder Structure

```text
project/
│
├── fill_excel.py
├── template.xlsx
├── testcases.txt
├── requirements.txt
│
└── output/
    └── output.xlsx
```

---

# Prerequisites

* Python 3.10 or later
* pip

Verify Python installation:

```bash
python --version
```

---

# Installation

Install required dependencies:

```bash
pip install -r requirements.txt
```

or

```bash
python -m pip install -r requirements.txt
```

---

# Before Running

## 1. Verify Input Files Exist

Ensure the following files are present:

```text
template.xlsx
testcases.txt
fill_excel.py
```

## 2. Delete Existing Output File

To avoid using stale data from previous runs, delete:

```text
output/output.xlsx
```

The script will automatically create a fresh copy from:

```text
template.xlsx
```

Recommended workflow:

```text
Delete output/output.xlsx
↓
Update testcases.txt
↓
Run fill_excel.py
↓
Review output/output.xlsx
```

---

# Running the Script

Execute:

```bash
python fill_excel.py
```

Example:

```bash
python fill_excel.py
```

---

# Output Location

Generated file:

```text
output/output.xlsx
```

---

# Supported Excel Formats

## Sheet Format 1

| Column | Content         |
| ------ | --------------- |
| A      | Test Case ID    |
| B      | Scenario        |
| D      | Steps           |
| F      | Expected Result |
| H      | Priority        |

Example:

| A     | B        | D     | F               | H        |
| ----- | -------- | ----- | --------------- | -------- |
| FT-01 | Scenario | Steps | Expected Result | Critical |

---

## Sheet Format 2

| Column | Content      |
| ------ | ------------ |
| A      | Test Case ID |
| B      | Scenario     |
| C      | Priority     |

Example:

| A     | B        | C        |
| ----- | -------- | -------- |
| FT-01 | Scenario | Critical |

---

# testcases.txt Format

The file must contain Markdown tables.

Each section can contain any category name such as:

```text
1. Functional Test Cases
2. Validation Test Cases
3. Negative Test Cases
4. Edge Cases
5. API Test Cases
6. UI/UX Test Cases
```

The parser reads all tables automatically.

---

# Required Table Format

```markdown
| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| ----- | ------------- | ---------- | --------------- | -------- |
| FT-01 | Verify Configuration screen is displayed when Doctor completes previous order steps | 1. Complete Patient Information.<br>2. Select Bluegrass Tongue Trainer appliance.<br>3. Proceed to Configuration. | Configuration screen loads successfully. | Critical |
| FT-02 | Verify 3D appliance preview is displayed when Configuration screen opens | Open Configuration screen. | 3D appliance preview is visible and rendered correctly. | Critical |
| FT-03 | Verify STL preview is displayed when STL file is available from previous workflow | Open Configuration with STL available. | STL preview is displayed successfully. | High |
```

---

# Rules for testcases.txt

## Mandatory Columns

The following column names must match exactly:

```text
TC-ID
Test Scenario
Test Steps
Expected Result
Priority
```

## Unique Test Case IDs

Each Test Case ID must be unique.

Correct:

```text
FT-01
FT-02
FT-03
```

Incorrect:

```text
FT-01
FT-01
FT-01
```

## Preserve Markdown Table Structure

Do not remove:

```markdown
|
```

Do not remove:

```markdown
| ----- |
```

separator rows.

## Multi-Step Test Cases

Use HTML line breaks:

```text
1. Login.<br>
2. Navigate to Orders.<br>
3. Click Submit.
```

These will automatically become separate lines in Excel.

---

# Example testcases.txt

```markdown
# Functional Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| ----- | ------------- | ---------- | --------------- | -------- |
| FT-01 | Verify Configuration screen is displayed when Doctor completes previous order steps | 1. Complete Patient Information.<br>2. Select Bluegrass Tongue Trainer appliance.<br>3. Proceed to Configuration. | Configuration screen loads successfully. | Critical |
| FT-02 | Verify 3D appliance preview is displayed when Configuration screen opens | Open Configuration screen. | 3D appliance preview is visible and rendered correctly. | Critical |

# Validation Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| ----- | ------------- | ---------- | --------------- | -------- |
| VAL-01 | Verify mandatory field validation | Leave mandatory field blank. | Validation message is displayed. | High |
```

---

# Troubleshooting

## Error: template.xlsx not found

Cause:

```text
template.xlsx is missing
```

Fix:

Place template.xlsx in the project root folder.

---

## Error: testcases.txt not found

Cause:

```text
testcases.txt is missing
```

Fix:

Create or copy testcases.txt into the project folder.

---

## Error: No test cases updated

Possible causes:

* TC IDs do not match Excel sheet IDs.
* Incorrect column names in testcases.txt.
* Markdown table format is broken.

Verify:

```text
TC-ID values in Excel == TC-ID values in testcases.txt
```

---

# Recommended Workflow

```text
1. Update testcases.txt
2. Delete output/output.xlsx
3. Run python fill_excel.py
4. Open output/output.xlsx
5. Verify generated data
```
