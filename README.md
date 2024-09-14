# Loan Approval Workflow Project

This project implements a simple loan approval workflow using DAML. It demonstrates the process of creating a loan request, approving it, and disbursing funds, as well as handling scenarios such as attempting to approve a loan that exceeds the bank's limit.

## Project Structure

The project consists of three main files:

1. `Main.daml`: Contains the main templates and choices for the loan approval workflow.
2. `TestLoanApprovalWorkflow.daml`: Contains a test script that demonstrates the workflow.
3. `daml.yaml`: The project configuration file.

## Templates

- `Token`: Represents the disbursed loan amount.
- `LoanLimit`: Defines the maximum amount a bank can lend.
- `LoanRequest`: Represents a borrower's request for a loan.
- `Loan`: Represents an approved loan.

## Workflow

1. A `LoanLimit` is set for the bank.
2. A borrower creates a `LoanRequest`.
3. The bank approves the `LoanRequest`, creating a `Loan`.
4. The bank disburses the loan amount, creating a `Token` for the borrower.

## Running the Project

To run this project, follow these steps:

1. Ensure you have DAML SDK installed (version 2.9.4 used in this project).

2. Clone the repository and navigate to the project directory.

3. Build the project:
   ```
   daml build
   ```

4. Start the DAML sandbox and navigator:
   ```
   daml start
   ```

5. In a new terminal, run the test script:
   ```
   daml script --dar .daml/dist/loan-approval-project-0.1.0.dar --script-name TestLoanApprovalWorkflow:testLoanApprovalWorkflow --ide-ledger
   ```

## Test Script Output

When you run the test script, you should see output similar to this:

```
[DA.Internal.Prelude:557]: "Allocated parties: Bank and Borrower"
[DA.Internal.Prelude:557]: "Created LoanLimit with cid: 00a2fa046944af9919370df37308d39c1c7d402edea3033eec4bc3383e9b9fb8a5"
[DA.Internal.Prelude:557]: "Created LoanRequest with cid: 00418297da0078c38edd349bf27d249a5b40ab516c83eb0b3830bd4cd8242dd04c"
[DA.Internal.Prelude:557]: "Approved LoanRequest. Created Loan with cid: 0073196fca7536f8b463085039cc844115d7f75286660923cb504f6b355e960460"
[DA.Internal.Prelude:557]: "Disbursed full loan amount. New Loan cid: 00f989f30aff5709a4566ea314f6d0adb29ab667d8bee2edfb9a33f95564f76bfe"
[DA.Internal.Prelude:557]: "Created over-limit LoanRequest with cid: 00a6dd6b5c32f47e2089e6578db307b23ba75a10a7c22b56f974071194dee098f7"
[DA.Internal.Prelude:557]: "Attempting to approve over-limit loan request (this should fail)"
[DA.Internal.Prelude:557]: "Test completed successfully!"
```

This output confirms that the loan approval workflow is functioning as expected, including the successful creation and approval of a valid loan request, and the failure to approve a loan request that exceeds the bank's limit.
