
# Email Verification Setup with Azure Logic App

This project implements a simple email verification system where users must enter a 6-digit code sent to their email. The system verifies the code by communicating with an Azure Logic App, which handles the verification process.

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Setup Steps](#setup-steps)
4. [Azure Logic App Configuration](#azure-logic-app-configuration)
5. [Front-End Setup](#front-end-setup)
6. [Testing](#testing)
7. [Notes](#notes)

## Overview

This project allows users to verify their identity by entering a 6-digit code that is sent to their email. The verification process involves:

1. **User requests a verification code.**
2. **A 6-digit verification code is sent to the user's email** via the Azure Logic App.
3. **User enters the verification code** on the front-end.
4. The code is verified by the Azure Logic App, which checks if the code matches the expected value.

### Key Components

- **Front-End (HTML, CSS, JavaScript):** 
    - Collects the user's 6-digit code input and sends it to the Azure Logic App for verification.
    - Displays success or failure messages based on the response from the Logic App.
  
- **Azure Logic App:**
    - Receives the verification request from the front-end.
    - Sends a 6-digit code to the user's email.
    - Verifies the code entered by the user and sends a response back.

## Prerequisites

Before proceeding, ensure you have the following:

1. **Azure Account:** Set up an Azure account at [Azure Portal](https://portal.azure.com/).
2. **Azure Logic App:** Create and configure an Azure Logic App to handle verification requests.
3. **Email Service:** An email service (like Office 365, Gmail, etc.) configured in the Logic App to send emails.
4. **Knowledge of JSON:** Basic understanding of JSON, as it is used to structure the data exchanged between the front-end and Logic App.

## Setup Steps

### 1. Azure Logic App Configuration

1. **Create a New Logic App:**
    - Go to the [Azure Portal](https://portal.azure.com/).
    - Search for "Logic Apps" and create a new Logic App.

2. **Set Up Trigger and Workflow:**
    - In the Logic App designer, add a trigger to start the workflow. Use the trigger "When an HTTP request is received."
    - Add the necessary steps to:
        - Generate a 6-digit verification code (this could be a random number generator or a fixed code for testing purposes).
        - Send the 6-digit code via email to the address passed in the request.
        - Return a success/failure response based on the code entered by the user.

3. **Create the Logic App Code:**
    - The logic app code, located in the `logicapp` folder, should be used as part of the setup. You may need to edit it to fit your requirements.
    - The code will include steps like:
        - HTTP trigger setup.
        - Actions to generate a random code.
        - Send an email via the connected email service.
        - Response step to return success/failure based on the user's input.

4. **Configure Connections:**
    - Set up connections to your email service (e.g., Office 365, Gmail) within the Logic App.
    - You'll need to authorize access to your email account for sending emails.

5. **Get the Logic App URL:**
    - Once your Logic App is configured, obtain the endpoint URL generated by the HTTP trigger. This URL will be used in your front-end code to interact with the Logic App.

### 2. Front-End Setup

1. **Edit the HTML File:**
    - The front-end consists of an HTML form where users will enter the 6-digit verification code.
    - The `verificationForm` will collect the input from the user and send it to the Logic App for verification.

2. **JavaScript Logic:**
    - The front-end JavaScript handles the user's input and sends a POST request to the Azure Logic App. 
    - It checks whether the code entered is valid (6 digits).
    - The request sends the session ID and the input code to the Logic App for validation.

3. **Email Display:**
    - The email where the code is sent is displayed dynamically using the `localStorage.getItem('email')`.

### 3. Testing

1. **Test the Logic App:**
    - Before testing the front-end, ensure that the Logic App is correctly set up and able to send verification codes.
    - You can test the Logic App by triggering it manually from the Azure Portal.

2. **Test the Front-End:**
    - Open the HTML page in a browser and enter a 6-digit code.
    - If everything is set up correctly, the front-end should send the code to the Logic App and receive a success or failure response.

3. **Verify Code Entry:**
    - The logic app will compare the entered code with the one generated and sent to the user's email.
    - If the code matches, the Logic App will return a success message, and the front-end will display "Verification successful!" and redirect to the `home.html` page.

## Notes

- Make sure to secure the Logic App by validating the request and ensuring that only authorized clients can call it.
- The verification code generation logic can be modified according to your security and complexity requirements.
- This system is meant for basic verification scenarios. You can extend it to include features like time expiration for the code, limiting retry attempts, etc.
