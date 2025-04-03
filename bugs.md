# Bugs Identified in Linq Profile and Contact Save Flow (Visitor Perspective)

This file documents bugs and usability issues found while testing the feature flow on https://linqapp.com/ashu_reddy?r=link: viewing a profile and attempting to save contact info as a visitor. Each bug includes a description, steps to reproduce, actual and expected results, severity, priority, environment, and screenshots (where applicable).

## Bug 1: Duplicate Contact Info Submissions Are Saved Without Warning

| **Bug ID** | 001 |
|------------|-----|
| **Test Case ID** | TC15 |
| **Description** | When a visitor submits the same contact info (same name and phone number) multiple times, the app saves the information each time without any warning or deduplication. This leads to duplicate entries being stored, which can cause data integrity issues and confusion for the user. |
| **Steps to Reproduce** | 1. Navigate to https://linqapp.com/ashu_reddy?r=link<br>2. Click "Exchange Contact"<br>3. Enter name (e.g., "visitor1") and phone number (e.g., +1 513-111-1111)<br>4. Click "Continue"<br>5. Repeat steps 2-4 with the same name and phone number |
| **Actual Result** | The app saves the duplicate contact info each time, showing the success modal ("You just connected with Ashu") for both submissions. |
| **Expected Result** | The app should either prevent the duplicate submission and display a message (e.g., "You have already connected with Ashu using this contact info") or allow the submission but deduplicate the data on the backend to avoid storing redundant entries. |
| **Severity** | Medium (data integrity issue; duplicate entries can affect analytics and user experience) |
| **Priority** | Medium (not a critical failure, but impacts data quality and user trust) |
| **Environment** | Mobile browser (Google Chrome on iOS), https://linqapp.com/ashu_reddy?r=link |
| **Screenshot** | Not applicable; behavior is functional, not visual |

## Bug 2: Automatic vCard Download Prompt After Clicking "Continue" Without In-App Confirmation

| **Bug ID** | 002 |
|------------|-----|
| **Test Case ID** | TC04, TC05, TC06, TC07, TC16 |
| **Description** | After clicking "Continue" in the "Exchange info with Ashu" modal, the app automatically triggers a browser prompt to download a vCard file (e.g., "Ashu_Reddy2241409.vcf") without first asking the user for confirmation within the app. While the browser does prompt the user to save or cancel the download, this initial trigger can be unexpected and intrusive, especially on mobile devices where download prompts may disrupt the user experience. |
| **Steps to Reproduce** | 1. Navigate to https://linqapp.com/ashu_reddy?r=link<br>2. Click "Exchange Contact"<br>3. Enter name (e.g., "visitor1") and phone number (e.g., +1 513-111-1111)<br>4. Click "Continue" |
| **Actual Result** | The browser immediately prompts to save a vCard file (e.g., "Ashu_Reddy2241409.vcf"). The file does not download automatically; the user must click "Save" to download or "Cancel" to skip. If the user cancels, the success modal ("You just connected with Ashu") appears. |
| **Expected Result** | The app should first display an in-app confirmation (e.g., a modal with "Would you like to save Ashu’s contact?") before triggering the browser download prompt. Alternatively, the app should not trigger the download automatically and rely on the "Download Contact" link (as in TC10) for manual downloads. After the user saves or cancels the download, the success modal should still appear. |
| **Severity** | Medium (usability issue; unexpected download prompt can disrupt user experience) |
| **Priority** | Medium (not a critical failure, but impacts user experience, especially on mobile) |
| **Environment** | Chrome browser, Windows OS (desktop), https://linqapp.com/ashu_reddy?r=link |
| **Screenshot** | [Screenshot of the browser save prompt; screenshot of the success modal after canceling] |


## Bug 3: Name Field Accepts All Characters Including Invalid Ones

| **Bug ID** | 003 |
|------------|-----|
| **Test Case ID** | TC13 |
| **Description** | The Name field in the "Exchange info with Ashu" modal accepts all characters, including invalid ones like numbers, special characters, and symbols (e.g., "#$%", or "123#$%"). In reality, a name should primarily contain alphabetic characters (letters A-Z, a-z) and possibly spaces or hyphens for realistic names (e.g., "visitor" ). The app should validate the Name field to prevent invalid characters from being accepted. |
| **Steps to Reproduce** | 1. Navigate to https://linqapp.com/ashu_reddy?r=link<br>2. Click "Exchange Contact"<br>3. In the Name field, enter a name with invalid characters (e.g., "#$%", or "123#$%")<br>4. Enter a valid phone number (e.g., +1 123-111-1111)<br>5. Click "Continue" |
| **Actual Result** | The app accepts the input (e.g., "#$%", or "123#$%") as a valid name, proceeds with the contact exchange, and shows the success modal ("You just connected with Ashu"). The invalid name is saved in the backend. |
| **Expected Result** | The app should validate the Name field to ensure it primarily contains alphabetic characters (letters A-Z, a-z) and allows only specific characters like spaces or hyphens for realistic names (e.g., "visitor"). If the input contains invalid characters like numbers or special characters (e.g., "123", "#$%"), the app should display a validation error (e.g., "Name can only contain letters, spaces, or hyphens") and prevent submission until the input is corrected. |
| **Severity** | Medium (validation issue; allows incorrect data to be saved, affecting data quality) |
| **Priority** | Medium (not a critical failure, but impacts data integrity and user trust) |
| **Environment** | Chrome browser, Windows OS (desktop), https://linqapp.com/ashu_reddy?r=link |
| **Screenshot** | [Screenshot of the Name field with invalid characters (e.g., "@@@@@");
![Bug screenshot]( https://github.com/AshwithaReddy1/QA-ANALYST-TAKE-HOME-ASSESSMENT/blob/main/Screenshot%202025-04-02%20205230.png )  ]|



