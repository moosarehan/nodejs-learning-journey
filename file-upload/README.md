# 📤 Multi-Field File Upload System with Multer

> A complete, beginner-friendly Node.js application demonstrating how to handle **secure multi-field file uploads** using Express, EJS, and **Multer**. Features custom disk storage, strict file size/MIME-type filters, and customized error boundaries.

---

## 🎯 What is File Upload in Node.js?

Browsers upload files using the `multipart/form-data` encoding format. Express does not parse this format out-of-the-box. This project demonstrates how to use **Multer**—a node.js middleware for handling multipart forms—to intercept incoming files, validate them against security policies, rename them using custom logic, and store them securely on the server's disk.

### ⚡ Key Features

*   **🗄️ Custom Disk Storage:** Saves files locally with randomized/timestamp-based filenames to prevent files from overwriting each other.
*   **📑 Multi-Field Support:** Accepts different file types in the same request payload (e.g., one profile photo AND multiple PDF documents).
*   **🛡️ Type Filtering (MIME-Type Validation):** Strict checks that permit only `.jpeg`/`.png` for images and `.pdf` for documents.
*   **⚖️ File Size Limits:** Built-in safeguards that enforce a strict **3MB size limit** per file to prevent Denial-of-Service (DoS) memory floods.
*   **💥 Error Boundaries:** Specialized error-handling middleware that catches and displays user-friendly errors for file size limits, invalid formats, or unexpected field names.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Badge | Purpose |
| :--- | :--- | :--- | :--- |
| **Backend Runtime** | **Node.js** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | JavaScript execution environment |
| **Framework** | **Express.js** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Routing and middleware core |
| **Upload Parser** | **Multer** | ![Multer](https://img.shields.io/badge/Multer-F25F22?style=flat-square&logo=npm&logoColor=white) | Multipart file stream parser |
| **Template Engine** | **EJS** | ![EJS](https://img.shields.io/badge/EJS-A91E50?style=flat-square&logo=ejs&logoColor=white) | Upload form frontend template |
| **Styling** | **Bootstrap 5** | ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) | CSS styling framework for the form |

---

## 🔄 File Stream Architecture

```text
  [ Client Browser ]                              [ Express Server / Multer ]
+----------------------+                       +----------------------------------+
| enctype:             |                       | 1. Intercepts request stream     |
| "multipart/form-data"|                       |                                  |
|                      |                       | 2. Evaluates limits & size       |
| - userfile (Image)   | -- (POST Request) --> |    (Max: 3MB)                    |
| - userdocuments (PDF)|                       |                                  |
| - username (Text)    |                       | 3. Passes through FileFilter     |
|                      |                       |    (Validates MIME types)        |
+----------------------+                       |                                  |
                                               | 4. Renames & saves to disk       |
                                               |    (Dest: ./uploads/)            |
                                               +-----------------+----------------+
                                                                 |
                                                                 v
                                                       [ Disk Directory ]
                                                       ./uploads/
                                                       └── 1717351600123.png
                                                       └── 1717351600456.pdf
```

---

## 📁 Project Directory Structure

```text
file-upload/
├── uploads/             # Destination folder where files are stored (automatically created)
├── views/
│   └── myform.ejs       # EJS form layout containing multi-field file inputs
├── index.js             # Main server logic, Multer setup, filters, routes, and error handlers
├── package.json         # NPM scripts and dependencies
└── README.md            # Documentation (this file)
```

---

## 📝 Multer Validation Matrix

The app configures two separate fields using `upload.fields()`, enforcing strict rules for each:

| Form Field Name | Input Type | Allowed File Extensions | Max File Count | File Size Limit |
| :--- | :--- | :--- | :--- | :--- |
| **`userfile`** | Single Image | `.jpg`, `.jpeg`, `.png` | 1 | 3 MB |
| **`userdocuments`** | Multiple Documents | `.pdf` | 3 | 3 MB |

---

## 🚀 Setup & Installation Guide

Follow these steps to set up and run the application locally:

### 1. Prerequisites
Ensure you have [Node.js](https://nodejs.org/) installed (v16.0.0 or higher).

### 2. Clone and Navigate
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/file-upload
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Running the App
*   **Development Mode (Auto-reloads on file changes):**
    ```bash
    npm start
    ```
*   **Production/Standard Mode:**
    ```bash
    node index.js
    ```

You should see:
```text
Server running on port 3000
```

### 5. Access the application
Open your web browser and visit: **[http://localhost:3000](http://localhost:3000)**

---

## 🧪 Testing Scenarios (Walkthrough)

Test the application limits to see how Multer and the error boundaries respond:

### Case A: Successful Upload (Happy Path)
1.  Enter your name.
2.  Choose a valid `.jpg` or `.png` file for the **Upload File** field.
3.  Choose one or two valid `.pdf` files for the **Documents File** field.
4.  Click **Submit**.
5.  *Expected Result (HTTP 200):* The server returns a JSON response listing metadata about your files (destination path, generated filename, file size, etc.).

### Case B: File Size Exceeded (Security Test)
1.  Attempt to upload a file larger than **3MB**.
2.  *Expected Result (HTTP 400):* The server returns a descriptive error message indicating the file is too large.

### Case C: Wrong File Type Uploaded (Validation Test)
1.  Choose a `.txt` or `.zip` file for the **Documents File** field.
2.  Click **Submit**.
3.  *Expected Result (HTTP 500):* The custom `fileFilter` throws an error: `Something went wrong: Only PDF are allowed for documents`.

### Case D: Too Many Files Uploaded (Limit Test)
1.  Attempt to upload **four** PDF files under the **Documents File** field.
2.  *Expected Result (HTTP 400):* The server returns a Multer error: `Error : Too many files uploaded!`.

---

## 🧠 What You'll Learn from This Project

1.  **Multipart Handling:** Understanding EJS forms using `enctype="multipart/form-data"`.
2.  **Disk Storage Configuration:** Customizing filename storage logic to use safe timestamps (`Date.now() + extname`).
3.  **Strict File Filter Strategies:** Validating file MIME types (`application/pdf`, `image/jpeg`) before writing bytes to disk.
4.  **Multer Error Boundaries:** Catching Multer errors using Express middleware (`error instanceof multer.MulterError`) to customize the HTTP response codes returned to the client.
5.  **Multi-field Processing:** Handling distinct constraints on multiple files simultaneously via `upload.fields()`.