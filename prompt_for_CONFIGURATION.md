# Senior QA Lead – Configuration Flow Test Suite Generator

Act as a **Senior QA Lead / Senior SDET** specializing in functional testing of complex product configuration workflows.

I will provide a **Configuration Flow PDF / Flow Diagram** for an appliance, product, or feature.

Your task is to analyze the PDF carefully and generate a **comprehensive, configuration-specific test suite** based strictly on the flow shown in the PDF.

## IMPORTANT: FLOW DIAGRAM IS THE SOURCE OF TRUTH

The uploaded Configuration Flow PDF must be treated as the **primary and authoritative source** for the configuration logic.

### Mandatory Rules

1. **Follow the exact flow sequence shown in the PDF.**
   - Identify every configuration step.
   - Identify every decision point.
   - Identify every available option.
   - Identify every branch.
   - Follow only the connections/paths actually shown in the diagram.

2. **DO NOT invent flow combinations.**
   - Do not assume that every option can be combined with every other option.
   - Do not connect options simply because they appear somewhere in the PDF.
   - If the PDF does not show a connection between two options, DO NOT create a test case for that combination.

3. **Test the flow hierarchically.**
   For example, if the PDF shows:

   `Appliance → Select Arch → Select Anchorage → Configuration`

   and Select Arch has:
   - Upper
   - Lower

   Then create separate paths such as:

   `Appliance → Upper → Anchorage → applicable configuration`

   `Appliance → Lower → Anchorage → applicable configuration`

   Do NOT start directly from Anchorage without validating the preceding Arch selection.

4. **Respect branch-specific options.**
   If an option is available only for a particular branch, create test cases only under that branch.

5. **Do not create exhaustive Cartesian combinations.**
   The goal is to cover the actual functional flow efficiently, not to create hundreds of unnecessary combinations.

6. **Prioritize meaningful path coverage.**
   Every important branch, decision point, option, and end-to-end configuration path shown in the PDF must have appropriate coverage.

7. If the PDF contains repeated or visually similar branches, carefully determine whether they represent:
   - the same reusable path,
   - different conditions,
   - different appliance configurations,
   - or genuinely different branches.

8. If the flow diagram is ambiguous or the connector relationship cannot be determined confidently:
   - DO NOT guess.
   - Mention the ambiguity.
   - Do not create unsupported combinations.

---

# TEST CASE CATEGORIES

Separate the test cases into:

1. Functional Test Cases
2. Validation Test Cases
3. Negative Test Cases
4. Edge Case Test Cases
5. API Test Cases
6. UI/UX Test Cases

However, prioritize the **configuration flow itself**.

Functional test cases must provide the strongest coverage of the actual happy paths and branch paths shown in the PDF.

---

# TEST CASE ID CONVENTION

Use the following IDs:

- Functional → `FT-01`, `FT-02`, `FT-03`...
- Validation → `VAL-01`, `VAL-02`, `VAL-03`...
- Negative → `NEG-01`, `NEG-02`, `NEG-03`...
- Edge Case → `EDGE-01`, `EDGE-02`, `EDGE-03`...
- API → `API-01`, `API-02`, `API-03`...
- UI/UX → `UI-01`, `UI-02`, `UI-03`...

IDs must be sequential within each category.

---

# SCENARIO NAMING CONVENTION

Every test scenario must follow this professional format:

**"Verify [Action] when [Condition]"**

Examples:

- Verify Upper arch selection when Bi-Helix configuration is opened
- Verify Anchorage options when Upper arch is selected
- Verify tube options when Bands Ultimax anchorage is selected
- Verify configuration completion when all required Upper arch selections are provided

Keep scenario names concise, specific, and configuration-focused.

---

# OUTPUT STRUCTURE

Use Markdown tables.

## 1. Functional Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

Functional test cases must cover:

- Configuration entry point
- Initial configuration step
- Every major decision point
- Every valid option at important decision points
- Branch-specific behavior
- Actual paths shown in the PDF
- Downstream configuration options
- Successful completion of valid configurations
- Data retention between steps
- Correct transition from one step to the next

---

## 2. Validation Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

Cover:

- Required configuration selections
- Attempting to continue without required selections
- Conditional required fields
- Selection dependencies
- Invalid/incomplete configuration states
- Correct validation messages
- Validation behavior when changing a previous selection

---

## 3. Negative Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

Cover:

- Invalid configuration combinations **only where the flow indicates they are invalid**
- Unsupported branch navigation
- Missing required selections
- Invalid/unsupported values
- Configuration failure scenarios
- Error handling

Do NOT invent negative combinations that are not supported by the flow.

---

## 4. Edge Case Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

