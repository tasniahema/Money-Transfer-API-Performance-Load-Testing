# Fintech API Load Testing — JMeter Test Plan

This repository contains a **complete JMeter Test Plan** for load testing a fintech transaction system, including money transfers, deposits, withdrawals, and payments. The tests are designed to simulate realistic user and admin activity while verifying performance, correctness, and system behavior under load.

---

## 🗂 Project Structure
```text
Test Plan
├── Thread Group 1 (Admin Setup)
│   ├── POST login (Admin)
│   ├── POST user-create (Customer1)
│   ├── POST user-create (Customer2)
│   ├── POST user-create (Agent)
│   ├── POST user-create (Merchant)
│   ├── GET user-list
│   ├── GET search-user-by-email
│   ├── GET search-user-by-id
│   ├── POST admin-create-virtual-money
│   ├── POST deposit-system-to-agent
│   ├── POST Deposit (SYSTEM → Customer)
│   └── GET system-virtual-balance
│
├── Commission
│   ├── GET commission listing
│   └── POST create commission
│
└── Thread Group 2 (User Load Test)
    ├── POST login (Customer)
    ├── POST login (Agent)
    ├── POST login (Merchant)
    ├── GET balance-check
    ├── GET transaction-history
    ├── GET transaction-details
    ├── POST Deposit (AGENT → Customer)
    ├── POST withdraw-customer-to-agent
    ├── POST send-money-customer-to-customer
    └── POST payment-customer-to-merchant


---

## ⚙ Environment

- **OS**: Windows 11  
- **Tool**: Apache JMeter 5.6+  
- **Browser / Client**: N/A (API load test)  
- **API Base URL**: `https://mta.newroztech.com/api`  

---

## 🔑 Configuration

1. **Global Variables / Properties**
   - Admin and user tokens are stored in **JMeter properties** for reuse across thread groups.
   - Customer and merchant details (email, phone) are dynamically generated and stored using **JSON Extractors** and **BeanShell PostProcessors**.

2. **Headers**
   - `Authorization: Bearer <token>`  
   - `AUTH-SECRET-KEY: <secret>`  
   - `Content-Type: application/json`  
   - `Accept: application/json`  

3. **Dynamic Variables**
   - Customer emails and phone numbers are stored globally for cross-thread access.
   - Transaction IDs are captured from responses to test transaction detail APIs.

---

## 🏃‍♂️ How to Run

1. Open **JMeter** on Windows 11.
2. Load the `.jmx` file for this test plan.
3. Make sure **Thread Groups** are configured to **run consecutively**.
4. Start the test.
5. View results using **View Results Tree** and **Aggregate Report** listeners.

---

## 📊 Test Coverage

This test plan covers:

- Admin operations:
  - Login
  - User creation (Customer, Agent, Merchant)
  - Virtual money management
  - System balance check
  - Commission creation and listing

- User operations:
  - Login (Customer, Agent, Merchant)
  - Balance check
  - Transaction history and details
  - Deposits and withdrawals
  - Money transfer (Customer → Customer)
  - Payment (Customer → Merchant)

- Load Testing Scenarios:
  - Concurrent users performing transactions
  - System performance under multiple deposits, withdrawals, and transfers
  - Response validation (Status code, Content-Type, transaction data)

---

## 💡 Notes & Best Practices

- Always run **Thread Group 1 (Admin Setup)** before **Thread Group 2 (User Load Test)** to ensure users are created and tokens are valid.
- Use **Debug Sampler** to validate variable extraction before using them in subsequent requests.
- Avoid duplicate headers (especially `Authorization`) to prevent 400 Bad Request errors.
- Use **properties** for cross-thread variables and **vars** for same-thread variables.
- For production-level load testing, configure **Thread Group ramp-up, loops, and timers** according to expected user load.

---

## 📌 References

- [Apache JMeter User Manual](https://jmeter.apache.org/usermanual/index.html)
- [JSON Extractor Documentation](https://jmeter.apache.org/usermanual/component_reference.html#JSON_Extractor)
- [BeanShell / JSR223 PostProcessor](https://jmeter.apache.org/usermanual/component_reference.html#JSR223_PostProcessor)

---
**Running the JMeter Test & Generating Report**
1. Open Command Prompt
Navigate to the JMeter bin directory:cd F:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin


2. Run the Test Plan in Non-GUI Mode
Execute the following command to run the test and save results:
jmeter -n -t "F:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\Money Transfer System Load Testing.jmx" -l "F:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\results.csv" -e -o "F:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\html_report"

Explanation of parameters:
-n → Run in non-GUI mode
-t → Path to your .jmx test plan
-l → Path to save results CSV
-e -o → Generate HTML report in the specified folder

3. Open the Generated HTML Report
Once the test finishes, open the report in your browser:start "" "F:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\html_report\index.html"


Notes:
Make sure the .jmx file exists at the specified path.
Ensure you have proper permissions to create files in the output folder.
Warnings about package scanning can be ignored; they do not prevent report generation.
---

---

## Author
**Tasnia Sultana Hema**
Jr.SQA Engineer 
