# 🧪 REST API Validation & Regression Suite

[![Automated REST API Tests](https://github.com/jelmardegoro-byte/postman-api-validation/actions/workflows/api-tests.yml/badge.svg)](https://github.com/jelmardegoro-byte/postman-api-validation/actions/workflows/api-tests.yml)
[![Postman](https://img.shields.io/badge/Postman-v10+-FF6C37?style=flat&logo=postman&logoColor=white)](https://www.postman.com/)
[![Newman](https://img.shields.io/badge/Newman-CLI_Runner-FF6C37?style=flat)](https://github.com/postmanlabs/newman)
[![JavaScript](https://img.shields.io/badge/JavaScript-Test_Scripts-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![QA Engineer](https://img.shields.io/badge/QA-Regression_%26_Functional-2563EB?style=flat)](https://jelmardegoro.vercel.app/)

A structured API test automation and data validation suite built with **Postman** and **Newman CLI**. 

This project simulates enterprise insurance portal validation: verifying HTTP contracts, data types, schema integrity, and performing field-by-field reconciliation between backend API responses and UI portal state.

> **Environment Note:** Utilizes [JSONPlaceholder](https://jsonplaceholder.typicode.com) as a simulated policyholder microservice. All test payloads are mock data; no proprietary or enterprise client data is included.

---

## 🎯 Test Suite Architecture

| ID | Test Scenario | Scope | Validations & Assertions |
|:---|:---|:---|:---|
| **TC-01** | `GET /users/{id}` (Valid ID) | Functional | Status `200 OK`, response time `< 1500ms`, Content-Type `application/json`, required field existence, data types, and email regex formatting |
| **TC-02** | `GET /users/{id}` (Unknown ID) | Negative | HTTP `404 Not Found`, data leak prevention, empty response payload |
| **TC-03** | `GET /users/{id}` (Invalid Format) | Negative / Edge Case | Malformed ID sanitization, proper client error status, no server stack trace leakage |
| **TC-04** | API vs. Portal UI Reconciliation | Data Integrity | Field-by-field verification comparing API JSON against portal session variables (`portal_name`, `portal_email`, `portal_city`, `portal_phone`, `portal_zipcode`). Reports deliberate field mismatches |
| **TC-05** | `GET /users` (Full Collection) | Regression | Dataset size validation, unique primary key validation, required attributes per record, and batch regex compliance |

---

## 🔍 Intentional Defect Injection (TC-04)

In enterprise insurance workflows, a backend database update may fail to propagate correctly to client-facing portal views.

- **TC-04** purposefully injects a discordant `portal_zipcode` value against the live API response.
- The test script catches this difference, logs the mismatch to the Postman Console, and triggers a structured defect report.
- See **[`SAMPLE_BUG_REPORT.md`](./SAMPLE_BUG_REPORT.md)** for the enterprise defect ticket format (Severity, Steps to Reproduce, Expected vs. Actual, and Logs).

---

## 🚀 Execution Instructions

### Option 1: Headless via Newman CLI (CI/CD Ready)
```bash
# Install Newman globally
npm install -g newman

# Execute test suite with CLI report
newman run Policyholder_API_Validation.postman_collection.json
```

### Option 2: In Postman GUI
1. Open Postman and click **Import**.
2. Select `Policyholder_API_Validation.postman_collection.json`.
3. Select the collection &rarr; Click **Run** &rarr; **Run Policyholder API Validation**.
4. Open the **Postman Console** (`Ctrl + Alt + C` / `Cmd + Option + C`) to inspect validation output.

---

## ⚙️ Automated CI Pipeline
This repository includes a native **GitHub Actions** workflow (`.github/workflows/api-tests.yml`). On every push to `main`, tests execute automatically in a clean headless environment via Newman, guaranteeing continuous test health and zero regressions.

---

## 👨‍💻 Author
**Jelmar Degoro** — QA Engineer & Full-Stack Developer  
- **Portfolio**: [jelmardegoro.vercel.app](https://jelmardegoro.vercel.app/)  
- **GitHub**: [@jelmardegoro-byte](https://github.com/jelmardegoro-byte)
