# Sample Bug Report

*Made-up example based on the mismatch check in TC-04. No real system or client data.*

| Field | Detail |
|-------|--------|
| **Bug ID** | BUG-001 |
| **Title** | Policyholder zipcode shown in portal does not match API value |
| **Severity** | Medium |
| **Priority** | Medium |
| **Environment** | Test environment, Postman v11, Chrome |
| **Found in** | TC-04 Compare API data to portal display |

## Description
The zipcode displayed on the policyholder portal page does not match the zipcode returned by the policyholder API for the same record. All other compared fields (name, email, city, phone) match.

## Steps to reproduce
1. Send `GET /users/1` and note `address.zipcode` in the response.
2. Open the portal page for the same policyholder (ID 1).
3. Compare the zipcode shown in the portal with the API value.

## Expected result
The portal zipcode matches the API value: `92998-3874`.

## Actual result
The portal shows `92998-0000`.

## Impact
An incorrect zipcode could produce wrong quotes, misrouted mail, or failed address validation for the policyholder.

## Evidence
Postman Console warning:
`MISMATCH [zipcode] API=92998-3874 | Portal=92998-0000`

## Suggested next step
Check how the portal populates the zipcode field (data mapping or caching) and confirm which source is correct.
