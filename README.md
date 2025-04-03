<<<<<<< HEAD
# QA-ANALYST-TAKE-HOME-ASSESSMENT
QA Analyst Take-Home Assessment for Linq. This repository contains manual test cases, bug reports, and notes for testing the Linq app user flow. It also includes API inspection using Postman and a comprehensive documentation of test scenarios and findings.
=======
# QA Analyst Take-Home Assessment Submission – ASHWITHA VOLLEM

## Overview  
This repository contains my submission for the **QA Analyst Take-Home Assessment** for Linq. The task involved testing a real user flow in the **Linq production app** (viewing a profile and saving contact info as a visitor), identifying bugs, and analyzing API interactions using **Postman**.  

My approach focused on **clarity, depth, structure, and curiosity**, ensuring a well-documented and thorough assessment.  

---

## Repository Structure  

📂 **`test-cases.md`** – A comprehensive list of **20 manual test cases** covering the visitor flow on [Linq Profile](https://linqapp.com/ashu_reddy?r=link).  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Organized based on the natural user journey (profile loading, contact exchange, post-exchange actions).  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Covers edge cases, validation checks, and mobile responsiveness.  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Each test case includes a **Test Case ID, Description, Steps, and Expected Result**.  

🐞 **`bugs.md`** – A **detailed bug report** documenting 3 critical issues found during testing.  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Each bug includes **Bug ID, Test Case ID, Steps to Reproduce, Actual vs. Expected Results, Severity, Priority, and Screenshots**.  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Identified issues range from **data integrity (duplicate submissions)** to **usability concerns (unexpected vCard prompts)** and **input validation flaws**.  

🔍 **`postman-notes.md`** – API analysis using **Postman** for the endpoint [`https://api.linqapp.com/api/v2/cards/ashu_reddy/contact_downloads`](https://api.linqapp.com/api/v2/cards/ashu_reddy/contact_downloads).  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Request and response breakdown, security concerns, and validation gaps.  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Key findings: **No authentication required, weak input validation, and unclear rate limiting**.  
&nbsp;&nbsp;&nbsp;&nbsp;✔ Additional **questions for further exploration**.  

📖 **`README.md`** – This file, providing an overview of the submission.  

🖼 **Screenshots** – Included in `bugs.md` to support findings.  

---

## Key Highlights  

### ✅ Test Cases  
I created **20 structured test cases**, covering:  
✔ **Happy Paths** – Successful contact exchanges (phone, email, etc.).  
✔ **Edge Cases** – Invalid inputs, empty fields, and duplicate submissions.  
✔ **Usability Checks** – Mobile responsiveness, keyboard navigation, and UI behavior.  

Each test case is designed to be **clear, repeatable, and actionable** for developers.  

### 🐛 Bug Reports  
I identified **3 critical issues**, including:  
- **Bug 001:** Duplicate contact submissions allowed without validation.  
- **Bug 002:** Automatic vCard download prompt may disrupt user experience.  
- **Bug 003:** Name field accepts invalid characters, leading to data inconsistencies.  

Each report includes **detailed reproduction steps, severity/priority ratings, and suggested fixes**.  

### 🔬 API Inspection (Postman Analysis)  
I analyzed the **contact exchange API request** using **Postman** and found:  
🚨 **No authentication required**, posing a security risk.  
🚨 **Weak input validation**, allowing invalid characters.  
🚨 **No clear rate limiting**, which may allow excessive API requests.  

I documented these concerns and **raised questions for further security and performance improvements**.  

---

## Approach  

🧐 **Exploratory Testing:** Navigated the app manually to observe real user interactions.  
📝 **Structured Documentation:** Created clear, well-organized test cases and bug reports.  
🛠 **Technical Depth:** Used DevTools to analyze network activity and Postman for API simulations.  
💡 **Curiosity & Proactiveness:** Explored potential security concerns and usability improvements beyond basic testing.  

---

## Tools Used  

- **Google Chrome (Desktop & Mobile)** – Manual testing.  
- **Chrome DevTools** – Inspecting network requests, UI responsiveness.  
- **Postman** – API analysis and testing.  
- **GitHub** – Organizing and submitting my work.  

---

## Conclusion  
This submission reflects my **attention to detail, structured problem-solving skills, and technical depth** in both **manual testing and API analysis**.  

>>>>>>> e8a7bc9 (Added postman-notes.md, README.md, and Bonus.md)
