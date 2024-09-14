# Loan Approval DAML Project

This project implements a basic loan approval workflow using DAML. It consists of two templates:
1. `LoanRequest` - Represents a request for a loan.
2. `Loan` - Represents an approved loan.

## Project Structure

- `Main.daml`: Defines the templates and loan approval logic.
- `TestLoanApproval.daml`: Contains test scripts to validate the loan approval process with additional test cases.

## Steps to Build and Run the Project

### Prerequisites
- Install DAML SDK (version 2.9.4 used in this project)
- Ensure you have set up a DAML environment.

### 1. Building the Project
To build the DAML project, run:

```bash
daml build

This will generate the .dar file for the project located in the dist directory.

2. Running the Project
Start the DAML application by running:


daml start


This will start a local ledger, navigator, and JSON API.
3. Running the Test Script
To test the loan approval workflow, execute the test script using the following command:

```bash
daml script --dar .daml/dist/LoanApprovalProject-0.0.1.dar --script-name TestLoanApproval:testLoanApproval --ide-ledger


This script tests two scenarios:
The approval of the first LoanRequest.
Verifying that the second LoanRequest remains active.
4. Output
After running the script, the following output will be generated:

```bash
[DA.Internal.Prelude:557]: ("Loan 1:",[(0050a4a365c664088a04f68b92f9594199c2a7f10ed8effe0cd048a980b3dbc21f,Loan {borrower = 'Borrower', bank = 'Bank', amount = 100.0})])
[DA.Internal.Prelude:557]: ("Active LoanRequest 2:",[(00418297da0078c38edd349bf27d249a5b40ab516c83eb0b3830bd4cd8242dd04c,LoanRequest {borrower = 'Borrower', bank = 'Bank', amount = 200.0})])


Loan 1: Shows that the first LoanRequest was approved, and the Loan contract was created with a loan amount of 100.0.
Active LoanRequest 2: Confirms that the second LoanRequest is still active, with a loan amount of 200.0.
Explanation of Test Cases
Test Case 1: Approve the First Loan Request
The borrower submits two loan requests, one for 100.0 and another for 200.0.
The bank approves the first loan request.
The system verifies that a Loan contract is created for the approved request.
Test Case 2: Keep the Second Loan Request Active
The second loan request remains unapproved, ensuring that it stays active on the ledger.
The debug output confirms that the second LoanRequest is still present.

Conclusion
This project demonstrates a simple loan approval process in DAML, with tests to ensure that requests can be approved or remain active based on the workflow logic.
