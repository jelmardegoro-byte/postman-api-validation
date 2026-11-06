# Policyholder API Validation (Sample Project)

A sample API testing project built with **Postman**. It shows how I validate an API's responses and compare them against what a user-facing portal displays, which mirrors the kind of validation I do in insurance portal QA work.

> **Note:** This project uses the free public [JSONPlaceholder](https://jsonplaceholder.typicode.com) API as a stand-in for a policyholder API. All data is public or made up. No employer or client data is used.

## What it covers

| ID | Test case | Type | What it checks |
|----|-----------|------|----------------|
| TC-01 | Get policyholder, valid ID | Functional | Status 200, response time, JSON content type, required fields, data types, email format, address fields |
| TC-02 | Get policyholder, unknown ID | Negative | 404 returned and no data leaked |
| TC-03 | Get policyholder, invalid ID format | Negative | Malformed ID rejected, no record data returned |
| TC-04 | Compare API data to portal display | Data validation | Field-by-field comparison of API values against simulated portal values, with mismatch reporting |
| TC-05 | List all policyholders | Regression | Record count, unique IDs, required fields, email format on every record |

## The data-mismatch check (TC-04)

Portal display values are stored as collection variables (`portal_name`, `portal_email`, `portal_city`, `portal_phone`, `portal_zipcode`). TC-04 compares each one with the API response and logs any difference in the Postman Console.

The `portal_zipcode` value is **deliberately wrong** to prove the check detects a real mismatch. The test passes when it finds that exact defect and nothing else. See `SAMPLE_BUG_REPORT.md` for how I would report it.

## How to run it

1. Open Postman and choose **Import**, then select `Policyholder_API_Validation.postman_collection.json`.
2. Click the collection, then **Run**, then **Run Policyholder API Validation**.
3. Open the **Console** (View > Show Postman Console) to see mismatch warnings.

Optional, from the command line with [Newman](https://github.com/postmanlabs/newman):

```
npm install -g newman
newman run Policyholder_API_Validation.postman_collection.json
```

## Skills demonstrated

API testing, test case design (happy path, negative, regression), assertions and test scripting in JavaScript, data validation between API and UI, and defect reporting.
