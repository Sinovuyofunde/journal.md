


# Function Decomposition Challenge

## 1. Responsibilities Identified

The original function does many things:

Input validation (checking null/empty data)
Source specific pre-processing (CSV, API, manual).

* Location validation (IP address, cell phone, WiFi)
  Further reduce the risk of fraud by preventing email and phone number duplication.
  The data transformation (formatting names, dates, address) has been applied.
  Business rules (age limits, postal rules)
  Discuss error handling and logging.
  A query that returns data based on groups. (valid, invalid, duplicate)
* Database saving
  Generate a report (summary results)
* Counting errors and error times

---

## 2. Decomposition Plan

Divide into smaller functions with a specific purpose:

### A. Validation Layer

* validateEmail()
* validatePhone()
* validateDateOfBirth()
* validateAddress()
* validateRequiredFields()

### B. Preprocessing Layer

* preprocessRecordBySource()
* preprocessCsvRecord()
* preprocessApiRecord()
* preprocessManualRecord()

### C. Deduplication Layer

* isDuplicateEmail()
* isDuplicatePhone()

### D. Transformation Layer

* formatName()
* normalizePhoneNumber()
* formatAddress()
* parseDate()

### E. Processing Layer

* processSingleRecord()
* processBatchRecords()

### F. Reporting Layer

* buildProcessingReport()
* calculateErrorStats()

### G. Persistence Layer

* saveValidRecordsToDatabase()

---

## 3. Simplified Flow - Refactored Main Function

The main function needs to coordinate ONLY:

* start timer
* loop records
* call processSingleRecord()
* collect results
* call saveValidRecordsToDatabase()
* return buildProcessingReport()

---

## 4. A helper function for use in examples

Before the function is called. (in the function itself)

The amount of mixed validation, parsing and logic throughout

### After:

function processSingleRecord(record, options)

* validate record
* preprocess record
* transform fields
* check duplicates
* return processed result

---

## 5. Benefits of Decomposition

* Very readable
* Each function should do one thing
* Easier debugging (isolated issues)
* Reusable validation functions
* Better unit testing
* Less cognitive overload
* More straightforward collaboration (several developers may work on various functions)

---

## 6. Reflection Questions

How did breaking it down help to make it easier to read?
It broke down a large complex function to smaller parts, so that the logic would be easier to understand.

---

### Most challenging part?

Finding overlapping responsibilities (Validation, Transformation, Business Rules).

---

### Most reusable function?

Validation functions (email, phone, date) as they can be used in lots of systems.

---

If you want, I can also compress it into a **1-page submission format** or turn it into a **PDF-ready document**.