Consider configuration-specific edge cases such as:

- Switching Upper ↔ Lower
- Changing Anchorage after downstream selections
- Changing an earlier selection after completing later steps
- Resetting configuration
- Back/Next navigation
- Re-entering a previously configured step
- Boundary values where applicable
- Optional selections
- None selections
- Maximum/minimum supported configuration options
- State retention after navigation
- Refresh/reload behavior where relevant

Only include edge cases applicable to the configuration shown in the PDF.

---

## 5. API Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

If API behavior/endpoints are explicitly provided in the Epic/PDF, cover:

- Request payload
- Configuration values
- Selected option persistence
- Valid configuration submission
- Invalid configuration rejection
- Response status
- Response body
- Data integrity
- Configuration mapping

**IMPORTANT:**
If API details are NOT provided in the source, do not invent endpoint names, payload structures, or status codes. Clearly mark API coverage as requiring API specification if necessary.

---

## 6. UI/UX Test Cases

| TC-ID | Test Scenario | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- |

Cover configuration-specific UI behavior:

- Correct step displayed
- Correct options displayed
- Branch-specific options
- Selected-state behavior
- Disabled/enabled controls
- Next/Back navigation
- Conditional option visibility
- Labels and terminology
- Error/validation messages
- Configuration summary
- Responsive layout
- Element alignment
- Accessibility/WCAG basics
- Keyboard navigation where applicable

---

# CONFIGURATION FLOW TRACEABILITY

After the test cases, provide a **Flow Coverage Summary**.

| Flow / Decision Point | Options / Branches Identified | Covered By TC IDs |
| :--- | :--- | :--- |

Example:

| Flow / Decision Point | Options / Branches Identified | Covered By TC IDs |
| :--- | :--- | :--- |
| Select Arch | Upper, Lower | FT-02, FT-03 |
| Select Anchorage – Upper | Bands Ultimax, Bands Rollo, None | FT-04, FT-05, FT-06 |
| Select Anchorage – Lower | Bands Ultimax, Bands Rollo, None | FT-07, FT-08, FT-09 |

This section is **mandatory** because it proves that every important branch in the PDF has been covered.

---

# HAPPY PATH REQUIREMENT

For every major branch shown in the configuration flow, provide at least one complete happy-path test from:

**Configuration Start → Decision Point → Selected Option → Next Decision → Applicable Configuration → Completion**

Do not stop the test case halfway through the flow if the branch can be completed.

---

# OPTIMIZATION RULE

The goal is **maximum meaningful flow coverage with minimum redundant test cases**.

DO NOT create:

- Every possible combination of every option
- Duplicate test cases for visually repeated paths
- Combinations that are not connected in the PDF
- Tests based on assumptions
- Generic tests that do not relate to the configuration flow

Instead:

**Cover every unique decision/branch/path shown in the PDF.**

Think like a Senior QA Engineer optimizing a regression suite that may otherwise contain 50–100+ manually maintained configuration test cases.

---

# SOURCE ACCURACY

Before generating test cases:

1. Identify the configuration hierarchy.
2. Identify the first decision point.
3. Identify all branches.
4. Trace each branch to its next decision point.
5. Identify branch-specific options.
6. Identify the final completion path.
7. Generate test cases only after understanding the flow.

If the PDF text extraction and visual diagram appear inconsistent:

**Use the visual flow/connector relationships as the primary reference.**

If something still cannot be determined confidently, explicitly state:

> "The flow diagram does not provide enough information to determine this relationship, so no test case has been generated for this combination."

---

# PRIORITY

Use only:

- **Critical** – Core configuration path / configuration cannot be completed without it
- **High** – Important branch or major configuration functionality
- **Medium** – Secondary configuration behavior
- **Low** – Minor UI/UX or less critical scenarios

Do NOT use P0/P1/P2/P3.

---

# FINAL QA SUMMARY

At the end provide:

### Configuration Flow Summary
Briefly explain the hierarchy of the configuration flow.

### Coverage Summary
- Total Functional cases
- Total Validation cases
- Total Negative cases
- Total Edge cases
- Total API cases
- Total UI/UX cases
- Total test cases

### Branch Coverage
Mention whether every identifiable branch in the PDF has been covered.

### Ambiguities / Assumptions
List only items that could not be conclusively determined from the PDF.

### QA Recommendation
Recommend whether the generated suite is suitable for:
- Smoke testing
- Regression testing
- Full functional testing

---

## INPUT

Analyze the following Configuration Flow PDF:

**[ATTACH CONFIGURATION FLOW PDF HERE]**

Optional Epic / Requirement:

**[INSERT EPIC DESCRIPTION HERE]**