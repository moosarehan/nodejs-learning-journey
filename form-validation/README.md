# 📝 Express Form Validation & Sanitization (Form Validation Project)

> A lightweight, complete Node.js project demonstrating how to secure backend endpoints using **express-validator** for schema constraints, sanitization hooks, and custom logic validations.

---

## 🎯 Project Overview

In backend development, validating and sanitizing user inputs is a crucial security barrier. This project demonstrates how to use the standard **`express-validator`** library to:
1.  **Validate Fields:** Ensure fields exist, meet length limits, and conform to specific formats (like alphanumeric strings, numeric age caps, or standard email addresses).
2.  **Sanitize Data:** Clean data before processing (e.g., downcasing email domains, stripping whitespace, and normalizing emails).
3.  **Implement Custom Rules:** Write custom JavaScript validators (e.g., prohibiting specific values like `"admin"`) and custom sanitizers.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Badge | Purpose |
| :--- | :--- | :--- | :--- |
| **Backend Runtime** | **Node.js** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | JavaScript execution environment |
| **Framework** | **Express.js** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Core server framework |
| **Validation Core** | **Express-Validator** | ![express-validator](https://img.shields.io/badge/express--validator-5C3E5A?style=flat-square) | Input validator and data sanitizer |
| **Template Engine** | **EJS** | ![EJS](https://img.shields.io/badge/EJS-A91E50?style=flat-square&logo=ejs&logoColor=white) | Dynamic server-side UI rendering |
| **Styling** | **Bootstrap 5** | ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) | CSS styling for forms and alert blocks |

---

## 🔄 Input Validation Pipe Flow

Here is how data passes through the validation pipeline:

```text
       [ HTML Form Input ]
      (e.g., username, pass)
                |
                v
       [ Express Router ]
      POST /saveform route
                |
                v
  +-------------+-------------+
  |  express-validator Pipe   |
  |                           |
  | 1. Checks basic types     |
  |    (isEmail, isNumeric)   |
  |                           |
  | 2. Filters strings        |
  |    (trim, toLowerCase)    |
  |                           |
  | 3. Runs Custom Logic      |
  |    (Not "admin"?)         |
  +-------------+-------------+
                |
        { Validation OK? }
         /            \
      [Yes]          [No]
       /                \
      v                  v
[ res.send(body) ]    [ res.render("myform", {errors}) ]
(Sends Sanitized Data) (Displays error cards in browser)
```

---

## 📋 Validation Rules Reference

The application applies the following criteria to inputs submitted to `/saveform`:

| Field Name | HTML Input Type | Validation Rules | Sanitization Applied | Custom Message |
| :--- | :--- | :--- | :--- | :--- |
| **`username`** | Text | Required; Must be at least 3 chars; Must contain letters only; Value cannot be `"admin"`. | Trims leading/trailing spaces; Converts all letters to lowercase. | `"Username is required."`<br>`"Username must contain only letters."`<br>`"Username 'admin' is not allowed."` |
| **`useremail`** | Email | Must be a valid email syntax. | Normalizes email address (removes Gmail dots, aliases, etc.). | `"Please provide a valid Email Id."` |
| **`userpass`** | Password | Length must be between 5 and 10 characters; Must be a strong password. | *None* | `"Password must be between 5 and 10 character long."`<br>`"Password must be strong."` |
| **`userage`** | Number | Must be numeric; Must be at least `18`. | *None* | `"Age must be numeric."`<br>`"Age must be at least 18 years old."` |
| **`usercity`** | Select option | Must be in `['Delhi', 'Mumbai', 'Goa', 'Agra']`. | *None* | `"City must be Delhi, Mumbai, Goa or Agra."` |

---

## 🚀 Setup & Installation Guide

Follow these steps to run the project on your machine:

### 1. Prerequisites
Ensure you have [Node.js](https://nodejs.org/) installed (v16.0.0 or higher).

### 2. Clone and Navigate
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/form-validation
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Run the Project
*   **Development Mode (Auto-reloads on file changes):**
    ```bash
    npm start
    ```
*   **Standard Mode:**
    ```bash
    node index.js
    ```

You should see:
```text
Express Server starts on port 3000!
```

### 5. Access the Form
Open your browser and navigate to:
👉 **[http://localhost:3000/myform](http://localhost:3000/myform)**

---

## 🧪 Testing Scenarios (Walkthrough)

Test the form inputs to see how the validation and sanitization hooks respond:

### Case A: Valid Submission (Happy Path)
1.  Enter Username: `John`
2.  Enter Email: `john.doe@gmail.com`
3.  Enter Password: `StrongPass123!` (contains uppercase, lowercase, number, symbol)
4.  Enter Age: `21`
5.  Select City: `Delhi`
6.  Click **Submit**.
7.  *Expected Result:* The page returns a JSON string showing your sanitized data:
    ```json
    {
      "username": "john",
      "useremail": "johndoe@gmail.com",
      "userpass": "StrongPass123!",
      "userage": "21",
      "usercity": "Delhi"
    }
    ```
    *(Note: `username` was downcased to `john` by the custom sanitizer).*

### Case B: Custom Username Rejection
1.  Enter Username: `admin` (or `ADMIN`)
2.  Enter other fields validly.
3.  Click **Submit**.
4.  *Expected Result:* The page re-renders displaying a red warning box:
    *   ❌ `Username "admin" is not allowed.`

### Case C: Soft Password / Wrong Length Check
1.  Enter Password: `123` (too short, weak structure).
2.  Click **Submit**.
3.  *Expected Result:* The warning box displays:
    *   ❌ `Password must be between 5 and 10 character long.`
    *   ❌ `Password must be strong.`

### Case D: Underage User Check
1.  Enter Age: `15`
2.  Click **Submit**.
3.  *Expected Result:* The warning box displays:
    *   ❌ `Age must be at least 18 years old.`
